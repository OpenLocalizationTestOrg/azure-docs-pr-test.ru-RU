---
title: "aaaCreate полную среду Linux с hello Azure CLI 1.0 | Документы Microsoft"
description: "Создайте хранилища, виртуальной Машины Linux, виртуальной сети и подсети, подсистемы балансировки нагрузки, сетевой Адаптер, общедоступный IP-адрес и группу безопасности сети из hello основание, с помощью hello Azure CLI 1.0."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ba4060b-ce95-4747-a735-1d7c68597a1a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 7fe00e138704fe9c9a1c9b87a7dd1afd6174e527
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-environment-with-hello-azure-cli-10"></a><span data-ttu-id="e5178-103">Создайте полную среду Linux с hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="e5178-103">Create a complete Linux environment with hello Azure CLI 1.0</span></span>
<span data-ttu-id="e5178-104">В этой статье мы создаем простую сеть с балансировщиком нагрузки и парой виртуальных машин, подходящих для разработки и простых вычислений.</span><span class="sxs-lookup"><span data-stu-id="e5178-104">In this article, we build a simple network with a load balancer and a pair of VMs that are useful for development and simple computing.</span></span> <span data-ttu-id="e5178-105">Мы будем рассматривать процесса hello, команда, пока не получится два рабочий защитить toowhich виртуальных машин Linux, которым можно подключаться из в любом месте на hello Интернет.</span><span class="sxs-lookup"><span data-stu-id="e5178-105">We walk through hello process command by command, until you have two working, secure Linux VMs toowhich you can connect from anywhere on hello Internet.</span></span> <span data-ttu-id="e5178-106">Затем можно переместить на toomore сложная топология сетей и сред.</span><span class="sxs-lookup"><span data-stu-id="e5178-106">Then you can move on toomore complex networks and environments.</span></span>

