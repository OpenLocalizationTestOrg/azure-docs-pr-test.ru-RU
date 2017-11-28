---
title: "Пример сценария CLI - tooVMs трафика балансировки нагрузки для обеспечения высокой доступности aaaAzure | Документы Microsoft"
description: "Пример сценария Azure CLI - tooVMs трафика балансировки нагрузки для обеспечения высокой доступности"
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
ms.openlocfilehash: 0954b5c261512724dfb9c6e7be123c9d45624f4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-traffic-toovms-for-high-availability"></a><span data-ttu-id="9f4ff-103">Загрузить tooVMs Балансировка трафика для обеспечения высокой доступности</span><span class="sxs-lookup"><span data-stu-id="9f4ff-103">Load balance traffic tooVMs for high availability</span></span>

<span data-ttu-id="9f4ff-104">В этом примере сценария создается все необходимое toorun несколько Ubuntu виртуальных машин, настроенных в высокой доступности и загрузить сбалансированной конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9f4ff-104">This script sample creates everything needed toorun several Ubuntu virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="9f4ff-105">После выполнения скрипта hello, будет иметь три виртуальные машины присоединены к домену tooan группе доступности Azure и доступный с помощью подсистемы балансировки нагрузки Azure.</span><span class="sxs-lookup"><span data-stu-id="9f4ff-105">After running hello script, you will have three virtual machines, joined tooan Azure Availability Set, and accessible through an Azure Load Balancer.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9f4ff-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="9f4ff-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="9f4ff-107">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="9f4ff-107">Clean up deployment</span></span> 

<span data-ttu-id="9f4ff-108">Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="9f4ff-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="9f4ff-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="9f4ff-109">Script explanation</span></span>

