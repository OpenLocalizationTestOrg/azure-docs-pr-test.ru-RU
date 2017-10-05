---
title: "Пример сценария Azure CLI. Балансировка нагрузки на нескольких веб-сайтах с помощью Azure CLI | Документация Майкрософт"
description: "Пример сценария Azure CLI для балансировки нагрузки нескольких веб-сайтов на одной виртуальной машине."
services: load-balancer
documentationcenter: load-balancer
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: c5a584b33025122033b930822ae0a0864a7ec1cb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="load-balance-multiple-websites"></a><span data-ttu-id="2dd5b-103">Балансировка нагрузки на нескольких веб-сайтах</span><span class="sxs-lookup"><span data-stu-id="2dd5b-103">Load balance multiple websites</span></span>

<span data-ttu-id="2dd5b-104">Этот пример сценария создает виртуальную сеть с двумя виртуальными машинами, которые входят в группу доступности.</span><span class="sxs-lookup"><span data-stu-id="2dd5b-104">This script sample creates a virtual network with two virtual machines (VM) that are members of an availability set.</span></span> <span data-ttu-id="2dd5b-105">Подсистема балансировки нагрузки направляет трафик с двух отдельных IP-адресов на две виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="2dd5b-105">A load balancer directs traffic for two separate IP addresses to the two VMs.</span></span> <span data-ttu-id="2dd5b-106">После выполнения сценария можно развернуть ПО веб-сервера на виртуальных машин и разместить несколько веб-сайтов, каждый из которых имеет собственный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="2dd5b-106">After running the script, you could deploy web server software to the VMs and host multiple web sites, each with its own IP address.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="2dd5b-107">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="2dd5b-107">Sample script</span></span>


