---
title: "aaaOpen порты tooa виртуальных Машин Linux с помощью Azure CLI 2.0 | Документы Microsoft"
description: "Узнайте, как tooopen порт / create tooyour конечной точки виртуальной Машины с Linux с помощью развертывания диспетчера ресурсов Azure hello модели и hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: eef9842b-495a-46cf-99a6-74e49807e74e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: c79b31206e97558171609cf033bb3cb3370777c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-and-endpoints-tooa-linux-vm-with-hello-azure-cli"></a><span data-ttu-id="3dda7-103">Откройте порты и конечные точки tooa виртуальных Машин Linux с hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3dda7-103">Open ports and endpoints tooa Linux VM with hello Azure CLI</span></span>
<span data-ttu-id="3dda7-104">Открытие порта, или создайте конечную точку, tooa виртуальной машины (VM в Azure, создав фильтр сети для подсети или сетевому интерфейсу виртуальной Машины).</span><span class="sxs-lookup"><span data-stu-id="3dda7-104">You open a port, or create an endpoint, tooa virtual machine (VM) in Azure by creating a network filter on a subnet or VM network interface.</span></span> <span data-ttu-id="3dda7-105">Эти фильтры, которые позволяют управлять входящего и исходящего трафика, поместите на ресурсе toohello вложенные группы безопасности сети, который принимает трафик hello.</span><span class="sxs-lookup"><span data-stu-id="3dda7-105">You place these filters, which control both inbound and outbound traffic, on a Network Security Group attached toohello resource that receives hello traffic.</span></span> <span data-ttu-id="3dda7-106">Давайте используем распространенный пример веб-трафика через порт 80.</span><span class="sxs-lookup"><span data-stu-id="3dda7-106">Let's use a common example of web traffic on port 80.</span></span> <span data-ttu-id="3dda7-107">В этой статье показано, как tooopen tooa порт виртуальной Машины с hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="3dda7-107">This article shows you how tooopen a port tooa VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="3dda7-108">Можно также выполнить следующие действия с hello [Azure CLI 1.0](nsg-quickstart-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="3dda7-108">You can also perform these steps with hello [Azure CLI 1.0](nsg-quickstart-nodejs.md).</span></span>