<span data-ttu-id="e5178-107">Вдоль hello образом вы узнаете о hello зависимостей иерархии дает hello модели развертывания диспетчера ресурсов, что о сведения о количестве энергии предоставляет.</span><span class="sxs-lookup"><span data-stu-id="e5178-107">Along hello way, you learn about hello dependency hierarchy that hello Resource Manager deployment model gives you, and about how much power it provides.</span></span> <span data-ttu-id="e5178-108">После появления построение hello системы можно перестроить его гораздо быстрее с помощью [шаблоны Azure Resource Manager](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e5178-108">After you see how hello system is built, you can rebuild it much more quickly by using [Azure Resource Manager templates](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="e5178-109">Кроме того после вы узнаете, как взаимодействуют hello части среды, создание шаблонов tooautomate их становится проще.</span><span class="sxs-lookup"><span data-stu-id="e5178-109">Also, after you learn how hello parts of your environment fit together, creating templates tooautomate them becomes easier.</span></span>

<span data-ttu-id="e5178-110">Среда Hello содержит:</span><span class="sxs-lookup"><span data-stu-id="e5178-110">hello environment contains:</span></span>

* <span data-ttu-id="e5178-111">две виртуальные машины в группе доступности;</span><span class="sxs-lookup"><span data-stu-id="e5178-111">Two VMs inside an availability set.</span></span>
* <span data-ttu-id="e5178-112">балансировщик нагрузки с правилом балансировки нагрузки для порта 80;</span><span class="sxs-lookup"><span data-stu-id="e5178-112">A load balancer with a load-balancing rule on port 80.</span></span>
* <span data-ttu-id="e5178-113">Группы безопасности сети (NSG) правила tooprotect ВМ от нежелательного трафика.</span><span class="sxs-lookup"><span data-stu-id="e5178-113">Network security group (NSG) rules tooprotect your VM from unwanted traffic.</span></span>

<span data-ttu-id="e5178-114">toocreate этой пользовательской среды необходимо hello последней [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) в режим диспетчера ресурсов (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="e5178-114">toocreate this custom environment, you need hello latest [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) in Resource Manager mode (`azure config mode arm`).</span></span> <span data-ttu-id="e5178-115">Кроме того, потребуется инструмент анализа JSON.</span><span class="sxs-lookup"><span data-stu-id="e5178-115">You also need a JSON parsing tool.</span></span> <span data-ttu-id="e5178-116">В этом примере используются [jq](https://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="e5178-116">This example uses [jq](https://stedolan.github.io/jq/).</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="e5178-117">Задача hello toocomplete версии CLI</span><span class="sxs-lookup"><span data-stu-id="e5178-117">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="e5178-118">Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.</span><span class="sxs-lookup"><span data-stu-id="e5178-118">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="e5178-119">[Azure CLI 1.0](#quick-commands) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)</span><span class="sxs-lookup"><span data-stu-id="e5178-119">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="e5178-120">[Azure CLI 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -нашей нового поколения CLI для модели развертывания hello ресурсов управления</span><span class="sxs-lookup"><span data-stu-id="e5178-120">[Azure CLI 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="e5178-121">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="e5178-121">Quick commands</span></span>
<span data-ttu-id="e5178-122">При необходимости tooquickly выполнения задачи hello, hello следующий раздел сведения hello базовые команды tooupload tooAzure виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="e5178-122">If you need tooquickly accomplish hello task, hello following section details hello base commands tooupload a VM tooAzure.</span></span> <span data-ttu-id="e5178-123">Более подробные сведения и контекста, для каждого шага можно найти в hello остальной части документа hello, начиная [здесь](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="e5178-123">More detailed information and context for each step can be found in hello rest of hello document, starting [here](#detailed-walkthrough).</span></span>

<span data-ttu-id="e5178-124">Убедитесь, что [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) входа в систему и использование режима диспетчера ресурсов:</span><span class="sxs-lookup"><span data-stu-id="e5178-124">Make sure that you have [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="e5178-125">В hello следующих примерах замените примеры имен параметров собственные значения.</span><span class="sxs-lookup"><span data-stu-id="e5178-125">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="e5178-126">Используемые имена параметров: `myResourceGroup`, `mystorageaccount` и `myVM`.</span><span class="sxs-lookup"><span data-stu-id="e5178-126">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

<span data-ttu-id="e5178-127">Создайте группу ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="e5178-127">Create hello resource group.</span></span> <span data-ttu-id="e5178-128">Hello следующий пример создает группу ресурсов с именем `myResourceGroup` в hello `westeurope` расположение:</span><span class="sxs-lookup"><span data-stu-id="e5178-128">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` location:</span></span>

```azurecli
azure group create -n myResourceGroup -l westeurope
```

<span data-ttu-id="e5178-129">Проверьте hello группы ресурсов с помощью средства синтаксического анализа JSON hello:</span><span class="sxs-lookup"><span data-stu-id="e5178-129">Verify hello resource group by using hello JSON parser:</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="e5178-130">Создайте учетную запись хранения hello.</span><span class="sxs-lookup"><span data-stu-id="e5178-130">Create hello storage account.</span></span> <span data-ttu-id="e5178-131">Hello следующий пример создает учетную запись хранения с именем `mystorageaccount`.</span><span class="sxs-lookup"><span data-stu-id="e5178-131">hello following example creates a storage account named `mystorageaccount`.</span></span> <span data-ttu-id="e5178-132">(имя учетной записи хранения hello должно быть уникальным, поэтому ввести уникальное имя).</span><span class="sxs-lookup"><span data-stu-id="e5178-132">(hello storage account name must be unique, so provide your own unique name.)</span></span>

```azurecli
azure storage account create -g myResourceGroup -l westeurope \
  --kind Storage --sku-name GRS mystorageaccount
```

<span data-ttu-id="e5178-133">Проверьте hello учетной записи хранилища с помощью средства синтаксического анализа JSON hello:</span><span class="sxs-lookup"><span data-stu-id="e5178-133">Verify hello storage account by using hello JSON parser:</span></span>

```azurecli
azure storage account show -g myResourceGroup mystorageaccount --json | jq '.'
```

<span data-ttu-id="e5178-134">Создайте виртуальную сеть hello.</span><span class="sxs-lookup"><span data-stu-id="e5178-134">Create hello virtual network.</span></span> <span data-ttu-id="e5178-135">Hello следующий пример создает виртуальную сеть с именем `myVnet`:</span><span class="sxs-lookup"><span data-stu-id="e5178-135">hello following example creates a virtual network named `myVnet`:</span></span>

```azurecli
azure network vnet create -g myResourceGroup -l westeurope\
  -n myVnet -a 192.168.0.0/16
```

<span data-ttu-id="e5178-136">Создайте подсеть.</span><span class="sxs-lookup"><span data-stu-id="e5178-136">Create a subnet.</span></span> <span data-ttu-id="e5178-137">Hello следующий пример создает подсеть с именем `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="e5178-137">hello following example creates a subnet named `mySubnet`:</span></span>

```azurecli
azure network vnet subnet create -g myResourceGroup \
  -e myVnet -n mySubnet -a 192.168.1.0/24
```

<span data-ttu-id="e5178-138">Проверьте hello виртуальной сети и подсети с помощью средства синтаксического анализа JSON hello:</span><span class="sxs-lookup"><span data-stu-id="e5178-138">Verify hello virtual network and subnet by using hello JSON parser:</span></span>

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

<span data-ttu-id="e5178-139">Создайте общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="e5178-139">Create a public IP.</span></span> <span data-ttu-id="e5178-140">Hello следующий пример создает общедоступный IP-адрес с именем `myPublicIP` с именем DNS hello `mypublicdns`.</span><span class="sxs-lookup"><span data-stu-id="e5178-140">hello following example creates a public IP named `myPublicIP` with hello DNS name of `mypublicdns`.</span></span> <span data-ttu-id="e5178-141">(hello DNS-имя должно быть уникальным, поэтому ввести уникальное имя).</span><span class="sxs-lookup"><span data-stu-id="e5178-141">(hello DNS name must be unique, so provide your own unique name.)</span></span>

```azurecli
azure network public-ip create -g myResourceGroup -l westeurope \
  -n myPublicIP  -d mypublicdns -a static -i 4
```

<span data-ttu-id="e5178-142">Создайте hello подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e5178-142">Create hello load balancer.</span></span> <span data-ttu-id="e5178-143">Hello следующий пример создает подсистемы балансировки нагрузки с именем `myLoadBalancer`:</span><span class="sxs-lookup"><span data-stu-id="e5178-143">hello following example creates a load balancer named `myLoadBalancer`:</span></span>

```azurecli
azure network lb create -g myResourceGroup -l westeurope -n myLoadBalancer
```

<span data-ttu-id="e5178-144">Создать пул IP переднего плана для подсистемы балансировки нагрузки hello и свяжите hello общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="e5178-144">Create a front-end IP pool for hello load balancer, and associate hello public IP.</span></span> <span data-ttu-id="e5178-145">Hello следующий пример создает интерфейсный IP пул с именем `mySubnetPool`:</span><span class="sxs-lookup"><span data-stu-id="e5178-145">hello following example creates a front-end IP pool named `mySubnetPool`:</span></span>

```azurecli
azure network lb frontend-ip create -g myResourceGroup -l myLoadBalancer \
  -i myPublicIP -n myFrontEndPool
```

<span data-ttu-id="e5178-146">Создайте пул IP-hello внутренней подсистемы балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="e5178-146">Create hello back-end IP pool for hello load balancer.</span></span> <span data-ttu-id="e5178-147">Hello следующем примере создается пул IP серверной части, с именем `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="e5178-147">hello following example creates a back-end IP pool named `myBackEndPool`:</span></span>

```azurecli
azure network lb address-pool create -g myResourceGroup -l myLoadBalancer \
  -n myBackEndPool
```

<span data-ttu-id="e5178-148">Создание правила преобразования адресов (NAT) для балансировки нагрузки hello входящего сетевого SSH.</span><span class="sxs-lookup"><span data-stu-id="e5178-148">Create SSH inbound network address translation (NAT) rules for hello load balancer.</span></span> <span data-ttu-id="e5178-149">Hello следующий пример создает два правила подсистемы балансировки нагрузки, `myLoadBalancerRuleSSH1` и `myLoadBalancerRuleSSH2`:</span><span class="sxs-lookup"><span data-stu-id="e5178-149">hello following example creates two load balancer rules, `myLoadBalancerRuleSSH1` and `myLoadBalancerRuleSSH2`:</span></span>

```azurecli
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH1 -p tcp -f 4222 -b 22
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH2 -p tcp -f 4223 -b 22
```

<span data-ttu-id="e5178-150">Создание веб-hello входящих правил NAT для hello подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e5178-150">Create hello web inbound NAT rules for hello load balancer.</span></span> <span data-ttu-id="e5178-151">Hello следующий пример создает правила подсистемы балансировки нагрузки с именем `myLoadBalancerRuleWeb`:</span><span class="sxs-lookup"><span data-stu-id="e5178-151">hello following example creates a load balancer rule named `myLoadBalancerRuleWeb`:</span></span>

```azurecli
azure network lb rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleWeb -p tcp -f 80 -b 80 \
  -t myFrontEndPool -o myBackEndPool
```

<span data-ttu-id="e5178-152">Создайте зонда работоспособности подсистемы балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="e5178-152">Create hello load balancer health probe.</span></span> <span data-ttu-id="e5178-153">Hello следующий пример создает TCP Проба с именем `myHealthProbe`:</span><span class="sxs-lookup"><span data-stu-id="e5178-153">hello following example creates a TCP probe named `myHealthProbe`:</span></span>

```azurecli
azure network lb probe create -g myResourceGroup -l myLoadBalancer \
  -n myHealthProbe -p "tcp" -i 15 -c 4
```

<span data-ttu-id="e5178-154">Проверьте hello балансировки нагрузки, пулы IP-адресов и правила NAT с помощью средства синтаксического анализа JSON hello:</span><span class="sxs-lookup"><span data-stu-id="e5178-154">Verify hello load balancer, IP pools, and NAT rules by using hello JSON parser:</span></span>

```azurecli
azure network lb show -g myResourceGroup -n myLoadBalancer --json | jq '.'
```

<span data-ttu-id="e5178-155">Создайте hello первый сетевой адаптер (NIC).</span><span class="sxs-lookup"><span data-stu-id="e5178-155">Create hello first network interface card (NIC).</span></span> <span data-ttu-id="e5178-156">Замените hello `#####-###-###` секции с идентификатором подписки Azure</span><span class="sxs-lookup"><span data-stu-id="e5178-156">Replace hello `#####-###-###` sections with your own Azure subscription ID.</span></span> <span data-ttu-id="e5178-157">Идентификатор, указывается в выходные данные hello подписки **jq** при исследовании hello ресурсов, вы создаете.</span><span class="sxs-lookup"><span data-stu-id="e5178-157">Your subscription ID is noted in hello output of **jq** when you examine hello resources you are creating.</span></span> <span data-ttu-id="e5178-158">Кроме того, его можно просмотреть, выполнив команду `azure account list`.</span><span class="sxs-lookup"><span data-stu-id="e5178-158">You can also view your subscription ID with `azure account list`.</span></span>

<span data-ttu-id="e5178-159">Hello следующий пример создает сетевой Адаптер с именем `myNic1`:</span><span class="sxs-lookup"><span data-stu-id="e5178-159">hello following example creates a NIC named `myNic1`:</span></span>

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic1 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
```

<span data-ttu-id="e5178-160">Создание hello второй сетевой адаптер.</span><span class="sxs-lookup"><span data-stu-id="e5178-160">Create hello second NIC.</span></span> <span data-ttu-id="e5178-161">Hello следующий пример создает сетевой Адаптер с именем `myNic2`:</span><span class="sxs-lookup"><span data-stu-id="e5178-161">hello following example creates a NIC named `myNic2`:</span></span>

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic2 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
```

<span data-ttu-id="e5178-162">Проверьте hello двух сетевых адаптеров с помощью средства синтаксического анализа JSON hello:</span><span class="sxs-lookup"><span data-stu-id="e5178-162">Verify hello two NICs by using hello JSON parser:</span></span>

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
azure network nic show myResourceGroup myNic2 --json | jq '.'
```

<span data-ttu-id="e5178-163">Создание группы безопасности сети hello.</span><span class="sxs-lookup"><span data-stu-id="e5178-163">Create hello network security group.</span></span> <span data-ttu-id="e5178-164">Hello следующий пример создает группу безопасности сети с именем `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="e5178-164">hello following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network nsg create -g myResourceGroup -l westeurope \
  -n myNetworkSecurityGroup
```

<span data-ttu-id="e5178-165">Добавьте два правила для входящих подключений для hello сетевой группы безопасности.</span><span class="sxs-lookup"><span data-stu-id="e5178-165">Add two inbound rules for hello network security group.</span></span> <span data-ttu-id="e5178-166">Hello в примере создаются два правила, `myNetworkSecurityGroupRuleSSH` и `myNetworkSecurityGroupRuleHTTP`:</span><span class="sxs-lookup"><span data-stu-id="e5178-166">hello following example creates two rules, `myNetworkSecurityGroupRuleSSH` and `myNetworkSecurityGroupRuleHTTP`:</span></span>

```azurecli
azure network nsg rule create -p tcp -r inbound -y 1000 -u 22 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleSSH
azure network nsg rule create -p tcp -r inbound -y 1001 -u 80 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleHTTP
```

<span data-ttu-id="e5178-167">Проверьте группы безопасности сети hello и правила для входящих подключений с помощью средства синтаксического анализа JSON hello:</span><span class="sxs-lookup"><span data-stu-id="e5178-167">Verify hello network security group and inbound rules by using hello JSON parser:</span></span>

```azurecli
azure network nsg show -g myResourceGroup -n myNetworkSecurityGroup --json | jq '.'
```

<span data-ttu-id="e5178-168">Привязать hello сетевой безопасности группы toohello двух сетевых адаптеров:</span><span class="sxs-lookup"><span data-stu-id="e5178-168">Bind hello network security group toohello two NICs:</span></span>

```azurecli
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic1
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic2
```

<span data-ttu-id="e5178-169">Создайте набор доступности hello.</span><span class="sxs-lookup"><span data-stu-id="e5178-169">Create hello availability set.</span></span> <span data-ttu-id="e5178-170">Hello следующий пример создает именованный набор доступности `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="e5178-170">hello following example creates an availability set named `myAvailabilitySet`:</span></span>

```azurecli
azure availset create -g myResourceGroup -l westeurope -n myAvailabilitySet
```

<span data-ttu-id="e5178-171">Создание hello первая виртуальная машина Linux.</span><span class="sxs-lookup"><span data-stu-id="e5178-171">Create hello first Linux VM.</span></span> <span data-ttu-id="e5178-172">Hello следующий пример создает Виртуальную машину с именем `myVM1`:</span><span class="sxs-lookup"><span data-stu-id="e5178-172">hello following example creates a VM named `myVM1`:</span></span>

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM1 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic1 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

<span data-ttu-id="e5178-173">Создать hello второй виртуальной Машины с Linux.</span><span class="sxs-lookup"><span data-stu-id="e5178-173">Create hello second Linux VM.</span></span> <span data-ttu-id="e5178-174">Hello следующий пример создает Виртуальную машину с именем `myVM2`:</span><span class="sxs-lookup"><span data-stu-id="e5178-174">hello following example creates a VM named `myVM2`:</span></span>

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM2 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic2 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

<span data-ttu-id="e5178-175">Используйте tooverify средство синтаксического анализа JSON hello, что было создано все:</span><span class="sxs-lookup"><span data-stu-id="e5178-175">Use hello JSON parser tooverify that everything that was built:</span></span>

```azurecli
azure vm show -g myResourceGroup -n myVM1 --json | jq '.'
azure vm show -g myResourceGroup -n myVM2 --json | jq '.'
```

<span data-ttu-id="e5178-176">Экспорт вашей новой среды tooa шаблона tooquickly повторного создания новых экземпляров.</span><span class="sxs-lookup"><span data-stu-id="e5178-176">Export your new environment tooa template tooquickly re-create new instances:</span></span>

```azurecli
azure group export myResourceGroup
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="e5178-177">Подробное пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="e5178-177">Detailed walkthrough</span></span>
<span data-ttu-id="e5178-178">Hello подробные инструкции, следующие за объяснить действия каждой команды при построении масштабирование среды.</span><span class="sxs-lookup"><span data-stu-id="e5178-178">hello detailed steps that follow explain what each command is doing as you build out your environment.</span></span> <span data-ttu-id="e5178-179">Эти понятия помогут вам при создании пользовательских сред для разработки или эксплуатации.</span><span class="sxs-lookup"><span data-stu-id="e5178-179">These concepts are helpful when you build your own custom environments for development or production.</span></span>

<span data-ttu-id="e5178-180">Убедитесь, что [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) входа в систему и использование режима диспетчера ресурсов:</span><span class="sxs-lookup"><span data-stu-id="e5178-180">Make sure that you have [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="e5178-181">В hello следующих примерах замените примеры имен параметров собственные значения.</span><span class="sxs-lookup"><span data-stu-id="e5178-181">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="e5178-182">Используемые имена параметров: `myResourceGroup`, `mystorageaccount` и `myVM`.</span><span class="sxs-lookup"><span data-stu-id="e5178-182">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

## <a name="create-resource-groups-and-choose-deployment-locations"></a><span data-ttu-id="e5178-183">Создание групп ресурсов и выбор расположений развертывания</span><span class="sxs-lookup"><span data-stu-id="e5178-183">Create resource groups and choose deployment locations</span></span>
<span data-ttu-id="e5178-184">Группы ресурсов Azure — Логическое развертывание сущности, которые содержат конфигурации сведения метаданных tooenable hello логического управления и развертывания ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e5178-184">Azure resource groups are logical deployment entities that contain configuration information and metadata tooenable hello logical management of resource deployments.</span></span> <span data-ttu-id="e5178-185">Hello следующий пример создает группу ресурсов с именем `myResourceGroup` в hello `westeurope` расположение:</span><span class="sxs-lookup"><span data-stu-id="e5178-185">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` location:</span></span>

```azurecli
azure group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="e5178-186">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e5178-186">Output:</span></span>

```azurecli                        
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westeurope
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

## <a name="create-a-storage-account"></a><span data-ttu-id="e5178-187">Создайте учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="e5178-187">Create a storage account</span></span>
<span data-ttu-id="e5178-188">Необходимые учетные записи хранения для дисков виртуальной Машины, а также для любых дополнительных дисков данных, которые должны tooadd.</span><span class="sxs-lookup"><span data-stu-id="e5178-188">You need storage accounts for your VM disks and for any additional data disks that you want tooadd.</span></span> <span data-ttu-id="e5178-189">Учетные записи хранения создаются практически сразу после создания групп ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e5178-189">You create storage accounts almost immediately after you create resource groups.</span></span>

<span data-ttu-id="e5178-190">Здесь мы используем hello `azure storage account create` команды, передав hello расположение учетной записи hello, hello группы ресурсов, которая управляет и hello тип поддержки хранения данных необходимо.</span><span class="sxs-lookup"><span data-stu-id="e5178-190">Here we use hello `azure storage account create` command, passing hello location of hello account, hello resource group that controls it, and hello type of storage support you want.</span></span> <span data-ttu-id="e5178-191">Hello следующий пример создает учетную запись хранения с именем `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="e5178-191">hello following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
azure storage account create \  
  --location westeurope \
  --resource-group myResourceGroup \
  --kind Storage --sku-name GRS \
  mystorageaccount
```

<span data-ttu-id="e5178-192">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e5178-192">Output:</span></span>

```azurecli
info:    Executing command storage account create
+ Creating storage account
info:    storage account create command OK
```

<span data-ttu-id="e5178-193">ресурс группы с помощью hello tooexamine `azure group show` команды, воспользуемся hello [jq](https://stedolan.github.io/jq/) инструментов вместе с hello `--json` параметр Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e5178-193">tooexamine our resource group by using hello `azure group show` command, let's use hello [jq](https://stedolan.github.io/jq/) tool along with hello `--json` Azure CLI option.</span></span> <span data-ttu-id="e5178-194">(Можно использовать **jsawk** или любую библиотеку языка вы предпочитаете tooparse hello JSON.)</span><span class="sxs-lookup"><span data-stu-id="e5178-194">(You can use **jsawk** or any language library you prefer tooparse hello JSON.)</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="e5178-195">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e5178-195">Output:</span></span>

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

<span data-ttu-id="e5178-196">tooinvestigate hello учетной записи хранилища с помощью hello CLI, необходимо сначала имена учетных записей tooset hello и ключи.</span><span class="sxs-lookup"><span data-stu-id="e5178-196">tooinvestigate hello storage account by using hello CLI, you first need tooset hello account names and keys.</span></span> <span data-ttu-id="e5178-197">Замените имя hello hello учетной записи хранения в следующий пример с именем выбранного hello:</span><span class="sxs-lookup"><span data-stu-id="e5178-197">Replace hello name of hello storage account in hello following example with a name that you choose:</span></span>

```bash
export AZURE_STORAGE_CONNECTION_STRING="$(azure storage account connectionstring show mystorageaccount --resource-group myResourceGroup --json | jq -r '.string')"
```

<span data-ttu-id="e5178-198">Это позволит с легкостью просматривать сведения о хранилище.</span><span class="sxs-lookup"><span data-stu-id="e5178-198">Then you can view your storage information easily:</span></span>

```azurecli
azure storage container list
```

<span data-ttu-id="e5178-199">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e5178-199">Output:</span></span>

```azurecli
info:    Executing command storage container list
+ Getting storage containers
data:    Name  Public-Access  Last-Modified
data:    ----  -------------  -----------------------------
data:    vhds  Off            Sun, 27 Sep 2015 19:03:54 GMT
info:    storage container list command OK
```

## <a name="create-a-virtual-network-and-subnet"></a><span data-ttu-id="e5178-200">Создание виртуальной сети и подсети</span><span class="sxs-lookup"><span data-stu-id="e5178-200">Create a virtual network and subnet</span></span>
<span data-ttu-id="e5178-201">Теперь ты tooneed toocreate виртуальная сеть в Azure и подсеть, в котором можно создавать виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="e5178-201">Next you're going tooneed toocreate a virtual network running in Azure and a subnet in which you can create your VMs.</span></span> <span data-ttu-id="e5178-202">Hello следующий пример создает виртуальную сеть с именем `myVnet` с hello `192.168.0.0/16` префикс адреса:</span><span class="sxs-lookup"><span data-stu-id="e5178-202">hello following example creates a virtual network named `myVnet` with hello `192.168.0.0/16` address prefix:</span></span>

```azurecli
azure network vnet create --resource-group myResourceGroup --location westeurope \
  --name myVnet --address-prefixes 192.168.0.0/16
```

<span data-ttu-id="e5178-203">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e5178-203">Output:</span></span>

```azurecli
info:    Executing command network vnet create
+ Looking up virtual network "myVnet"
+ Creating virtual network "myVnet"
+ Loading virtual network state
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet
data:    Name                            : myVnet
data:    Type                            : Microsoft.Network/virtualNetworks
data:    Location                        : westeurope
data:    ProvisioningState               : Succeeded
data:    Address prefixes:
data:      192.168.0.0/16
info:    network vnet create command OK
```

<span data-ttu-id="e5178-204">Опять же, давайте используйте параметр--json hello `azure group show` и `jq` toosee как мы создаем ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e5178-204">Again, let's use hello --json option of `azure group show` and `jq` toosee how we're building our resources.</span></span> <span data-ttu-id="e5178-205">Теперь у нас есть ресурс `storageAccounts` и ресурс `virtualNetworks`.</span><span class="sxs-lookup"><span data-stu-id="e5178-205">We now have a `storageAccounts` resource and a `virtualNetworks` resource.</span></span>  

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="e5178-206">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e5178-206">Output:</span></span>

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
      "name": "myVnet",
      "type": "virtualNetworks",
      "location": "westeurope",
      "tags": null
    },
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

<span data-ttu-id="e5178-207">Теперь давайте создадим подсети в hello `myVnet` виртуальной сети, в которой hello развернутых виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e5178-207">Now let's create a subnet in hello `myVnet` virtual network into which hello VMs are deployed.</span></span> <span data-ttu-id="e5178-208">Мы используем hello `azure network vnet subnet create` команду вместе с ресурсами hello, мы уже создали: hello `myResourceGroup` группы ресурсов и hello `myVnet` виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="e5178-208">We use hello `azure network vnet subnet create` command, along with hello resources we've already created: hello `myResourceGroup` resource group and hello `myVnet` virtual network.</span></span> <span data-ttu-id="e5178-209">В следующем примере hello, мы добавляем hello подсеть с именем `mySubnet` с префикс подсети адреса hello `192.168.1.0/24`:</span><span class="sxs-lookup"><span data-stu-id="e5178-209">In hello following example, we add hello subnet named `mySubnet` with hello subnet address prefix of `192.168.1.0/24`:</span></span>

```azurecli
azure network vnet subnet create --resource-group myResourceGroup \
  --vnet-name myVnet --name mySubnet --address-prefix 192.168.1.0/24
```

<span data-ttu-id="e5178-210">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e5178-210">Output:</span></span>

```azurecli
info:    Executing command network vnet subnet create
+ Looking up hello subnet "mySubnet"
+ Creating subnet "mySubnet"
+ Looking up hello subnet "mySubnet"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:    Type                            : Microsoft.Network/virtualNetworks/subnets
data:    ProvisioningState               : Succeeded
data:    Name                            : mySubnet
data:    Address prefix                  : 192.168.1.0/24
data:
info:    network vnet subnet create command OK
```

<span data-ttu-id="e5178-211">Так как подсеть hello логически находится внутри виртуальной сети hello, мы просмотрите сведения о подсети hello с немного другой командой.</span><span class="sxs-lookup"><span data-stu-id="e5178-211">Because hello subnet is logically inside hello virtual network, we look for hello subnet information with a slightly different command.</span></span> <span data-ttu-id="e5178-212">Команда Hello, мы используем `azure network vnet show`, но мы продолжим выходных данных JSON hello tooexamine с помощью `jq`.</span><span class="sxs-lookup"><span data-stu-id="e5178-212">hello command we use is `azure network vnet show`, but we continue tooexamine hello JSON output by using `jq`.</span></span>

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

<span data-ttu-id="e5178-213">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e5178-213">Output:</span></span>

```json
{
  "subnets": [
    {
      "ipConfigurations": [],
      "addressPrefix": "192.168.1.0/24",
      "provisioningState": "Succeeded",
      "name": "mySubnet",
      "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
    }
  ],
  "tags": {},
  "addressSpace": {
    "addressPrefixes": [
      "192.168.0.0/16"
    ]
  },
  "dhcpOptions": {
    "dnsServers": []
  },
  "provisioningState": "Succeeded",
  "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
  "name": "myVnet",
  "location": "westeurope"
}
```

## <a name="create-a-public-ip-address"></a><span data-ttu-id="e5178-214">Создание общедоступного IP-адреса</span><span class="sxs-lookup"><span data-stu-id="e5178-214">Create a public IP address</span></span>
<span data-ttu-id="e5178-215">Теперь давайте создадим hello общедоступный IP-адрес (PIP), будут назначены tooyour подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e5178-215">Now let's create hello public IP address (PIP) that we assign tooyour load balancer.</span></span> <span data-ttu-id="e5178-216">Благодаря этому можно tooyour tooconnect виртуальных машин из hello Интернета с помощью hello `azure network public-ip create` команды.</span><span class="sxs-lookup"><span data-stu-id="e5178-216">It enables you tooconnect tooyour VMs from hello Internet by using hello `azure network public-ip create` command.</span></span> <span data-ttu-id="e5178-217">Так как адрес по умолчанию hello является динамическим, мы создадим именованную запись DNS в hello **cloudapp.azure.com** домена с помощью hello `--domain-name-label` параметр.</span><span class="sxs-lookup"><span data-stu-id="e5178-217">Because hello default address is dynamic, we create a named DNS entry in hello **cloudapp.azure.com** domain by using hello `--domain-name-label` option.</span></span> <span data-ttu-id="e5178-218">Hello следующий пример создает общедоступный IP-адрес с именем `myPublicIP` с именем DNS hello `mypublicdns`.</span><span class="sxs-lookup"><span data-stu-id="e5178-218">hello following example creates a public IP named `myPublicIP` with hello DNS name of `mypublicdns`.</span></span> <span data-ttu-id="e5178-219">Поскольку hello DNS-имя должно быть уникальным, вы предоставляете собственное уникальное имя DNS:</span><span class="sxs-lookup"><span data-stu-id="e5178-219">Because hello DNS name must be unique, you provide your own unique DNS name:</span></span>

```azurecli
azure network public-ip create --resource-group myResourceGroup \
  --location westeurope --name myPublicIP --domain-name-label mypublicdns
```

<span data-ttu-id="e5178-220">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e5178-220">Output:</span></span>

```azurecli
info:    Executing command network public-ip create
+ Looking up hello public ip "myPublicIP"
+ Creating public ip address "myPublicIP"
+ Looking up hello public ip "myPublicIP"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
data:    Name                            : myPublicIP
data:    Type                            : Microsoft.Network/publicIPAddresses
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Allocation method               : Dynamic
data:    Idle timeout                    : 4
data:    Domain name label               : mypublicdns
data:    FQDN                            : mypublicdns.westeurope.cloudapp.azure.com
info:    network public-ip create command OK
```

<span data-ttu-id="e5178-221">Hello общедоступный IP-адрес является также верхнего уровня, чтобы можно было видеть его с `azure group show`.</span><span class="sxs-lookup"><span data-stu-id="e5178-221">hello public IP address is also a top-level resource, so you can see it with `azure group show`.</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="e5178-222">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e5178-222">Output:</span></span>

```json
{
"tags": {},
"id": "/subscriptions/guid/resourceGroups/myResourceGroup",
"name": "myResourceGroup",
"provisioningState": "Succeeded",
"location": "westeurope",
"properties": {
    "provisioningState": "Succeeded"
},
"resources": [
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
    "name": "myPublicIP",
    "type": "publicIPAddresses",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
    "name": "myVnet",
    "type": "virtualNetworks",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
    "name": "mystorageaccount",
    "type": "storageAccounts",
    "location": "westeurope",
    "tags": null
    }
],
"permissions": [
    {
    "actions": [
        "*"
    ],
    "notActions": []
    }
]
}
```

<span data-ttu-id="e5178-223">Можно выяснить, Дополнительные сведения о ресурсов, включая hello полное доменное имя (FQDN) подобласти hello с помощью hello полный `azure network public-ip show` команды.</span><span class="sxs-lookup"><span data-stu-id="e5178-223">You can investigate more resource details, including hello fully qualified domain name (FQDN) of hello subdomain, by using hello complete `azure network public-ip show` command.</span></span> <span data-ttu-id="e5178-224">логически выделил Hello открытого ресурса IP-адреса, но определенный адрес еще не были назначены.</span><span class="sxs-lookup"><span data-stu-id="e5178-224">hello public IP address resource has been allocated logically, but a specific address has not yet been assigned.</span></span> <span data-ttu-id="e5178-225">tooobtain IP-адрес, ты tooneed балансировки нагрузки, который мы еще не создана.</span><span class="sxs-lookup"><span data-stu-id="e5178-225">tooobtain an IP address, you're going tooneed a load balancer, which we have not yet created.</span></span>

```azurecli
azure network public-ip show myResourceGroup myPublicIP --json | jq '.'
```

<span data-ttu-id="e5178-226">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e5178-226">Output:</span></span>

```json
{
"tags": {},
"publicIpAllocationMethod": "Dynamic",
"dnsSettings": {
    "domainNameLabel": "mypublicdns",
    "fqdn": "mypublicdns.westeurope.cloudapp.azure.com"
},
"idleTimeoutInMinutes": 4,
"provisioningState": "Succeeded",
"etag": "W/\"c63154b3-1130-49b9-a887-877d74d5ebc5\"",
"id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
"name": "myPublicIP",
"location": "westeurope"
}
```

## <a name="create-a-load-balancer-and-ip-pools"></a><span data-ttu-id="e5178-227">Создание балансировщика нагрузки и пулов IP-адресов</span><span class="sxs-lookup"><span data-stu-id="e5178-227">Create a load balancer and IP pools</span></span>
<span data-ttu-id="e5178-228">При создании подсистемы балансировки нагрузки можно toodistribute трафика между несколькими виртуальными машинами.</span><span class="sxs-lookup"><span data-stu-id="e5178-228">When you create a load balancer, it enables you toodistribute traffic across multiple VMs.</span></span> <span data-ttu-id="e5178-229">Он также обеспечивает избыточность tooyour приложения, выполнив несколько виртуальных машин, которые отвечают toouser запросы в событии hello обслуживания или в больших нагрузках.</span><span class="sxs-lookup"><span data-stu-id="e5178-229">It also provides redundancy tooyour application by running multiple VMs that respond toouser requests in hello event of maintenance or heavy loads.</span></span> <span data-ttu-id="e5178-230">Hello следующий пример создает подсистемы балансировки нагрузки с именем `myLoadBalancer`:</span><span class="sxs-lookup"><span data-stu-id="e5178-230">hello following example creates a load balancer named `myLoadBalancer`:</span></span>

```azurecli
azure network lb create --resource-group myResourceGroup --location westeurope \
  --name myLoadBalancer
```

<span data-ttu-id="e5178-231">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e5178-231">Output:</span></span>

```azurecli
info:    Executing command network lb create
+ Looking up hello load balancer "myLoadBalancer"
+ Creating load balancer "myLoadBalancer"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer
data:    Name                            : myLoadBalancer
data:    Type                            : Microsoft.Network/loadBalancers
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
info:    network lb create command OK
```

<span data-ttu-id="e5178-232">Наш балансировщик нагрузки выглядит пустым, поэтому давайте создадим несколько пулов IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="e5178-232">Our load balancer is fairly empty, so let's create some IP pools.</span></span> <span data-ttu-id="e5178-233">Мы хотим пулы toocreate двух IP-адресов для наших балансировки нагрузки, для внешнего интерфейса hello и для серверной части hello.</span><span class="sxs-lookup"><span data-stu-id="e5178-233">We want toocreate two IP pools for our load balancer, one for hello front end and one for hello back end.</span></span> <span data-ttu-id="e5178-234">внешний пул IP-адресов Hello публично видимыми.</span><span class="sxs-lookup"><span data-stu-id="e5178-234">hello front-end IP pool is publicly visible.</span></span> <span data-ttu-id="e5178-235">Это также toowhich расположение hello, которые будут назначены hello PIP, которая была создана ранее.</span><span class="sxs-lookup"><span data-stu-id="e5178-235">It's also hello location toowhich we assign hello PIP that we created earlier.</span></span> <span data-ttu-id="e5178-236">Далее мы используем hello внутреннем пуле как расположение для наших tooconnect виртуальных машин для.</span><span class="sxs-lookup"><span data-stu-id="e5178-236">Then we use hello back-end pool as a location for our VMs tooconnect to.</span></span> <span data-ttu-id="e5178-237">Таким образом, hello трафик может проходить через toohello подсистемы балансировки нагрузки hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e5178-237">That way, hello traffic can flow through hello load balancer toohello VMs.</span></span>

<span data-ttu-id="e5178-238">Сначала создадим интерфейсный пул IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="e5178-238">First, let's create our front-end IP pool.</span></span> <span data-ttu-id="e5178-239">Hello следующий пример создает внешний пул с именем `myFrontEndPool`:</span><span class="sxs-lookup"><span data-stu-id="e5178-239">hello following example creates a front-end pool named `myFrontEndPool`:</span></span>

```azurecli
azure network lb frontend-ip create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --public-ip-name myPublicIP \
  --name myFrontEndPool
```

<span data-ttu-id="e5178-240">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e5178-240">Output:</span></span>

```azurecli
info:    Executing command network lb frontend-ip create
+ Looking up hello load balancer "myLoadBalancer"
+ Looking up hello public ip "myPublicIP"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myFrontEndPool
data:    Provisioning state              : Succeeded
data:    Private IP allocation method    : Dynamic
data:    Public IP address id            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
info:    network lb mySubnet-ip create command OK
```

<span data-ttu-id="e5178-241">Обратите внимание на то, как мы использовали hello `--public-ip-name` коммутатор toopass в hello `myPublicIP` , созданную ранее.</span><span class="sxs-lookup"><span data-stu-id="e5178-241">Note how we used hello `--public-ip-name` switch toopass in hello `myPublicIP` that we created earlier.</span></span> <span data-ttu-id="e5178-242">Назначение hello открытый IP-адрес подсистемы балансировки нагрузки toohello позволяет tooreach виртуальные машины по Интернету hello.</span><span class="sxs-lookup"><span data-stu-id="e5178-242">Assigning hello public IP address toohello load balancer allows you tooreach your VMs across hello Internet.</span></span>

<span data-ttu-id="e5178-243">Теперь создадим второй пул IP-адресов, на этот раз для внутреннего трафика.</span><span class="sxs-lookup"><span data-stu-id="e5178-243">Next, let's create our second IP pool, this time for our back-end traffic.</span></span> <span data-ttu-id="e5178-244">Hello следующий пример создает пул серверной части, с именем `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="e5178-244">hello following example creates a back-end pool named `myBackEndPool`:</span></span>

```azurecli
azure network lb address-pool create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myBackEndPool
```

<span data-ttu-id="e5178-245">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e5178-245">Output:</span></span>

```azurecli
info:    Executing command network lb address-pool create
+ Looking up hello load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myBackEndPool
data:    Provisioning state              : Succeeded
info:    network lb address-pool create command OK
```

<span data-ttu-id="e5178-246">Можно увидеть, насколько нашей подсистемы балансировки нагрузки путем поиска с `azure network lb show` и изучения выходных данных JSON hello:</span><span class="sxs-lookup"><span data-stu-id="e5178-246">We can see how our load balancer is doing by looking with `azure network lb show` and examining hello JSON output:</span></span>

```azurecli
azure network lb show myResourceGroup myLoadBalancer --json | jq '.'
```

<span data-ttu-id="e5178-247">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e5178-247">Output:</span></span>

```json
{
  "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [],
  "probes": []
}
```

## <a name="create-load-balancer-nat-rules"></a><span data-ttu-id="e5178-248">Создание правил NAT балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="e5178-248">Create load balancer NAT rules</span></span>
<span data-ttu-id="e5178-249">tooget трафик через наших балансировки нагрузки, нам нужно toocreate правила преобразования сетевых адресов (NAT), указать входящих или исходящих действия.</span><span class="sxs-lookup"><span data-stu-id="e5178-249">tooget traffic flowing through our load balancer, we need toocreate network address translation (NAT) rules that specify either inbound or outbound actions.</span></span> <span data-ttu-id="e5178-250">Можно указать протокол toouse hello, а затем сопоставление портов toointernal внешними портами в случае необходимости.</span><span class="sxs-lookup"><span data-stu-id="e5178-250">You can specify hello protocol toouse, then map external ports toointernal ports as desired.</span></span> <span data-ttu-id="e5178-251">В нашей среде давайте создадим некоторые правила, которые разрешают SSH через наших tooour подсистемы балансировки нагрузки виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e5178-251">For our environment, let's create some rules that allow SSH through our load balancer tooour VMs.</span></span> <span data-ttu-id="e5178-252">Мы устанавливаем tooTCP toodirect порты 4222 и 4223 TCP-порт 22 на нашем виртуальных машин (которые мы создаем более поздней версии).</span><span class="sxs-lookup"><span data-stu-id="e5178-252">We set up TCP ports 4222 and 4223 toodirect tooTCP port 22 on our VMs (which we create later).</span></span> <span data-ttu-id="e5178-253">Hello следующий код создает правило с именем `myLoadBalancerRuleSSH1` toomap TCP-порт 4222 tooport 22:</span><span class="sxs-lookup"><span data-stu-id="e5178-253">hello following example creates a rule named `myLoadBalancerRuleSSH1` toomap TCP port 4222 tooport 22:</span></span>

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH1 \
  --protocol tcp --frontend-port 4222 --backend-port 22
```

<span data-ttu-id="e5178-254">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e5178-254">Output:</span></span>

```azurecli
info:    Executing command network lb inbound-nat-rule create
+ Looking up hello load balancer "myLoadBalancer"
warn:    Using default enable floating ip: false
warn:    Using default idle timeout: 4
warn:    Using default mySubnet IP configuration "myFrontEndPool"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleSSH1
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 4222
data:    Backend port                    : 22
data:    Enable floating IP              : false
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
info:    network lb inbound-nat-rule create command OK
```

<span data-ttu-id="e5178-255">Повторите процедуру hello второго правила NAT для SSH.</span><span class="sxs-lookup"><span data-stu-id="e5178-255">Repeat hello procedure for your second NAT rule for SSH.</span></span> <span data-ttu-id="e5178-256">Hello следующий код создает правило с именем `myLoadBalancerRuleSSH2` toomap TCP-порт 4223 tooport 22:</span><span class="sxs-lookup"><span data-stu-id="e5178-256">hello following example creates a rule named `myLoadBalancerRuleSSH2` toomap TCP port 4223 tooport 22:</span></span>

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH2 --protocol tcp \
  --frontend-port 4223 --backend-port 22
```

<span data-ttu-id="e5178-257">Давайте также пойти дальше и создать правило NAT для TCP-порт 80 для веб-трафика, подключая пулы IP-адресов tooour правило hello.</span><span class="sxs-lookup"><span data-stu-id="e5178-257">Let's also go ahead and create a NAT rule for TCP port 80 for web traffic, hooking hello rule up tooour IP pools.</span></span> <span data-ttu-id="e5178-258">Если мы подключить tooan правило hello пула IP-вместо привязки tooour правило hello виртуальных машин по отдельности, мы можно добавить или удалить виртуальных машин из пула IP-hello.</span><span class="sxs-lookup"><span data-stu-id="e5178-258">If we hook up hello rule tooan IP pool, instead of hooking up hello rule tooour VMs individually, we can add or remove VMs from hello IP pool.</span></span> <span data-ttu-id="e5178-259">Подсистема балансировки нагрузки Hello автоматически корректируется hello поток трафика.</span><span class="sxs-lookup"><span data-stu-id="e5178-259">hello load balancer automatically adjusts hello flow of traffic.</span></span> <span data-ttu-id="e5178-260">Hello следующий код создает правило с именем `myLoadBalancerRuleWeb` toomap TCP-порт 80 tooport 80:</span><span class="sxs-lookup"><span data-stu-id="e5178-260">hello following example creates a rule named `myLoadBalancerRuleWeb` toomap TCP port 80 tooport 80:</span></span>

```azurecli
azure network lb rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleWeb --protocol tcp \
  --frontend-port 80 --backend-port 80 --frontend-ip-name myFrontEndPool \
  --backend-address-pool-name myBackEndPool
```

<span data-ttu-id="e5178-261">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e5178-261">Output:</span></span>

```azurecli
info:    Executing command network lb rule create
+ Looking up hello load balancer "myLoadBalancer"
warn:    Using default idle timeout: 4
warn:    Using default enable floating ip: false
warn:    Using default load distribution: Default
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleWeb
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 80
data:    Backend port                    : 80
data:    Enable floating IP              : false
data:    Load distribution               : Default
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
data:    Backend address pool id         : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
info:    network lb rule create command OK
```

## <a name="create-a-load-balancer-health-probe"></a><span data-ttu-id="e5178-262">Создание пробы работоспособности балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="e5178-262">Create a load balancer health probe</span></span>
<span data-ttu-id="e5178-263">Состояния проверки периодически проверок hello виртуальных машин, находящихся за нашей toomake подсистемы балансировки нагрузки, убедиться, что они операционной и отвечать на запросы toorequests, как определено.</span><span class="sxs-lookup"><span data-stu-id="e5178-263">A health probe periodically checks on hello VMs that are behind our load balancer toomake sure they're operating and responding toorequests as defined.</span></span> <span data-ttu-id="e5178-264">Если нет, они были удалены из tooensure операции, для которого пользователи не перенаправлен toothem.</span><span class="sxs-lookup"><span data-stu-id="e5178-264">If not, they're removed from operation tooensure that users aren't being directed toothem.</span></span> <span data-ttu-id="e5178-265">Можно определить пользовательские проверки для проверки работоспособности hello, вместе с интервалами и значения времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="e5178-265">You can define custom checks for hello health probe, along with intervals and timeout values.</span></span> <span data-ttu-id="e5178-266">Дополнительные сведения о пробах работоспособности см. в статье [Проверки балансировщика нагрузки](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e5178-266">For more information about health probes, see [Load Balancer probes](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="e5178-267">Hello следующий пример создает TCP работоспособности проверяется именованный `myHealthProbe`:</span><span class="sxs-lookup"><span data-stu-id="e5178-267">hello following example creates a TCP health probed named `myHealthProbe`:</span></span>

```azurecli
azure network lb probe create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myHealthProbe --protocol "tcp" \
  --interval 15 --count 4
```

<span data-ttu-id="e5178-268">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e5178-268">Output:</span></span>

```azurecli
info:    Executing command network lb probe create
warn:    Using default probe port: 80
+ Looking up hello load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myHealthProbe
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    Port                            : 80
data:    Interval in seconds             : 15
data:    Number of probes                : 4
info:    network lb probe create command OK
```

<span data-ttu-id="e5178-269">Здесь мы указали интервал в 15 секунд для проверок работоспособности.</span><span class="sxs-lookup"><span data-stu-id="e5178-269">Here, we specified an interval of 15 seconds for our health checks.</span></span> <span data-ttu-id="e5178-270">Мы может пропустить более четырех зондов (одна минута) подсистемы балансировки нагрузки hello считает, что перестал работать, на которых размещены hello.</span><span class="sxs-lookup"><span data-stu-id="e5178-270">We can miss a maximum of four probes (one minute) before hello load balancer considers that hello host is no longer functioning.</span></span>

## <a name="verify-hello-load-balancer"></a><span data-ttu-id="e5178-271">Проверьте hello балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="e5178-271">Verify hello load balancer</span></span>
<span data-ttu-id="e5178-272">Теперь делается hello конфигурации подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e5178-272">Now hello load balancer configuration is done.</span></span> <span data-ttu-id="e5178-273">Ниже приведены hello действия, предпринятые.</span><span class="sxs-lookup"><span data-stu-id="e5178-273">Here are hello steps you took:</span></span>

1. <span data-ttu-id="e5178-274">Вы создали балансировщик нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e5178-274">You created a load balancer.</span></span>
2. <span data-ttu-id="e5178-275">Созданы переднего плана пула IP и назначена открытый tooit IP.</span><span class="sxs-lookup"><span data-stu-id="e5178-275">You created a front-end IP pool and assigned a public IP tooit.</span></span>
3. <span data-ttu-id="e5178-276">Потом вы создали внутренний пул IP-адресов, к которому могут подключаться виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="e5178-276">You created a back-end IP pool that VMs can connect to.</span></span>
4. <span data-ttu-id="e5178-277">Вы создали правила NAT, которые разрешают ВМ toohello SSH для управления, а также правила, которое разрешает TCP-порт 80 для наших веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="e5178-277">You created NAT rules that allow SSH toohello VMs for management, along with a rule that allows TCP port 80 for our web app.</span></span>
5. <span data-ttu-id="e5178-278">Вы добавили работоспособности проверки tooperiodically проверки hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e5178-278">You added a health probe tooperiodically check hello VMs.</span></span> <span data-ttu-id="e5178-279">Эта проверка работоспособности гарантирует, что пользователи не предпринять tooaccess виртуальной Машины, которая больше не работает или передача содержимого.</span><span class="sxs-lookup"><span data-stu-id="e5178-279">This health probe ensures that users don't try tooaccess a VM that is no longer functioning or serving content.</span></span>

<span data-ttu-id="e5178-280">Давайте посмотрим, как теперь выглядит балансировщик нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e5178-280">Let's review what your load balancer looks like now:</span></span>

```azurecli
azure network lb show --resource-group myResourceGroup \
  --name myLoadBalancer --json | jq '.'
```

<span data-ttu-id="e5178-281">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e5178-281">Output:</span></span>

```json
{
  "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH1",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4222,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    },
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH2",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4223,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    }
  ],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "inboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        },
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleWeb",
      "provisioningState": "Succeeded",
      "enableFloatingIP": false,
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "backendAddressPool": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
      },
      "protocol": "Tcp",
      "loadDistribution": "Default",
      "mySubnetPort": 80,
      "backendPort": 80,
      "idleTimeoutInMinutes": 4
    }
  ],
  "probes": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myHealthProbe",
      "provisioningState": "Succeeded",
      "numberOfProbes": 4,
      "intervalInSeconds": 15,
      "port": 80,
      "protocol": "Tcp",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/probes/myHealthProbe"
    }
  ]
}
```

## <a name="create-an-nic-toouse-with-hello-linux-vm"></a><span data-ttu-id="e5178-282">Создать toouse сетевого Адаптера с hello ВМ Linux</span><span class="sxs-lookup"><span data-stu-id="e5178-282">Create an NIC toouse with hello Linux VM</span></span>
<span data-ttu-id="e5178-283">Сетевые адаптеры программно недоступны, так как можно применять правила использования tootheir.</span><span class="sxs-lookup"><span data-stu-id="e5178-283">NICs are programmatically available because you can apply rules tootheir use.</span></span> <span data-ttu-id="e5178-284">Кроме того, можно использовать несколько сетевых карт.</span><span class="sxs-lookup"><span data-stu-id="e5178-284">You can also have more than one.</span></span> <span data-ttu-id="e5178-285">В следующих hello `azure network nic create` команды подключить пула IP-адресов Сетевых toohello нагрузки внутренней hello и связать его с hello трафика SSH toopermit правило NAT.</span><span class="sxs-lookup"><span data-stu-id="e5178-285">In hello following `azure network nic create` command, you hook up hello NIC toohello load back-end IP pool and associate it with hello NAT rule toopermit SSH traffic.</span></span>

<span data-ttu-id="e5178-286">Замените hello `#####-###-###` секции с идентификатором подписки Azure</span><span class="sxs-lookup"><span data-stu-id="e5178-286">Replace hello `#####-###-###` sections with your own Azure subscription ID.</span></span> <span data-ttu-id="e5178-287">Идентификатор, указывается в выходные данные hello подписки `jq` при исследовании hello ресурсов, вы создаете.</span><span class="sxs-lookup"><span data-stu-id="e5178-287">Your subscription ID is noted in hello output of `jq` when you examine hello resources you are creating.</span></span> <span data-ttu-id="e5178-288">Кроме того, его можно просмотреть, выполнив команду `azure account list`.</span><span class="sxs-lookup"><span data-stu-id="e5178-288">You can also view your subscription ID with `azure account list`.</span></span>

<span data-ttu-id="e5178-289">Hello следующий пример создает сетевой Адаптер с именем `myNic1`:</span><span class="sxs-lookup"><span data-stu-id="e5178-289">hello following example creates a NIC named `myNic1`:</span></span>

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic1 \
  --lb-address-pool-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
```

<span data-ttu-id="e5178-290">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e5178-290">Output:</span></span>

```azurecli
info:    Executing command network nic create
+ Looking up hello subnet "mySubnet"
+ Looking up hello network interface "myNic1"
+ Creating network interface "myNic1"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1
data:    Name                            : myNic1
data:    Type                            : Microsoft.Network/networkInterfaces
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Enable IP forwarding            : false
data:    IP configurations:
data:      Name                          : Nic-IP-config
data:      Provisioning state            : Succeeded
data:      Private IP address            : 192.168.1.4
data:      Private IP allocation method  : Dynamic
data:      Subnet                        : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:      Load balancer backend address pools:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
data:      Load balancer inbound NAT rules:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
data:
info:    network nic create command OK
```

<span data-ttu-id="e5178-291">Hello сведений можно определить, проверив hello ресурсов напрямую.</span><span class="sxs-lookup"><span data-stu-id="e5178-291">You can see hello details by examining hello resource directly.</span></span> <span data-ttu-id="e5178-292">Просмотрите hello ресурсов с помощью hello `azure network nic show` команды:</span><span class="sxs-lookup"><span data-stu-id="e5178-292">You examine hello resource by using hello `azure network nic show` command:</span></span>

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
```

<span data-ttu-id="e5178-293">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e5178-293">Output:</span></span>

```json
{
  "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
  "provisioningState": "Succeeded",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1",
  "name": "myNic1",
  "type": "Microsoft.Network/networkInterfaces",
  "location": "westeurope",
  "ipConfigurations": [
    {
      "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1/ipConfigurations/Nic-IP-config",
      "loadBalancerBackendAddressPools": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
        }
      ],
      "loadBalancerInboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        }
      ],
      "privateIPAddress": "192.168.1.4",
      "privateIPAllocationMethod": "Dynamic",
      "subnet": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
      },
      "provisioningState": "Succeeded",
      "name": "Nic-IP-config"
    }
  ],
  "dnsSettings": {
    "appliedDnsServers": [],
    "dnsServers": []
  },
  "enableIPForwarding": false,
  "resourceGuid": "a20258b8-6361-45f6-b1b4-27ffed28798c"
}
```

<span data-ttu-id="e5178-294">Теперь мы создадим hello второй сетевой Адаптер, подключение в пул IP-адресов серверной части tooour еще раз.</span><span class="sxs-lookup"><span data-stu-id="e5178-294">Now we create hello second NIC, hooking in tooour back-end IP pool again.</span></span> <span data-ttu-id="e5178-295">Это правило время hello второй NAT разрешает трафик по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="e5178-295">This time hello second NAT rule permits SSH traffic.</span></span> <span data-ttu-id="e5178-296">Hello следующий пример создает сетевой Адаптер с именем `myNic2`:</span><span class="sxs-lookup"><span data-stu-id="e5178-296">hello following example creates a NIC named `myNic2`:</span></span>

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic2 \
  --lb-address-pool-ids  /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2
```

## <a name="create-a-network-security-group-and-rules"></a><span data-ttu-id="e5178-297">Создание группы безопасности сети и правил</span><span class="sxs-lookup"><span data-stu-id="e5178-297">Create a network security group and rules</span></span>
<span data-ttu-id="e5178-298">Теперь мы создайте группу безопасности сети и hello входящие правила, контролирующие доступ toohello сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="e5178-298">Now we create a network security group and hello inbound rules that govern access toohello NIC.</span></span> <span data-ttu-id="e5178-299">Группа безопасности сети может быть применен tooa сетевой Адаптер или подсети.</span><span class="sxs-lookup"><span data-stu-id="e5178-299">A network security group can be applied tooa NIC or subnet.</span></span> <span data-ttu-id="e5178-300">Определение правила toocontrol hello поток трафика и из него виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e5178-300">You define rules toocontrol hello flow of traffic in and out of your VMs.</span></span> <span data-ttu-id="e5178-301">Hello следующий пример создает группу безопасности сети с именем `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="e5178-301">hello following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network nsg create --resource-group myResourceGroup --location westeurope \
  --name myNetworkSecurityGroup
```

<span data-ttu-id="e5178-302">Давайте добавим hello входящее правило для hello NSG tooallow входящих подключений через порт 22 (toosupport SSH).</span><span class="sxs-lookup"><span data-stu-id="e5178-302">Let's add hello inbound rule for hello NSG tooallow inbound connections on port 22 (toosupport SSH).</span></span> <span data-ttu-id="e5178-303">Hello следующий код создает правило с именем `myNetworkSecurityGroupRuleSSH` tooallow TCP через порт 22:</span><span class="sxs-lookup"><span data-stu-id="e5178-303">hello following example creates a rule named `myNetworkSecurityGroupRuleSSH` tooallow TCP on port 22:</span></span>

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1000 --destination-port-range 22 --access allow \
  --name myNetworkSecurityGroupRuleSSH
```

<span data-ttu-id="e5178-304">Теперь добавим hello входящее правило для hello NSG tooallow входящих подключений через порт 80 (toosupport веб-трафик).</span><span class="sxs-lookup"><span data-stu-id="e5178-304">Now let's add hello inbound rule for hello NSG tooallow inbound connections on port 80 (toosupport web traffic).</span></span> <span data-ttu-id="e5178-305">Hello следующий код создает правило с именем `myNetworkSecurityGroupRuleHTTP` tooallow TCP через порт 80:</span><span class="sxs-lookup"><span data-stu-id="e5178-305">hello following example creates a rule named `myNetworkSecurityGroupRuleHTTP` tooallow TCP on port 80:</span></span>

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1001 --destination-port-range 80 --access allow \
  --name myNetworkSecurityGroupRuleHTTP
```

> [!NOTE]
> <span data-ttu-id="e5178-306">Правило входящего трафика Hello является фильтром для входящих подключений.</span><span class="sxs-lookup"><span data-stu-id="e5178-306">hello inbound rule is a filter for inbound network connections.</span></span> <span data-ttu-id="e5178-307">В этом примере выполняется привязка toohello NSG hello виртуальных машин виртуальный сетевой Адаптер, это означает, что любой запрос tooport 22 передается через toohello сетевого Адаптера на нашем виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="e5178-307">In this example, we bind hello NSG toohello VMs virtual NIC, which means that any request tooport 22 is passed through toohello NIC on our VM.</span></span> <span data-ttu-id="e5178-308">Это правило для входящего сетевого подключения, а не конечной точки, как это было бы в классическом развертывании.</span><span class="sxs-lookup"><span data-stu-id="e5178-308">This inbound rule is about a network connection, and not about an endpoint, which is what it would be about in classic deployments.</span></span> <span data-ttu-id="e5178-309">tooopen порт, необходимо оставить hello `--source-port-range` значение слишком "\*" tooaccept (значение по умолчанию hello) входящие запросы от **любой** запрашивает порта.</span><span class="sxs-lookup"><span data-stu-id="e5178-309">tooopen a port, you must leave hello `--source-port-range` set too'\*' (hello default value) tooaccept inbound requests from **any** requesting port.</span></span> <span data-ttu-id="e5178-310">Обычно порты являются динамическими.</span><span class="sxs-lookup"><span data-stu-id="e5178-310">Ports are typically dynamic.</span></span>
>
>

## <a name="bind-toohello-nic"></a><span data-ttu-id="e5178-311">Привязать toohello сетевого Адаптера</span><span class="sxs-lookup"><span data-stu-id="e5178-311">Bind toohello NIC</span></span>
<span data-ttu-id="e5178-312">Привязать hello NSG toohello сетевых адаптеров.</span><span class="sxs-lookup"><span data-stu-id="e5178-312">Bind hello NSG toohello NICs.</span></span> <span data-ttu-id="e5178-313">Мы должны tooconnect нашей сетевые адаптеры с нашей группой безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="e5178-313">We need tooconnect our NICs with our network security group.</span></span> <span data-ttu-id="e5178-314">Выполните обе команды toohook копирование оба наших сетевых адаптеров:</span><span class="sxs-lookup"><span data-stu-id="e5178-314">Run both commands, toohook up both of our NICs:</span></span>

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic1 \
  --network-security-group-name myNetworkSecurityGroup
```

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic2 \
  --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-an-availability-set"></a><span data-ttu-id="e5178-315">"Создать группу доступности"</span><span class="sxs-lookup"><span data-stu-id="e5178-315">Create an availability set</span></span>
<span data-ttu-id="e5178-316">Группы доступности помогают распределить виртуальные машины между доменами сбоя и доменами обновления.</span><span class="sxs-lookup"><span data-stu-id="e5178-316">Availability sets help spread your VMs across fault domains and upgrade domains.</span></span> <span data-ttu-id="e5178-317">Создадим группу доступности для виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e5178-317">Let's create an availability set for your VMs.</span></span> <span data-ttu-id="e5178-318">Hello следующий пример создает именованный набор доступности `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="e5178-318">hello following example creates an availability set named `myAvailabilitySet`:</span></span>

```azurecli
azure availset create --resource-group myResourceGroup --location westeurope
  --name myAvailabilitySet
```

<span data-ttu-id="e5178-319">Домены сбоя определяют группу виртуальных машин, совместно использующих общий источник питания и сетевой коммутатор.</span><span class="sxs-lookup"><span data-stu-id="e5178-319">Fault domains define a grouping of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="e5178-320">По умолчанию hello виртуальных машин, настроенных в наборе доступности должны быть разделены между toothree домены сбоя.</span><span class="sxs-lookup"><span data-stu-id="e5178-320">By default, hello virtual machines that are configured within your availability set are separated across up toothree fault domains.</span></span> <span data-ttu-id="e5178-321">Hello идея заключается в том, что проблема оборудования в одном из этих доменов сбоя не влияет на каждой виртуальной Машины, на котором выполняется приложение.</span><span class="sxs-lookup"><span data-stu-id="e5178-321">hello idea is that a hardware issue in one of these fault domains does not affect every VM that is running your app.</span></span> <span data-ttu-id="e5178-322">Azure автоматически распределяет виртуальные машины в доменах сбоя hello при помещении их в группу доступности.</span><span class="sxs-lookup"><span data-stu-id="e5178-322">Azure automatically distributes VMs across hello fault domains when placing them in an availability set.</span></span>

<span data-ttu-id="e5178-323">Домены обновления указания групп виртуальных машин и физического оборудования, можно перезагрузить в hello то же время.</span><span class="sxs-lookup"><span data-stu-id="e5178-323">Upgrade domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at hello same time.</span></span> <span data-ttu-id="e5178-324">порядок Hello перезагрузке доменов обновления могут быть непоследовательными во время планового обслуживания, но только одно обновление перезагружается одновременно.</span><span class="sxs-lookup"><span data-stu-id="e5178-324">hello order in which upgrade domains are rebooted might not be sequential during planned maintenance, but only one upgrade is rebooted at a time.</span></span> <span data-ttu-id="e5178-325">Опять же, Azure автоматически распределяет виртуальные машины между доменами обновления при помещении их в группу доступности.</span><span class="sxs-lookup"><span data-stu-id="e5178-325">Again, Azure automatically distributes your VMs across upgrade domains when placing them in an availability site.</span></span>

<span data-ttu-id="e5178-326">Дополнительные сведения о [управление hello доступности виртуальных машин](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e5178-326">Read more about [managing hello availability of VMs](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="create-hello-linux-vms"></a><span data-ttu-id="e5178-327">Создание виртуальных машин Linux hello</span><span class="sxs-lookup"><span data-stu-id="e5178-327">Create hello Linux VMs</span></span>
<span data-ttu-id="e5178-328">Вы создали hello ресурсы хранилища и сети виртуальных машин toosupport, доступном через Интернет.</span><span class="sxs-lookup"><span data-stu-id="e5178-328">You've created hello storage and network resources toosupport Internet-accessible VMs.</span></span> <span data-ttu-id="e5178-329">Теперь давайте создадим эти виртуальные машины и защитим их ключом SSH без пароля.</span><span class="sxs-lookup"><span data-stu-id="e5178-329">Now let's create those VMs and secure them with an SSH key that doesn't have a password.</span></span> <span data-ttu-id="e5178-330">В этом случае мы будем toocreate Виртуальной машине Ubuntu на основании hello последних Результатов.</span><span class="sxs-lookup"><span data-stu-id="e5178-330">In this case, we're going toocreate an Ubuntu VM based on hello most recent LTS.</span></span> <span data-ttu-id="e5178-331">Информацию об этом образе мы находим с помощью команды `azure vm image list`, как описано в статье о [поиске образов виртуальных машин Azure](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e5178-331">We locate that image information by using `azure vm image list`, as described in [finding Azure VM images](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="e5178-332">Мы выбрали образ с помощью команды hello `azure vm image list westeurope canonical | grep LTS`.</span><span class="sxs-lookup"><span data-stu-id="e5178-332">We selected an image by using hello command `azure vm image list westeurope canonical | grep LTS`.</span></span> <span data-ttu-id="e5178-333">В этом случае мы используем `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`.</span><span class="sxs-lookup"><span data-stu-id="e5178-333">In this case, we use `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`.</span></span> <span data-ttu-id="e5178-334">Для последнего поля hello, мы передаем `latest` , чтобы в будущем hello мы всегда получать последнюю сборку hello.</span><span class="sxs-lookup"><span data-stu-id="e5178-334">For hello last field, we pass `latest` so that in hello future we always get hello most recent build.</span></span> <span data-ttu-id="e5178-335">(мы используем строка hello `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).</span><span class="sxs-lookup"><span data-stu-id="e5178-335">(hello string we use is `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).</span></span>

<span data-ttu-id="e5178-336">Это следующий шаг — знакомый tooanyone, кто уже создал ssh открытого и закрытого ключей rsa сопряжения на Mac или Linux с помощью **ssh-keygen - t rsa -b 2048**.</span><span class="sxs-lookup"><span data-stu-id="e5178-336">This next step is familiar tooanyone who has already created an ssh rsa public and private key pair on Linux or Mac by using **ssh-keygen -t rsa -b 2048**.</span></span> <span data-ttu-id="e5178-337">Если в вашем каталоге `~/.ssh` нет пар ключей сертификата, то их можно создать:</span><span class="sxs-lookup"><span data-stu-id="e5178-337">If you do not have any certificate key pairs in your `~/.ssh` directory, you can create them:</span></span>

* <span data-ttu-id="e5178-338">Автоматически, с помощью hello `azure vm create --generate-ssh-keys` параметр.</span><span class="sxs-lookup"><span data-stu-id="e5178-338">Automatically, by using hello `azure vm create --generate-ssh-keys` option.</span></span>
* <span data-ttu-id="e5178-339">Вручную с помощью [toocreate инструкции hello их самостоятельно](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e5178-339">Manually, by using [hello instructions toocreate them yourself](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="e5178-340">Кроме того, можно использовать hello `--admin-password` метод tooauthenticate создания подключений SSH после hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="e5178-340">Alternatively, you can use hello `--admin-password` method tooauthenticate your SSH connections after hello VM is created.</span></span> <span data-ttu-id="e5178-341">Обычно этот метод менее безопасен.</span><span class="sxs-lookup"><span data-stu-id="e5178-341">This method is typically less secure.</span></span>

<span data-ttu-id="e5178-342">Мы создаем hello виртуальной Машине путем подключения к нашей ресурсы и сведения, а также hello `azure vm create` команды:</span><span class="sxs-lookup"><span data-stu-id="e5178-342">We create hello VM by bringing all our resources and information together with hello `azure vm create` command:</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM1 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic1 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

<span data-ttu-id="e5178-343">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e5178-343">Output:</span></span>

```azurecli
info:    Executing command vm create
+ Looking up hello VM "myVM1"
info:    Verifying hello public key SSH file: /home/ahmet/.ssh/id_rsa.pub
info:    Using hello VM Size "Standard_DS1"
info:    hello [OS, Data] Disk or image configuration requires storage account
+ Looking up hello storage account mystorageaccount
+ Looking up hello availability set "myAvailabilitySet"
info:    Found an Availability set "myAvailabilitySet"
+ Looking up hello NIC "myNic1"
info:    Found an existing NIC "myNic1"
info:    Found an IP configuration with virtual network subnet id "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet" in hello NIC "myNic1"
info:    This is an NIC without publicIP configured
info:    hello storage URI 'https://mystorageaccount.blob.core.windows.net/' will be used for boot diagnostics settings, and it can be overwritten by hello parameter input of '--boot-diagnostics-storage-uri'.
info:    vm create command OK
```

<span data-ttu-id="e5178-344">Немедленно tooyour ВМ можно подключиться с помощью ключей SSH по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e5178-344">You can connect tooyour VM immediately by using your default SSH keys.</span></span> <span data-ttu-id="e5178-345">Убедитесь, что указан соответствующий порт hello, так как мы передается через hello балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e5178-345">Make sure that you specify hello appropriate port since we're passing through hello load balancer.</span></span> <span data-ttu-id="e5178-346">(Для нашей первая виртуальная машина подготовим hello NAT правило tooforward порт 4222 tooour виртуальной Машины.)</span><span class="sxs-lookup"><span data-stu-id="e5178-346">(For our first VM, we set up hello NAT rule tooforward port 4222 tooour VM.)</span></span>

```bash
ssh ops@mypublicdns.westeurope.cloudapp.azure.com -p 4222
```

<span data-ttu-id="e5178-347">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e5178-347">Output:</span></span>

```bash
hello authenticity of host '[mypublicdns.westeurope.cloudapp.azure.com]:4222 ([xx.xx.xx.xx]:4222)' can't be established.
ECDSA key fingerprint is 94:2d:d0:ce:6b:fb:7f:ad:5b:3c:78:93:75:82:12:f9.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added '[mypublicdns.westeurope.cloudapp.azure.com]:4222,[xx.xx.xx.xx]:4222' (ECDSA) toohello list of known hosts.
Welcome tooUbuntu 16.04.1 LTS (GNU/Linux 4.4.0-34-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

ops@myVM1:~$
```

<span data-ttu-id="e5178-348">Создайте второй ВМ в hello так же:</span><span class="sxs-lookup"><span data-stu-id="e5178-348">Go ahead and create your second VM in hello same manner:</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM2 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic2 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

<span data-ttu-id="e5178-349">Теперь можно использовать hello `azure vm show myResourceGroup myVM1` команды tooexamine вы создали.</span><span class="sxs-lookup"><span data-stu-id="e5178-349">And you can now use hello `azure vm show myResourceGroup myVM1` command tooexamine what you've created.</span></span> <span data-ttu-id="e5178-350">На данном этапе имеются работающие виртуальные машины Ubuntu, расположенные за балансировщиком нагрузки в Azure, входить на которые можно только с помощью пары ключей SSH (так как пароли отключены).</span><span class="sxs-lookup"><span data-stu-id="e5178-350">At this point, you're running your Ubuntu VMs behind a load balancer in Azure that you can sign into only with your SSH key pair (because passwords are disabled).</span></span> <span data-ttu-id="e5178-351">Установить nginx или httpd, развертывание веб-приложения и видеть hello трафик проходил через hello tooboth подсистемы балансировки нагрузки виртуальных машин hello.</span><span class="sxs-lookup"><span data-stu-id="e5178-351">You can install nginx or httpd, deploy a web app, and see hello traffic flow through hello load balancer tooboth of hello VMs.</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myVM1
```

<span data-ttu-id="e5178-352">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e5178-352">Output:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up hello VM "TestVM1"
+ Looking up hello NIC "myNic1"
data:    Id                              :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Succeeded
data:    Name                            :myVM1
data:    Location                        :westeurope
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_DS1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :canonical
data:        Offer                       :UbuntuServer
data:        Sku                         :16.04.0-LTS
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :clib45a8b650f4428a1-os-1471973896525
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/clib45a8b650f4428a1-os-1471973896525.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-24-D4-AA
data:          Provisioning State        :Succeeded
data:          Name                      :LmyNic1
data:          Location                  :westeurope
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/availabilitySets/myAvailabilitySet
data:
data:    Diagnostics Profile:
data:      BootDiagnostics Enabled       :true
data:      BootDiagnostics StorageUri    :https://mystorageaccount.blob.core.windows.net/
data:
data:      Diagnostics Instance View:
info:    vm show command OK

```


## <a name="export-hello-environment-as-a-template"></a><span data-ttu-id="e5178-353">Экспорт hello среду как шаблон</span><span class="sxs-lookup"><span data-stu-id="e5178-353">Export hello environment as a template</span></span>
<span data-ttu-id="e5178-354">Теперь после создания этой среды, что делать, если вы хотите toocreate среде дополнительная разработка с hello такими же параметрами или рабочей среде, которая сопоставляет его?</span><span class="sxs-lookup"><span data-stu-id="e5178-354">Now that you have built out this environment, what if you want toocreate an additional development environment with hello same parameters, or a production environment that matches it?</span></span> <span data-ttu-id="e5178-355">Диспетчер ресурсов использует JSON шаблонов, определяющих все параметры hello для вашей среды.</span><span class="sxs-lookup"><span data-stu-id="e5178-355">Resource Manager uses JSON templates that define all hello parameters for your environment.</span></span> <span data-ttu-id="e5178-356">Можно полностью создавать среды, ссылаясь на этот шаблон JSON.</span><span class="sxs-lookup"><span data-stu-id="e5178-356">You build out entire environments by referencing this JSON template.</span></span> <span data-ttu-id="e5178-357">Вы можете [вручную построить шаблоны JSON](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) или экспортировать существующий шаблон JSON hello toocreate среды:</span><span class="sxs-lookup"><span data-stu-id="e5178-357">You can [build JSON templates manually](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or export an existing environment toocreate hello JSON template for you:</span></span>

```azurecli
azure group export --name myResourceGroup
```

<span data-ttu-id="e5178-358">Эта команда создает hello `myResourceGroup.json` файла в текущий рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="e5178-358">This command creates hello `myResourceGroup.json` file in your current working directory.</span></span> <span data-ttu-id="e5178-359">При создании среды на основе этого шаблона, запрашиваются все имена ресурсов hello, включая имена hello для балансировки нагрузки hello, сетевые интерфейсы или виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e5178-359">When you create an environment from this template, you are prompted for all hello resource names, including hello names for hello load balancer, network interfaces, or VMs.</span></span> <span data-ttu-id="e5178-360">Эти имена можно заполнить в файле шаблона, добавляя hello `-p` или `--includeParameterDefaultValue` toohello параметр `azure group export` команду, которая было показано ранее.</span><span class="sxs-lookup"><span data-stu-id="e5178-360">You can populate these names in your template file by adding hello `-p` or `--includeParameterDefaultValue` parameter toohello `azure group export` command that was shown earlier.</span></span> <span data-ttu-id="e5178-361">Редактирование JSON шаблона toospecify hello имена ресурсов, или [создайте файл parameters.json](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) , указывающий имена ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="e5178-361">Edit your JSON template toospecify hello resource names, or [create a parameters.json file](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that specifies hello resource names.</span></span>

<span data-ttu-id="e5178-362">toocreate среды из шаблона:</span><span class="sxs-lookup"><span data-stu-id="e5178-362">toocreate an environment from your template:</span></span>

```azurecli
azure group deployment create --resource-group myNewResourceGroup \
  --template-file myResourceGroup.json
```

<span data-ttu-id="e5178-363">Может потребоваться tooread [Дополнительные сведения о том, как toodeploy из шаблонов](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e5178-363">You might want tooread [more about how toodeploy from templates](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="e5178-364">Сведения о средах обновление tooincrementally, использовать файл параметров hello и получить доступ к шаблонам с единым хранилища.</span><span class="sxs-lookup"><span data-stu-id="e5178-364">Learn about how tooincrementally update environments, use hello parameters file, and access templates from a single storage location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5178-365">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e5178-365">Next steps</span></span>
<span data-ttu-id="e5178-366">Теперь вы готовы toobegin работа с несколькими сетевыми компонентами и виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="e5178-366">Now you're ready toobegin working with multiple networking components and VMs.</span></span> <span data-ttu-id="e5178-367">Toobuild среды этот образец можно использовать из приложения с помощью hello основные компоненты представленные здесь.</span><span class="sxs-lookup"><span data-stu-id="e5178-367">You can use this sample environment toobuild out your application by using hello core components introduced here.</span></span>
