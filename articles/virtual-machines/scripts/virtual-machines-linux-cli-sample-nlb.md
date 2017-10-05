---
title: "Пример скрипта Azure CLI. Создание виртуальной машины Linux с помощью NLB | Документация Майкрософт"
description: "Пример скрипта Azure CLI. Создание виртуальной машины Linux с помощью NLB"
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
ms.openlocfilehash: a0052605da9f0023d11cc9253d8aecfb1d452e1a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-highly-available-vm"></a><span data-ttu-id="0b22e-103">Создание высокодоступной виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="0b22e-103">Create a highly available VM</span></span>

<span data-ttu-id="0b22e-104">Этот пример скрипта позволяет создать все необходимые компоненты для запуска нескольких виртуальных машин Ubuntu, настроенных в высокодоступной конфигурации с балансировкой нагрузки.</span><span class="sxs-lookup"><span data-stu-id="0b22e-104">This script sample creates everything needed to run several Ubuntu virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="0b22e-105">После выполнения этого сценария будут созданы три виртуальные машины, которые будут добавлены в группу доступности Azure. Доступ к ним можно будет получить через Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="0b22e-105">After running the script, you will have three virtual machines, joined to an Azure Availability Set, and accessible through an Azure Load Balancer.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="0b22e-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="0b22e-106">Sample script</span></span>

<span data-ttu-id="0b22e-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.sh "Быстрое создание виртуальной машины")]</span><span class="sxs-lookup"><span data-stu-id="0b22e-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="0b22e-108">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="0b22e-108">Clean up deployment</span></span> 

<span data-ttu-id="0b22e-109">Выполните следующую команду, чтобы удалить группу ресурсов, виртуальную машину и все связанные с ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="0b22e-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="0b22e-110">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="0b22e-110">Script explanation</span></span>