<span data-ttu-id="9f4ff-110">Этот скрипт использует hello следующие команды toocreate группы ресурсов, виртуальная машина, группа доступности, балансировки нагрузки и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="9f4ff-110">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="9f4ff-111">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="9f4ff-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9f4ff-112">Команда</span><span class="sxs-lookup"><span data-stu-id="9f4ff-112">Command</span></span> | <span data-ttu-id="9f4ff-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="9f4ff-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9f4ff-114">az group create</span><span class="sxs-lookup"><span data-stu-id="9f4ff-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="9f4ff-115">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="9f4ff-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9f4ff-116">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="9f4ff-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="9f4ff-117">Создает виртуальную сеть и подсеть Azure.</span><span class="sxs-lookup"><span data-stu-id="9f4ff-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="9f4ff-118">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="9f4ff-118">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="9f4ff-119">Создает общедоступный IP-адрес со статическим IP-адресом и связанным DNS-именем.</span><span class="sxs-lookup"><span data-stu-id="9f4ff-119">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="9f4ff-120">az network lb create</span><span class="sxs-lookup"><span data-stu-id="9f4ff-120">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#create) | <span data-ttu-id="9f4ff-121">Создает службу Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="9f4ff-121">Creates an Azure load balancer.</span></span> |
| [<span data-ttu-id="9f4ff-122">az network lb probe create</span><span class="sxs-lookup"><span data-stu-id="9f4ff-122">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | <span data-ttu-id="9f4ff-123">Создает зонд подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="9f4ff-123">Creates a load balancer probe.</span></span> <span data-ttu-id="9f4ff-124">Зонд подсистемы балансировки нагрузки является используется toomonitor каждой виртуальной Машины в наборе балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="9f4ff-124">A load balancer probe is used toomonitor each VM in hello load balancer set.</span></span> <span data-ttu-id="9f4ff-125">Если все виртуальные Машины, становится недоступной, трафик не перенаправленное toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="9f4ff-125">If any VM becomes inaccessible, traffic is not routed toohello VM.</span></span> |
| [<span data-ttu-id="9f4ff-126">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="9f4ff-126">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="9f4ff-127">Создает правило подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="9f4ff-127">Creates a load balancer rule.</span></span> <span data-ttu-id="9f4ff-128">В этом примере создается правило для порта 80.</span><span class="sxs-lookup"><span data-stu-id="9f4ff-128">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="9f4ff-129">HTTP-трафик поступает на hello балансировки нагрузки, это перенаправленное tooport 80 один из виртуальных машин hello в наборе hello балансировки Нагрузки.</span><span class="sxs-lookup"><span data-stu-id="9f4ff-129">As HTTP traffic arrives at hello load balancer, it is routed tooport 80 one of hello VMs in hello LB set.</span></span> |
| [<span data-ttu-id="9f4ff-130">az network lb inbound-nat-rule create</span><span class="sxs-lookup"><span data-stu-id="9f4ff-130">az network lb inbound-nat-rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) | <span data-ttu-id="9f4ff-131">Создает правило преобразования сетевых адресов (NAT) подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="9f4ff-131">Creates load balancer Network Address Translation (NAT) rule.</span></span>  <span data-ttu-id="9f4ff-132">Правила преобразования сетевых адресов сопоставление порта порта tooa подсистемы балансировки нагрузки hello на виртуальной Машине.</span><span class="sxs-lookup"><span data-stu-id="9f4ff-132">NAT rules map a port of hello load balancer tooa port on a VM.</span></span> <span data-ttu-id="9f4ff-133">В этом образце правило NAT создается для SSH tooeach трафик виртуальной Машины в наборе балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="9f4ff-133">In this sample, a NAT rule is created for SSH traffic tooeach VM in hello load balancer set.</span></span>  |
| [<span data-ttu-id="9f4ff-134">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="9f4ff-134">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="9f4ff-135">Создание группы безопасности сети (NSG), который является границей безопасности между виртуальными машинами hello Интернет» и «hello.</span><span class="sxs-lookup"><span data-stu-id="9f4ff-135">Creates a network security group (NSG), which is a security boundary between hello internet and hello virtual machine.</span></span> |
| [<span data-ttu-id="9f4ff-136">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="9f4ff-136">az network nsg rule create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="9f4ff-137">Создает правило NSG tooallow входящий трафик.</span><span class="sxs-lookup"><span data-stu-id="9f4ff-137">Creates an NSG rule tooallow inbound traffic.</span></span> <span data-ttu-id="9f4ff-138">В этом примере открывается порт 22 для трафика SSH.</span><span class="sxs-lookup"><span data-stu-id="9f4ff-138">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="9f4ff-139">az network nic create</span><span class="sxs-lookup"><span data-stu-id="9f4ff-139">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="9f4ff-140">Создает виртуальный сетевой адаптер и присоединяет его toohello виртуальной сети, подсети и NSG.</span><span class="sxs-lookup"><span data-stu-id="9f4ff-140">Creates a virtual network card and attaches it toohello virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="9f4ff-141">az vm availability-set create</span><span class="sxs-lookup"><span data-stu-id="9f4ff-141">az vm availability-set create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="9f4ff-142">Создает группу доступности.</span><span class="sxs-lookup"><span data-stu-id="9f4ff-142">Creates an availability set.</span></span> <span data-ttu-id="9f4ff-143">Наборы доступности обеспечения бесперебойной работы приложения, распределяя hello виртуальных машин между физическими ресурсами, таким образом, что в случае сбоя всего набора hello не влияют.</span><span class="sxs-lookup"><span data-stu-id="9f4ff-143">Availability sets ensure application uptime by spreading hello virtual machines across physical resources such that if failure occurs, hello entire set is not effected.</span></span> |
| [<span data-ttu-id="9f4ff-144">az vm create</span><span class="sxs-lookup"><span data-stu-id="9f4ff-144">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="9f4ff-145">Создает виртуальную машину hello и подключает его toohello сетевой карты, виртуальной сети, подсети и NSG.</span><span class="sxs-lookup"><span data-stu-id="9f4ff-145">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="9f4ff-146">Эта команда также указывает hello toobe образа на виртуальной машине используется и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="9f4ff-146">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="9f4ff-147">az group delete</span><span class="sxs-lookup"><span data-stu-id="9f4ff-147">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="9f4ff-148">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="9f4ff-148">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9f4ff-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9f4ff-149">Next steps</span></span>

<span data-ttu-id="9f4ff-150">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9f4ff-150">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9f4ff-151">Дополнительные образцы сценариев CLI сети Azure можно найти в hello [сеть Azure документации](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9f4ff-151">Additional Azure Networking CLI script samples can be found in hello [Azure Networking documentation](../cli-samples.md).</span></span>
