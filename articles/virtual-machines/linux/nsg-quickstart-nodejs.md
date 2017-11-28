---
title: "aaaOpen порты tooa виртуальных Машин Linux с помощью Azure CLI 1.0 | Документы Microsoft"
description: "Узнайте, как tooopen порт / create tooyour конечной точки виртуальной Машины с Linux с помощью развертывания диспетчера ресурсов Azure hello модели и hello Azure CLI 1.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 337c37d151f527b43d4852291159b2f70a00accc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="opening-ports-and-endpoints-tooa-linux-vm-in-azure-using-hello-azure-cli-10"></a><span data-ttu-id="5f5d4-103">Открытие портов и конечные точки tooa виртуальных Машин Linux в Azure с помощью hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="5f5d4-103">Opening ports and endpoints tooa Linux VM in Azure using hello Azure CLI 1.0</span></span>
<span data-ttu-id="5f5d4-104">Открытие порта, или создайте конечную точку, tooa виртуальной машины (VM в Azure, создав фильтр сети для подсети или сетевому интерфейсу виртуальной Машины).</span><span class="sxs-lookup"><span data-stu-id="5f5d4-104">You open a port, or create an endpoint, tooa virtual machine (VM) in Azure by creating a network filter on a subnet or VM network interface.</span></span> <span data-ttu-id="5f5d4-105">Эти фильтры, которые позволяют управлять входящего и исходящего трафика, поместите на ресурсе toohello вложенные группы безопасности сети, который принимает трафик hello.</span><span class="sxs-lookup"><span data-stu-id="5f5d4-105">You place these filters, which control both inbound and outbound traffic, on a Network Security Group attached toohello resource that receives hello traffic.</span></span> <span data-ttu-id="5f5d4-106">Давайте используем распространенный пример веб-трафика через порт 80.</span><span class="sxs-lookup"><span data-stu-id="5f5d4-106">Let's use a common example of web traffic on port 80.</span></span> <span data-ttu-id="5f5d4-107">В этой статье показано, как использование виртуальной Машины порт tooa tooopen hello Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="5f5d4-107">This article shows you how tooopen a port tooa VM using hello Azure CLI 1.0.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="5f5d4-108">Задача hello toocomplete версии CLI</span><span class="sxs-lookup"><span data-stu-id="5f5d4-108">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="5f5d4-109">Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.</span><span class="sxs-lookup"><span data-stu-id="5f5d4-109">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="5f5d4-110">[Azure CLI 1.0](#quick-commands) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)</span><span class="sxs-lookup"><span data-stu-id="5f5d4-110">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="5f5d4-111">[Azure CLI 2.0](nsg-quickstart.md) -нашей нового поколения CLI для модели развертывания hello ресурсов управления</span><span class="sxs-lookup"><span data-stu-id="5f5d4-111">[Azure CLI 2.0](nsg-quickstart.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="5f5d4-112">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="5f5d4-112">Quick commands</span></span>
<span data-ttu-id="5f5d4-113">toocreate сетевой группы безопасности и правила необходимо [hello Azure CLI 1.0](../../cli-install-nodejs.md) установлен и использование режима диспетчера ресурсов:</span><span class="sxs-lookup"><span data-stu-id="5f5d4-113">toocreate a Network Security Group and rules you need [hello Azure CLI 1.0](../../cli-install-nodejs.md) installed and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="5f5d4-114">В hello следующих примерах замените примеры имен параметров собственные значения.</span><span class="sxs-lookup"><span data-stu-id="5f5d4-114">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="5f5d4-115">Примеры имен параметров: *myResourceGroup*, *mystorageaccount* и *myVM*.</span><span class="sxs-lookup"><span data-stu-id="5f5d4-115">Example parameter names included *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="5f5d4-116">Создайте группу безопасности сети, указав собственные имена и расположение.</span><span class="sxs-lookup"><span data-stu-id="5f5d4-116">Create your Network Security Group, entering your own names and location appropriately.</span></span> <span data-ttu-id="5f5d4-117">Hello следующий пример создает группу безопасности сети с именем *myNetworkSecurityGroup* в hello *eastus* расположение:</span><span class="sxs-lookup"><span data-stu-id="5f5d4-117">hello following example creates a Network Security Group named *myNetworkSecurityGroup* in hello *eastus* location:</span></span>

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="5f5d4-118">Добавить веб-серверу трафика tooyour правило tooallow HTTP (или настроить для собственных сценариев, например для подключения SSH access или базы данных).</span><span class="sxs-lookup"><span data-stu-id="5f5d4-118">Add a rule tooallow HTTP traffic tooyour webserver (or adjust for your own scenario, such as SSH access or database connectivity).</span></span> <span data-ttu-id="5f5d4-119">Hello следующий код создает правило с именем *myNetworkSecurityGroupRule* tooallow TCP-трафик через порт 80:</span><span class="sxs-lookup"><span data-stu-id="5f5d4-119">hello following example creates a rule named *myNetworkSecurityGroupRule* tooallow TCP traffic on port 80:</span></span>