<span data-ttu-id="0b22e-111">Для создания группы ресурсов, виртуальной машины, группы доступности, балансировщика нагрузки и всех связанных ресурсов этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="0b22e-111">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="0b22e-112">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="0b22e-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="0b22e-113">Команда</span><span class="sxs-lookup"><span data-stu-id="0b22e-113">Command</span></span> | <span data-ttu-id="0b22e-114">Примечания</span><span class="sxs-lookup"><span data-stu-id="0b22e-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0b22e-115">az group create</span><span class="sxs-lookup"><span data-stu-id="0b22e-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="0b22e-116">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="0b22e-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0b22e-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="0b22e-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="0b22e-118">Создает виртуальную сеть и подсеть Azure.</span><span class="sxs-lookup"><span data-stu-id="0b22e-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="0b22e-119">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="0b22e-119">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="0b22e-120">Создает общедоступный IP-адрес со статическим IP-адресом и связанным DNS-именем.</span><span class="sxs-lookup"><span data-stu-id="0b22e-120">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="0b22e-121">az network lb create</span><span class="sxs-lookup"><span data-stu-id="0b22e-121">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#create) | <span data-ttu-id="0b22e-122">Создает балансировщик сетевой нагрузки Azure.</span><span class="sxs-lookup"><span data-stu-id="0b22e-122">Creates an Azure Network Load Balancer (NLB).</span></span> |
| [<span data-ttu-id="0b22e-123">az network lb probe create</span><span class="sxs-lookup"><span data-stu-id="0b22e-123">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | <span data-ttu-id="0b22e-124">Создает пробу балансировщика сетевой нагрузки.</span><span class="sxs-lookup"><span data-stu-id="0b22e-124">Creates an NLB probe.</span></span> <span data-ttu-id="0b22e-125">Она используется для отслеживания каждой виртуальной машины в наборе балансировщика сетевой нагрузки.</span><span class="sxs-lookup"><span data-stu-id="0b22e-125">An NLB probe is used to monitor each VM in the NLB set.</span></span> <span data-ttu-id="0b22e-126">Если любая виртуальная машина становится недоступной, к ней не направляется трафик.</span><span class="sxs-lookup"><span data-stu-id="0b22e-126">If any VM becomes inaccessible, traffic is not routed to the VM.</span></span> |
| [<span data-ttu-id="0b22e-127">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="0b22e-127">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="0b22e-128">Создает правило балансировщика сетевой нагрузки.</span><span class="sxs-lookup"><span data-stu-id="0b22e-128">Creates an NLB rule.</span></span> <span data-ttu-id="0b22e-129">В этом примере создается правило для порта 80.</span><span class="sxs-lookup"><span data-stu-id="0b22e-129">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="0b22e-130">Так как трафик HTTP поступает в балансировщик сетевой нагрузки, он перенаправляется на порт 80 одной из виртуальных машин в наборе балансировщика сетевой нагрузки.</span><span class="sxs-lookup"><span data-stu-id="0b22e-130">As HTTP traffic arrives at the NLB, it is routed to port 80 one of the VMs in the NLB set.</span></span> |
| [<span data-ttu-id="0b22e-131">az network lb inbound-nat-rule create</span><span class="sxs-lookup"><span data-stu-id="0b22e-131">az network lb inbound-nat-rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) | <span data-ttu-id="0b22e-132">Создает правило преобразования сетевых адресов (NAT) балансировщика сетевой нагрузки.</span><span class="sxs-lookup"><span data-stu-id="0b22e-132">Creates an NLB Network Address Translation (NAT) rule.</span></span>  <span data-ttu-id="0b22e-133">Правила NAT сопоставляют порт балансировщика сетевой нагрузки с портом виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0b22e-133">NAT rules map a port of the NLB to a port on a VM.</span></span> <span data-ttu-id="0b22e-134">В этом примере создается правило NAT для SSH-трафика на каждой виртуальной машине в наборе балансировщика сетевой нагрузки.</span><span class="sxs-lookup"><span data-stu-id="0b22e-134">In this sample, a NAT rule is created for SSH traffic to each VM in the NLB set.</span></span>  |
| [<span data-ttu-id="0b22e-135">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="0b22e-135">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="0b22e-136">Создает группу безопасности сети (NSG), которая выполняет роль периметра безопасности между Интернетом и виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="0b22e-136">Creates a network security group (NSG), which is a security boundary between the internet and the virtual machine.</span></span> |
| [<span data-ttu-id="0b22e-137">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="0b22e-137">az network nsg rule create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="0b22e-138">Создает правило NSG, разрешающее входящий трафик.</span><span class="sxs-lookup"><span data-stu-id="0b22e-138">Creates an NSG rule to allow inbound traffic.</span></span> <span data-ttu-id="0b22e-139">В этом примере открывается порт 22 для трафика SSH.</span><span class="sxs-lookup"><span data-stu-id="0b22e-139">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="0b22e-140">az network nic create</span><span class="sxs-lookup"><span data-stu-id="0b22e-140">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="0b22e-141">Создает виртуальную сетевую карту и подключает ее к виртуальной сети, подсети и группе безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="0b22e-141">Creates a virtual network card and attaches it to the virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="0b22e-142">az vm availability-set create</span><span class="sxs-lookup"><span data-stu-id="0b22e-142">az vm availability-set create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="0b22e-143">Создает группу доступности.</span><span class="sxs-lookup"><span data-stu-id="0b22e-143">Creates an availability set.</span></span> <span data-ttu-id="0b22e-144">Группы доступности обеспечивают непрерывную работу приложения, распределяя виртуальные машины по физическим ресурсам. Таким образом, в случае сбоя он не затронет весь набор ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0b22e-144">Availability sets ensure application uptime by spreading the virtual machines across physical resources such that if failure occurs, the entire set is not effected.</span></span> |
| [<span data-ttu-id="0b22e-145">az vm create</span><span class="sxs-lookup"><span data-stu-id="0b22e-145">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="0b22e-146">Создает виртуальную машину и подключает ее к сетевой карте, виртуальной сети, подсети и группе безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="0b22e-146">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="0b22e-147">Эта команда также указывает образ виртуальной машины, который будет использоваться, и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="0b22e-147">This command also specifies the virtual machine image to be used and administrative credentials.</span></span>  |
| [<span data-ttu-id="0b22e-148">az group delete</span><span class="sxs-lookup"><span data-stu-id="0b22e-148">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="0b22e-149">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="0b22e-149">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0b22e-150">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0b22e-150">Next steps</span></span>

<span data-ttu-id="0b22e-151">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0b22e-151">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="0b22e-152">Дополнительные примеры скриптов интерфейса командной строки для виртуальных машин см. в [документации по виртуальным машинам Azure под управлением Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0b22e-152">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