## <a name="quick-commands"></a><span data-ttu-id="3dda7-109">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="3dda7-109">Quick commands</span></span>
<span data-ttu-id="3dda7-110">Группы безопасности сети toocreate и правила, которые требуется последняя версия hello [Azure CLI 2.0](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="3dda7-110">toocreate a Network Security Group and rules you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="3dda7-111">В hello следующих примерах замените примеры имен параметров собственные значения.</span><span class="sxs-lookup"><span data-stu-id="3dda7-111">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="3dda7-112">Примеры имен параметров: *myResourceGroup*, *mystorageaccount* и *myVM*.</span><span class="sxs-lookup"><span data-stu-id="3dda7-112">Example parameter names include *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="3dda7-113">Создание группы безопасности сети hello с [создать az сети nsg](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="3dda7-113">Create hello network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="3dda7-114">Hello следующий пример создает группу безопасности сети с именем *myNetworkSecurityGroup* в hello *eastus* расположение:</span><span class="sxs-lookup"><span data-stu-id="3dda7-114">hello following example creates a network security group named *myNetworkSecurityGroup* in hello *eastus* location:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="3dda7-115">Добавить правило с [создать правило nsg сети az](/cli/azure/network/nsg/rule#create) tooallow HTTP-трафик, tooyour веб-сервер (или настроить для собственных сценариев, например для подключения SSH access или базы данных).</span><span class="sxs-lookup"><span data-stu-id="3dda7-115">Add a rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) tooallow HTTP traffic tooyour webserver (or adjust for your own scenario, such as SSH access or database connectivity).</span></span> <span data-ttu-id="3dda7-116">Hello следующий код создает правило с именем *myNetworkSecurityGroupRule* tooallow TCP-трафик через порт 80:</span><span class="sxs-lookup"><span data-stu-id="3dda7-116">hello following example creates a rule named *myNetworkSecurityGroupRule* tooallow TCP traffic on port 80:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 80
```

<span data-ttu-id="3dda7-117">Связать hello сетевой группы безопасности с сетевым интерфейсом Виртуальной машины (NIC) с [обновления сетевого адаптера сети az](/cli/azure/network/nic#update).</span><span class="sxs-lookup"><span data-stu-id="3dda7-117">Associate hello Network Security Group with your VM's network interface (NIC) with [az network nic update](/cli/azure/network/nic#update).</span></span> <span data-ttu-id="3dda7-118">Hello следующий пример сопоставляет существующего сетевого Адаптера с именем *myNic* с hello сетевую группу безопасности с именем *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="3dda7-118">hello following example associates an existing NIC named *myNic* with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nic update \
    --resource-group myResourceGroup \
    --name myNic \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="3dda7-119">Кроме того, можно поставить в вашей группе безопасности сети подсети виртуальной сети с [обновления подсети виртуальной сети сети az](/cli/azure/network/vnet/subnet#update) вместо просто toohello сетевого интерфейса на одной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="3dda7-119">Alternatively, you can associate your Network Security Group with a virtual network subnet with [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) rather than just toohello network interface on a single VM.</span></span> <span data-ttu-id="3dda7-120">Hello следующем примере производится связывание существующей подсети с именем *mySubnet* в hello *myVnet* виртуальную сеть с hello сетевую группу безопасности с именем *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="3dda7-120">hello following example associates an existing subnet named *mySubnet* in hello *myVnet* virtual network with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="3dda7-121">Дополнительная информация о группах безопасности сети</span><span class="sxs-lookup"><span data-stu-id="3dda7-121">More information on Network Security Groups</span></span>
<span data-ttu-id="3dda7-122">Hello здесь Быстрые команды позволяют tooget вверх и работает с tooyour передачу трафика виртуальных Машин.</span><span class="sxs-lookup"><span data-stu-id="3dda7-122">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="3dda7-123">Сетевые группы безопасности предоставляют много замечательных функций и гранулярности для управления доступа к ресурсам tooyour.</span><span class="sxs-lookup"><span data-stu-id="3dda7-123">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="3dda7-124">[Здесь](tutorial-virtual-network.md#secure-network-traffic)вы можете больше прочитать о создании группы безопасности сети и правил ACL.</span><span class="sxs-lookup"><span data-stu-id="3dda7-124">You can read more about [creating a Network Security Group and ACL rules here](tutorial-virtual-network.md#secure-network-traffic).</span></span>

<span data-ttu-id="3dda7-125">Для веб-приложений с высокой доступностью необходимо поместить виртуальную машину за Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="3dda7-125">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="3dda7-126">Подсистема балансировки нагрузки Hello распределяет трафик tooVMs, с группой безопасности сети, которая обеспечивает фильтрацию трафика.</span><span class="sxs-lookup"><span data-stu-id="3dda7-126">hello load balancer distributes traffic tooVMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="3dda7-127">Дополнительные сведения см. в разделе [как баланс tooload Linux виртуальных машин в Azure toocreate приложение с высокой доступностью](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="3dda7-127">For more information, see [How tooload balance Linux virtual machines in Azure toocreate a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3dda7-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3dda7-128">Next steps</span></span>
<span data-ttu-id="3dda7-129">В этом примере вы создали трафика tooallow HTTP простое правило.</span><span class="sxs-lookup"><span data-stu-id="3dda7-129">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="3dda7-130">Можно найти сведения о создании более подробные сред в hello в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="3dda7-130">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="3dda7-131">Общие сведения об Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3dda7-131">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="3dda7-132">Группа безопасности сети</span><span class="sxs-lookup"><span data-stu-id="3dda7-132">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