```azurecli
azure network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --destination-port-range 80 \
    --access allow
```

<span data-ttu-id="5f5d4-120">Свяжите hello группы безопасности сети с Виртуальной машины сетевого интерфейса (NIC).</span><span class="sxs-lookup"><span data-stu-id="5f5d4-120">Associate hello Network Security Group with your VM's network interface (NIC).</span></span> <span data-ttu-id="5f5d4-121">Hello следующий пример сопоставляет существующего сетевого Адаптера с именем *myNic* с hello сетевую группу безопасности с именем *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="5f5d4-121">hello following example associates an existing NIC named *myNic* with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --name myNic
```

<span data-ttu-id="5f5d4-122">Кроме того можно связать вашей группе безопасности сети с подсеть виртуальной сети, а не просто toohello сетевого интерфейса на одной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5f5d4-122">Alternatively, you can associate your Network Security Group with a virtual network subnet rather than just toohello network interface on a single VM.</span></span> <span data-ttu-id="5f5d4-123">Hello следующем примере производится связывание существующей подсети с именем *mySubnet* в hello *myVnet* виртуальную сеть с hello сетевую группу безопасности с именем *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="5f5d4-123">hello following example associates an existing subnet named *mySubnet* in hello *myVnet* virtual network with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network vnet subnet set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --vnet-name myVnet --name mySubnet
```

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="5f5d4-124">Дополнительная информация о группах безопасности сети</span><span class="sxs-lookup"><span data-stu-id="5f5d4-124">More information on Network Security Groups</span></span>
<span data-ttu-id="5f5d4-125">Hello здесь Быстрые команды позволяют tooget вверх и работает с tooyour передачу трафика виртуальных Машин.</span><span class="sxs-lookup"><span data-stu-id="5f5d4-125">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="5f5d4-126">Сетевые группы безопасности предоставляют много замечательных функций и гранулярности для управления доступа к ресурсам tooyour.</span><span class="sxs-lookup"><span data-stu-id="5f5d4-126">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="5f5d4-127">[Здесь](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)вы можете больше прочитать о создании группы безопасности сети и правил ACL.</span><span class="sxs-lookup"><span data-stu-id="5f5d4-127">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span></span>

<span data-ttu-id="5f5d4-128">Группы безопасности сети и правила ACL можно также определять в шаблонах Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5f5d4-128">You can define Network Security Groups and ACL rules as part of Azure Resource Manager templates.</span></span> <span data-ttu-id="5f5d4-129">Узнайте больше о [создании групп безопасности сети с помощью шаблонов](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="5f5d4-129">Read more about [creating Network Security Groups with templates](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span></span>

<span data-ttu-id="5f5d4-130">Перенаправление портов toouse toomap внутренний порт tooan уникальный внешний порт на виртуальной Машине, используйте подсистему балансировки нагрузки и правила преобразования сетевых адресов (NAT).</span><span class="sxs-lookup"><span data-stu-id="5f5d4-130">If you need toouse port-forwarding toomap a unique external port tooan internal port on your VM, use a load balancer and Network Address Translation (NAT) rules.</span></span> <span data-ttu-id="5f5d4-131">Например можно tooexpose TCP-порт 8080 извне и трафик, направленный tooTCP порт 80 на виртуальной Машине.</span><span class="sxs-lookup"><span data-stu-id="5f5d4-131">For example, you may want tooexpose TCP port 8080 externally and have traffic directed tooTCP port 80 on a VM.</span></span> <span data-ttu-id="5f5d4-132">Вы можете узнать о [создании балансировщика нагрузки с выходом в Интернет](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5f5d4-132">You can learn about [creating an Internet-facing load balancer](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f5d4-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5f5d4-133">Next steps</span></span>
<span data-ttu-id="5f5d4-134">В этом примере вы создали трафика tooallow HTTP простое правило.</span><span class="sxs-lookup"><span data-stu-id="5f5d4-134">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="5f5d4-135">Можно найти сведения о создании более подробные сред в hello в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="5f5d4-135">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="5f5d4-136">Общие сведения об Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5f5d4-136">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="5f5d4-137">Группа безопасности сети</span><span class="sxs-lookup"><span data-stu-id="5f5d4-137">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="5f5d4-138">Поддержка диспетчера ресурсов Azure для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="5f5d4-138">Azure Resource Manager Overview for Load Balancers</span></span>](../../load-balancer/load-balancer-arm.md)

