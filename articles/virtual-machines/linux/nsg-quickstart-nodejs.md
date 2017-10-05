---
title: "Открытие портов для виртуальной машины Linux с помощью интерфейса командной строки Azure 1.0 | Документация Майкрософт"
description: "Узнайте, как открыть порт или создать конечную точку для виртуальной машины Linux, используя модель развертывания с помощью Azure Resource Manager и Azure CLI 1.0."
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
ms.openlocfilehash: 847bc76c37ed929851712ba1c12463a01032e267
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="opening-ports-and-endpoints-to-a-linux-vm-in-azure-using-the-azure-cli-10"></a><span data-ttu-id="d3caf-103">Открытие портов и конечных точек для виртуальной машины Linux в Azure с помощью интерфейса командной строки Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="d3caf-103">Opening ports and endpoints to a Linux VM in Azure using the Azure CLI 1.0</span></span>
<span data-ttu-id="d3caf-104">Чтобы открыть порт или создать конечную точку для виртуальной машины в Azure, создайте сетевой фильтр для подсети или сетевого интерфейса виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d3caf-104">You open a port, or create an endpoint, to a virtual machine (VM) in Azure by creating a network filter on a subnet or VM network interface.</span></span> <span data-ttu-id="d3caf-105">Эти фильтры, контролирующие входящий и исходящий трафик, добавляются в группу безопасности сети и присоединяются к ресурсу, который будет получать трафик.</span><span class="sxs-lookup"><span data-stu-id="d3caf-105">You place these filters, which control both inbound and outbound traffic, on a Network Security Group attached to the resource that receives the traffic.</span></span> <span data-ttu-id="d3caf-106">Давайте используем распространенный пример веб-трафика через порт 80.</span><span class="sxs-lookup"><span data-stu-id="d3caf-106">Let's use a common example of web traffic on port 80.</span></span> <span data-ttu-id="d3caf-107">В этой статье показано, как открыть порт для виртуальной машины с помощью интерфейса командной строки Azure версии 1.0.</span><span class="sxs-lookup"><span data-stu-id="d3caf-107">This article shows you how to open a port to a VM using the Azure CLI 1.0.</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="d3caf-108">Версии интерфейса командной строки для выполнения задачи</span><span class="sxs-lookup"><span data-stu-id="d3caf-108">CLI versions to complete the task</span></span>
<span data-ttu-id="d3caf-109">Вы можете выполнить задачу, используя одну из следующих версий интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="d3caf-109">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="d3caf-110">[Azure CLI 1.0](#quick-commands) — интерфейс командной строки для классической модели развертывания и модели развертывания Resource Manager (в этой статье).</span><span class="sxs-lookup"><span data-stu-id="d3caf-110">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="d3caf-111">[Azure CLI 2.0](nsg-quickstart.md) — интерфейс командной строки следующего поколения для модели развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d3caf-111">[Azure CLI 2.0](nsg-quickstart.md) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="d3caf-112">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="d3caf-112">Quick commands</span></span>
<span data-ttu-id="d3caf-113">Для создания группы безопасности сети и правил нужно установить [интерфейс командной строки Azure версии 1.0](../../cli-install-nodejs.md) и перевести его в режим Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d3caf-113">To create a Network Security Group and rules you need [the Azure CLI 1.0](../../cli-install-nodejs.md) installed and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="d3caf-114">В следующих примерах замените имена параметров собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="d3caf-114">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="d3caf-115">Примеры имен параметров: *myResourceGroup*, *mystorageaccount* и *myVM*.</span><span class="sxs-lookup"><span data-stu-id="d3caf-115">Example parameter names included *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="d3caf-116">Создайте группу безопасности сети, указав собственные имена и расположение.</span><span class="sxs-lookup"><span data-stu-id="d3caf-116">Create your Network Security Group, entering your own names and location appropriately.</span></span> <span data-ttu-id="d3caf-117">В следующем примере создается группа безопасности сети *myNetworkSecurityGroup* в расположении *eastus*.</span><span class="sxs-lookup"><span data-stu-id="d3caf-117">The following example creates a Network Security Group named *myNetworkSecurityGroup* in the *eastus* location:</span></span>

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="d3caf-118">Добавьте правило, разрешающее HTTP-трафик к вашему веб-серверу (или настройте правило под собственные нужды, например доступ по протоколу SSH или подключение к базе данных).</span><span class="sxs-lookup"><span data-stu-id="d3caf-118">Add a rule to allow HTTP traffic to your webserver (or adjust for your own scenario, such as SSH access or database connectivity).</span></span> <span data-ttu-id="d3caf-119">В следующем примере создается правило с именем *myNetworkSecurityGroupRule*. Это правило разрешает TCP-трафик через порт 80:</span><span class="sxs-lookup"><span data-stu-id="d3caf-119">The following example creates a rule named *myNetworkSecurityGroupRule* to allow TCP traffic on port 80:</span></span>

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

<span data-ttu-id="d3caf-120">Свяжите группу безопасности сети с сетевым интерфейсом виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d3caf-120">Associate the Network Security Group with your VM's network interface (NIC).</span></span> <span data-ttu-id="d3caf-121">В следующем примере существующий сетевой адаптер *myNic* связывается с группой безопасности сети *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="d3caf-121">The following example associates an existing NIC named *myNic* with the Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --name myNic
```

<span data-ttu-id="d3caf-122">Кроме того, группу безопасности сети можно связать с подсетью виртуальной сети, а не только с сетевым интерфейсом на отдельной виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="d3caf-122">Alternatively, you can associate your Network Security Group with a virtual network subnet rather than just to the network interface on a single VM.</span></span> <span data-ttu-id="d3caf-123">В следующем примере существующий сетевой адаптер *myNic* в виртуальной сети *myVnet* связывается с группой безопасности сети *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="d3caf-123">The following example associates an existing subnet named *mySubnet* in the *myVnet* virtual network with the Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network vnet subnet set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --vnet-name myVnet --name mySubnet
```

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="d3caf-124">Дополнительная информация о группах безопасности сети</span><span class="sxs-lookup"><span data-stu-id="d3caf-124">More information on Network Security Groups</span></span>
<span data-ttu-id="d3caf-125">Приведенные здесь быстрые команды позволят настроить трафик, поступающий в виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="d3caf-125">The quick commands here allow you to get up and running with traffic flowing to your VM.</span></span> <span data-ttu-id="d3caf-126">Группы безопасности сети предоставляют множество полезных функций и всевозможные настройки для управления доступом к ресурсам.</span><span class="sxs-lookup"><span data-stu-id="d3caf-126">Network Security Groups provide many great features and granularity for controlling access to your resources.</span></span> <span data-ttu-id="d3caf-127">[Здесь](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)вы можете больше прочитать о создании группы безопасности сети и правил ACL.</span><span class="sxs-lookup"><span data-stu-id="d3caf-127">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span></span>

<span data-ttu-id="d3caf-128">Группы безопасности сети и правила ACL можно также определять в шаблонах Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d3caf-128">You can define Network Security Groups and ACL rules as part of Azure Resource Manager templates.</span></span> <span data-ttu-id="d3caf-129">Узнайте больше о [создании групп безопасности сети с помощью шаблонов](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="d3caf-129">Read more about [creating Network Security Groups with templates](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span></span>

<span data-ttu-id="d3caf-130">Если необходимо использовать перенаправление портов, чтобы сопоставить уникальный внешний порт с внутренним портом на своей виртуальной машине, то воспользуйтесь балансировщиком нагрузки и правилами преобразования сетевых адресов (NAT).</span><span class="sxs-lookup"><span data-stu-id="d3caf-130">If you need to use port-forwarding to map a unique external port to an internal port on your VM, use a load balancer and Network Address Translation (NAT) rules.</span></span> <span data-ttu-id="d3caf-131">Например, может потребоваться открыть TCP-порт 8080 для доступа извне и направить трафик на TCP-порт 80 виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d3caf-131">For example, you may want to expose TCP port 8080 externally and have traffic directed to TCP port 80 on a VM.</span></span> <span data-ttu-id="d3caf-132">Вы можете узнать о [создании балансировщика нагрузки с выходом в Интернет](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="d3caf-132">You can learn about [creating an Internet-facing load balancer](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3caf-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d3caf-133">Next steps</span></span>
<span data-ttu-id="d3caf-134">В этом примере создано простое правило, разрешающее трафик HTTP.</span><span class="sxs-lookup"><span data-stu-id="d3caf-134">In this example, you created a simple rule to allow HTTP traffic.</span></span> <span data-ttu-id="d3caf-135">Информацию о создании более детализированных сред можно найти в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="d3caf-135">You can find information on creating more detailed environments in the following articles:</span></span>

* [<span data-ttu-id="d3caf-136">Общие сведения об Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d3caf-136">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="d3caf-137">Группа безопасности сети</span><span class="sxs-lookup"><span data-stu-id="d3caf-137">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="d3caf-138">Поддержка диспетчера ресурсов Azure для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="d3caf-138">Azure Resource Manager Overview for Load Balancers</span></span>](../../load-balancer/load-balancer-arm.md)

