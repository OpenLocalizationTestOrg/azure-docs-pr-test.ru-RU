---
title: "Образец скрипта CLI - aaaAzure распределяет нагрузку между несколькими веб-сайтов с hello Azure CLI | Документы Microsoft"
description: "Пример сценария Azure CLI - распределяет нагрузку между несколькими toohello веб-сайтов одной виртуальной машине"
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
ms.openlocfilehash: 136da5d1783fb9f9dc87f1ffad8eec7b95c6bd7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-multiple-websites"></a><span data-ttu-id="093ac-103">Балансировка нагрузки на нескольких веб-сайтах</span><span class="sxs-lookup"><span data-stu-id="093ac-103">Load balance multiple websites</span></span>

<span data-ttu-id="093ac-104">Этот пример сценария создает виртуальную сеть с двумя виртуальными машинами, которые входят в группу доступности.</span><span class="sxs-lookup"><span data-stu-id="093ac-104">This script sample creates a virtual network with two virtual machines (VM) that are members of an availability set.</span></span> <span data-ttu-id="093ac-105">Балансировщик нагрузки направляет трафик для двух разных IP-адреса toohello двух виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="093ac-105">A load balancer directs traffic for two separate IP addresses toohello two VMs.</span></span> <span data-ttu-id="093ac-106">После выполнения скрипта hello можно развернуть web server программного обеспечения toohello виртуальных машин и размещать несколько веб-сайтов, каждая из которых свой IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="093ac-106">After running hello script, you could deploy web server software toohello VMs and host multiple web sites, each with its own IP address.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="093ac-107">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="093ac-107">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.sh  "Load balance multiple web sites")]

## <a name="clean-up-deployment"></a><span data-ttu-id="093ac-108">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="093ac-108">Clean up deployment</span></span> 

<span data-ttu-id="093ac-109">Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="093ac-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="093ac-110">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="093ac-110">Script explanation</span></span>