<span data-ttu-id="2dd5b-108">[!code-azurecli-interactive[main](../../../cli_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.sh  "Балансировка нагрузки на нескольких веб-сайтах")]</span><span class="sxs-lookup"><span data-stu-id="2dd5b-108">[!code-azurecli-interactive[main](../../../cli_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.sh  "Load balance multiple web sites")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="2dd5b-109">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="2dd5b-109">Clean up deployment</span></span> 

<span data-ttu-id="2dd5b-110">Выполните следующую команду, чтобы удалить группу ресурсов, виртуальную машину и все связанные с ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="2dd5b-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="2dd5b-111">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="2dd5b-111">Script explanation</span></span>

<span data-ttu-id="2dd5b-112">Для создания группы ресурсов, виртуальной сети, подсистемы балансировки нагрузки и всех связанных ресурсов этот сценарий использует приведенные ниже команды.</span><span class="sxs-lookup"><span data-stu-id="2dd5b-112">This script uses the following commands to create a resource group, virtual network, load balancer, and all related resources.</span></span> <span data-ttu-id="2dd5b-113">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="2dd5b-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="2dd5b-114">Команда</span><span class="sxs-lookup"><span data-stu-id="2dd5b-114">Command</span></span> | <span data-ttu-id="2dd5b-115">Примечания</span><span class="sxs-lookup"><span data-stu-id="2dd5b-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2dd5b-116">az group create</span><span class="sxs-lookup"><span data-stu-id="2dd5b-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="2dd5b-117">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="2dd5b-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2dd5b-118">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="2dd5b-118">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="2dd5b-119">Создает виртуальную сеть и подсеть Azure.</span><span class="sxs-lookup"><span data-stu-id="2dd5b-119">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="2dd5b-120">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="2dd5b-120">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="2dd5b-121">Создает общедоступный IP-адрес со статическим IP-адресом и связанным DNS-именем.</span><span class="sxs-lookup"><span data-stu-id="2dd5b-121">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="2dd5b-122">az network lb create</span><span class="sxs-lookup"><span data-stu-id="2dd5b-122">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#create) | <span data-ttu-id="2dd5b-123">Создает службу Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="2dd5b-123">Creates an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="2dd5b-124">az network lb probe create</span><span class="sxs-lookup"><span data-stu-id="2dd5b-124">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | <span data-ttu-id="2dd5b-125">Создает зонд подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="2dd5b-125">Creates a load balancer probe.</span></span> <span data-ttu-id="2dd5b-126">Зонд подсистемы балансировки нагрузки используется для мониторинга каждой виртуальной машины в наборе подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="2dd5b-126">A load balancer probe is used to monitor each VM in the load balancer set.</span></span> <span data-ttu-id="2dd5b-127">Если любая виртуальная машина становится недоступной, к ней не направляется трафик.</span><span class="sxs-lookup"><span data-stu-id="2dd5b-127">If any VM becomes inaccessible, traffic is not routed to the VM.</span></span> |
| [<span data-ttu-id="2dd5b-128">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="2dd5b-128">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="2dd5b-129">Создает правило подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="2dd5b-129">Creates a load balancer rule.</span></span> <span data-ttu-id="2dd5b-130">В этом примере создается правило для порта 80.</span><span class="sxs-lookup"><span data-stu-id="2dd5b-130">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="2dd5b-131">Так как трафик HTTP поступает в подсистему балансировки нагрузки, он перенаправляется на порт 80 одной из виртуальных машин в наборе подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="2dd5b-131">As HTTP traffic arrives at the load balancer, it is routed to port 80 one of the VMs in the load balancer set.</span></span> |
| [<span data-ttu-id="2dd5b-132">az network lb frontend-ip create</span><span class="sxs-lookup"><span data-stu-id="2dd5b-132">az network lb frontend-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) | <span data-ttu-id="2dd5b-133">Создает интерфейсный IP-адрес для подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="2dd5b-133">Create a frontend IP address for the Load Balancer.</span></span> |
| [<span data-ttu-id="2dd5b-134">az network lb address-pool create</span><span class="sxs-lookup"><span data-stu-id="2dd5b-134">az network lb address-pool create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) | <span data-ttu-id="2dd5b-135">Создает внутренний пул адресов.</span><span class="sxs-lookup"><span data-stu-id="2dd5b-135">Creates a backend address pool.</span></span> |
| [<span data-ttu-id="2dd5b-136">az network nic create</span><span class="sxs-lookup"><span data-stu-id="2dd5b-136">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="2dd5b-137">Создает виртуальную сетевую карту и подключает ее к виртуальной сети и подсети.</span><span class="sxs-lookup"><span data-stu-id="2dd5b-137">Creates a virtual network card and attaches it to the virtual network, and subnet.</span></span> |
| [<span data-ttu-id="2dd5b-138">az vm availability-set create</span><span class="sxs-lookup"><span data-stu-id="2dd5b-138">az vm availability-set create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="2dd5b-139">Создает группу доступности.</span><span class="sxs-lookup"><span data-stu-id="2dd5b-139">Creates an availability set.</span></span> <span data-ttu-id="2dd5b-140">Группы доступности обеспечивают непрерывную работу приложения, распределяя виртуальные машины по физическим ресурсам. Таким образом, в случае сбоя он не затронет весь набор ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2dd5b-140">Availability sets ensure application uptime by spreading the virtual machines across physical resources such that if failure occurs, the entire set is not effected.</span></span> |
| [<span data-ttu-id="2dd5b-141">az network nic ip-config create</span><span class="sxs-lookup"><span data-stu-id="2dd5b-141">az network nic ip-config create</span></span>](https://docs.microsoft.com/cli/azure/network/nic/ip-config#create) | <span data-ttu-id="2dd5b-142">Создает IP-конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="2dd5b-142">Creates an IP confiuration.</span></span> <span data-ttu-id="2dd5b-143">Для подписки должна быть включена функция Microsoft.Network/AllowMultipleIpConfigurationsPerNic.</span><span class="sxs-lookup"><span data-stu-id="2dd5b-143">You must have the Microsoft.Network/AllowMultipleIpConfigurationsPerNic feature enabled for your subscription.</span></span> <span data-ttu-id="2dd5b-144">В качестве основной IP-конфигурации каждой сетевой карте можно назначить только одну конфигурацию. Для этого используется флаг --make-primary.</span><span class="sxs-lookup"><span data-stu-id="2dd5b-144">Only one configuration may be designated as the primary IP configuration per NIC, using the --make-primary flag.</span></span> |
| [<span data-ttu-id="2dd5b-145">az vm create</span><span class="sxs-lookup"><span data-stu-id="2dd5b-145">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="2dd5b-146">Создает виртуальную машину и подключает ее к сетевой карте, виртуальной сети, подсети и группе безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="2dd5b-146">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="2dd5b-147">Эта команда также указывает образ виртуальной машины, который будет использоваться, и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="2dd5b-147">This command also specifies the virtual machine image to be used and administrative credentials.</span></span>  |
| [<span data-ttu-id="2dd5b-148">az group delete</span><span class="sxs-lookup"><span data-stu-id="2dd5b-148">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="2dd5b-149">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="2dd5b-149">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2dd5b-150">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2dd5b-150">Next steps</span></span>

<span data-ttu-id="2dd5b-151">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2dd5b-151">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2dd5b-152">Дополнительные примеры сценариев Azure CLI для сетей см. в статье [Примеры Azure CLI](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2dd5b-152">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