<span data-ttu-id="093ac-111">Этот скрипт использует hello, следующие команды toocreate группу ресурсов виртуальной сети, подсистема балансировки нагрузки и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="093ac-111">This script uses hello following commands toocreate a resource group, virtual network, load balancer, and all related resources.</span></span> <span data-ttu-id="093ac-112">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="093ac-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="093ac-113">Команда</span><span class="sxs-lookup"><span data-stu-id="093ac-113">Command</span></span> | <span data-ttu-id="093ac-114">Примечания</span><span class="sxs-lookup"><span data-stu-id="093ac-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="093ac-115">az group create</span><span class="sxs-lookup"><span data-stu-id="093ac-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="093ac-116">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="093ac-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="093ac-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="093ac-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="093ac-118">Создает виртуальную сеть и подсеть Azure.</span><span class="sxs-lookup"><span data-stu-id="093ac-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="093ac-119">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="093ac-119">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="093ac-120">Создает общедоступный IP-адрес со статическим IP-адресом и связанным DNS-именем.</span><span class="sxs-lookup"><span data-stu-id="093ac-120">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="093ac-121">az network lb create</span><span class="sxs-lookup"><span data-stu-id="093ac-121">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#create) | <span data-ttu-id="093ac-122">Создает службу Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="093ac-122">Creates an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="093ac-123">az network lb probe create</span><span class="sxs-lookup"><span data-stu-id="093ac-123">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | <span data-ttu-id="093ac-124">Создает зонд подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="093ac-124">Creates a load balancer probe.</span></span> <span data-ttu-id="093ac-125">Зонд подсистемы балансировки нагрузки является используется toomonitor каждой виртуальной Машины в наборе балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="093ac-125">A load balancer probe is used toomonitor each VM in hello load balancer set.</span></span> <span data-ttu-id="093ac-126">Если все виртуальные Машины, становится недоступной, трафик не перенаправленное toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="093ac-126">If any VM becomes inaccessible, traffic is not routed toohello VM.</span></span> |
| [<span data-ttu-id="093ac-127">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="093ac-127">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="093ac-128">Создает правило подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="093ac-128">Creates a load balancer rule.</span></span> <span data-ttu-id="093ac-129">В этом примере создается правило для порта 80.</span><span class="sxs-lookup"><span data-stu-id="093ac-129">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="093ac-130">HTTP-трафик поступает на hello балансировки нагрузки, это перенаправленное tooport 80 один из виртуальных машин hello в набор балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="093ac-130">As HTTP traffic arrives at hello load balancer, it is routed tooport 80 one of hello VMs in hello load balancer set.</span></span> |
| [<span data-ttu-id="093ac-131">az network lb frontend-ip create</span><span class="sxs-lookup"><span data-stu-id="093ac-131">az network lb frontend-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) | <span data-ttu-id="093ac-132">Создайте интерфейсный IP-адрес для hello подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="093ac-132">Create a frontend IP address for hello Load Balancer.</span></span> |
| [<span data-ttu-id="093ac-133">az network lb address-pool create</span><span class="sxs-lookup"><span data-stu-id="093ac-133">az network lb address-pool create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) | <span data-ttu-id="093ac-134">Создает внутренний пул адресов.</span><span class="sxs-lookup"><span data-stu-id="093ac-134">Creates a backend address pool.</span></span> |
| [<span data-ttu-id="093ac-135">az network nic create</span><span class="sxs-lookup"><span data-stu-id="093ac-135">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="093ac-136">Создает виртуальный сетевой адаптер и присоединяет его toohello виртуальной сети и подсети.</span><span class="sxs-lookup"><span data-stu-id="093ac-136">Creates a virtual network card and attaches it toohello virtual network, and subnet.</span></span> |
| [<span data-ttu-id="093ac-137">az vm availability-set create</span><span class="sxs-lookup"><span data-stu-id="093ac-137">az vm availability-set create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="093ac-138">Создает группу доступности.</span><span class="sxs-lookup"><span data-stu-id="093ac-138">Creates an availability set.</span></span> <span data-ttu-id="093ac-139">Наборы доступности обеспечения бесперебойной работы приложения, распределяя hello виртуальных машин между физическими ресурсами, таким образом, что в случае сбоя всего набора hello не влияют.</span><span class="sxs-lookup"><span data-stu-id="093ac-139">Availability sets ensure application uptime by spreading hello virtual machines across physical resources such that if failure occurs, hello entire set is not effected.</span></span> |
| [<span data-ttu-id="093ac-140">az network nic ip-config create</span><span class="sxs-lookup"><span data-stu-id="093ac-140">az network nic ip-config create</span></span>](https://docs.microsoft.com/cli/azure/network/nic/ip-config#create) | <span data-ttu-id="093ac-141">Создает IP-конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="093ac-141">Creates an IP confiuration.</span></span> <span data-ttu-id="093ac-142">Необходимо иметь возможность Microsoft.Network/AllowMultipleIpConfigurationsPerNic hello включена для вашей подписки.</span><span class="sxs-lookup"><span data-stu-id="093ac-142">You must have hello Microsoft.Network/AllowMultipleIpConfigurationsPerNic feature enabled for your subscription.</span></span> <span data-ttu-id="093ac-143">Только одна конфигурация может быть определен как hello основной IP-конфигурации каждого сетевого Адаптера, с помощью hello--флаг сделать основным.</span><span class="sxs-lookup"><span data-stu-id="093ac-143">Only one configuration may be designated as hello primary IP configuration per NIC, using hello --make-primary flag.</span></span> |
| [<span data-ttu-id="093ac-144">az vm create</span><span class="sxs-lookup"><span data-stu-id="093ac-144">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="093ac-145">Создает виртуальную машину hello и подключает его toohello сетевой карты, виртуальной сети, подсети и NSG.</span><span class="sxs-lookup"><span data-stu-id="093ac-145">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="093ac-146">Эта команда также указывает hello toobe образа на виртуальной машине используется и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="093ac-146">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="093ac-147">az group delete</span><span class="sxs-lookup"><span data-stu-id="093ac-147">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="093ac-148">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="093ac-148">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="093ac-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="093ac-149">Next steps</span></span>

<span data-ttu-id="093ac-150">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="093ac-150">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="093ac-151">Дополнительные сетевые образцы сценариев CLI можно найти в hello [документации Azure Общие сведения о сети](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="093ac-151">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
