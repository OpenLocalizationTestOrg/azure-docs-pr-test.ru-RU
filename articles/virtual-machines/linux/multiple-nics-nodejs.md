---
title: "aaaCreate виртуальной Машины Linux в Azure с несколькими сетевыми адаптерами | Документы Microsoft"
description: "Узнайте, как toocreate ВМ Linux с несколькими сетевыми адаптерами присоединенного tooit с помощью шаблонов hello Azure CLI или диспетчер ресурсов."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 457dab734ceeeefd35cddaf1ebb9ea0a82f4e207
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-multiple-nics-using-hello-azure-cli-10"></a><span data-ttu-id="62889-103">Создание виртуальной машины Linux с несколькими сетевыми адаптерами, используя hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="62889-103">Create a Linux virtual machine with multiple NICs using hello Azure CLI 1.0</span></span>
<span data-ttu-id="62889-104">Можно создать виртуальную машину (ВМ) в Azure, которая имеет несколько tooit интерфейсов (NIC), подключенных виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="62889-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached tooit.</span></span> <span data-ttu-id="62889-105">Типичный сценарий состоит в разных подсетях toohave для внешнего и внутреннего интерфейса подключения или сеть, выделенная tooa наблюдения или решение для резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="62889-105">A common scenario is toohave different subnets for front-end and back-end connectivity, or a network dedicated tooa monitoring or backup solution.</span></span> <span data-ttu-id="62889-106">Эта статья содержит toocreate Быстрые команды виртуальной Машины с несколькими tooit присоединенного сетевых адаптеров.</span><span class="sxs-lookup"><span data-stu-id="62889-106">This article provides quick commands toocreate a VM with multiple NICs attached tooit.</span></span> <span data-ttu-id="62889-107">Подробные сведения, включая как toocreate несколько сетевых адаптеров в собственных Bash скрипты, Дополнительные сведения о [развертывание виртуальных машин multi-NIC](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="62889-107">For detailed information, including how toocreate multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span></span> <span data-ttu-id="62889-108">Различные [размеры виртуальных машин](sizes.md) поддерживают разное число сетевых карт, так что выбирайте соответствующий размер виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="62889-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

> [!WARNING]
> <span data-ttu-id="62889-109">Необходимо подключить несколько сетевых адаптеров, после создания виртуальной Машины — не удается добавить существующие ВМ в Azure CLI 1.0 hello tooan сетевых адаптеров.</span><span class="sxs-lookup"><span data-stu-id="62889-109">You must attach multiple NICs when you create a VM - you cannot add NICs tooan existing VM with hello Azure CLI 1.0.</span></span> <span data-ttu-id="62889-110">Вы можете [добавить существующие ВМ в Azure CLI 2.0 hello tooan сетевые адаптеры](multiple-nics.md).</span><span class="sxs-lookup"><span data-stu-id="62889-110">You can [add NICs tooan existing VM with hello Azure CLI 2.0](multiple-nics.md).</span></span> <span data-ttu-id="62889-111">Вы также можете [создания основании hello исходные виртуальные диски виртуальной Машины](copy-vm.md) и создать несколько сетевых адаптеров, при развертывании виртуальной Машины hello.</span><span class="sxs-lookup"><span data-stu-id="62889-111">You can also [create a VM based on hello original virtual disk(s)](copy-vm.md) and create multiple NICs as you deploy hello VM.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="62889-112">Задача hello toocomplete версии CLI</span><span class="sxs-lookup"><span data-stu-id="62889-112">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="62889-113">Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.</span><span class="sxs-lookup"><span data-stu-id="62889-113">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="62889-114">[Azure CLI 1.0](#create-supporting-resources) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)</span><span class="sxs-lookup"><span data-stu-id="62889-114">[Azure CLI 1.0](#create-supporting-resources) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="62889-115">[Azure CLI 2.0](multiple-nics.md) -нашей нового поколения CLI для модели развертывания hello ресурсов управления</span><span class="sxs-lookup"><span data-stu-id="62889-115">[Azure CLI 2.0](multiple-nics.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="create-supporting-resources"></a><span data-ttu-id="62889-116">Создание вспомогательных ресурсов</span><span class="sxs-lookup"><span data-stu-id="62889-116">Create supporting resources</span></span>
<span data-ttu-id="62889-117">Убедитесь, что имеется hello [Azure CLI](../../cli-install-nodejs.md) входа в систему и использование режима диспетчера ресурсов:</span><span class="sxs-lookup"><span data-stu-id="62889-117">Make sure that you have hello [Azure CLI](../../cli-install-nodejs.md) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="62889-118">В hello следующих примерах замените примеры имен параметров собственные значения.</span><span class="sxs-lookup"><span data-stu-id="62889-118">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="62889-119">Примеры имен параметров: *myResourceGroup*, *mystorageaccount* и *myVM*.</span><span class="sxs-lookup"><span data-stu-id="62889-119">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *myVM*.</span></span>

<span data-ttu-id="62889-120">Сначала создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="62889-120">First, create a resource group.</span></span> <span data-ttu-id="62889-121">Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение:</span><span class="sxs-lookup"><span data-stu-id="62889-121">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
azure group create myResourceGroup --location eastus
```

<span data-ttu-id="62889-122">Создание учетной записи хранилища toohold виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="62889-122">Create a storage account toohold your VMs.</span></span> <span data-ttu-id="62889-123">Hello следующий пример создает учетную запись хранения с именем *mystorageaccount*:</span><span class="sxs-lookup"><span data-stu-id="62889-123">hello following example creates a storage account named *mystorageaccount*:</span></span>

```azurecli
azure storage account create mystorageaccount \
    --resource-group myResourceGroup \
    --location eastus \
    --kind Storage \
    --sku-name PLRS
```

<span data-ttu-id="62889-124">Создайте виртуальные машины tooconnect виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="62889-124">Create a virtual network tooconnect your VMs to.</span></span> <span data-ttu-id="62889-125">Hello следующий пример создает виртуальную сеть с именем *myVnet* с префикс адреса *192.168.0.0/16*:</span><span class="sxs-lookup"><span data-stu-id="62889-125">hello following example creates a virtual network named *myVnet* with an address prefix of *192.168.0.0/16*:</span></span>

```azurecli
azure network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefixes 192.168.0.0/16
```

<span data-ttu-id="62889-126">Создайте две подсети виртуальной сети — для интерфейсного трафика и для внутреннего трафика.</span><span class="sxs-lookup"><span data-stu-id="62889-126">Create two virtual network subnets - one for front-end traffic and one for back-end traffic.</span></span> <span data-ttu-id="62889-127">Hello следующий пример создает две подсети, с именем *mySubnetFrontEnd* и *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="62889-127">hello following example creates two subnets, named *mySubnetFrontEnd* and *mySubnetBackEnd*:</span></span>

```azurecli
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetFrontEnd \
    --address-prefix 192.168.1.0/24
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

## <a name="create-and-configure-multiple-nics"></a><span data-ttu-id="62889-128">Создание и настройка нескольких сетевых карт</span><span class="sxs-lookup"><span data-stu-id="62889-128">Create and configure multiple NICs</span></span>
<span data-ttu-id="62889-129">Можно прочитать дополнительные сведения о [развертывание нескольких сетевых адаптеров с помощью Azure CLI hello](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), включая сценарии процесс hello циклический перебор toocreate всех сетевых адаптеров hello.</span><span class="sxs-lookup"><span data-stu-id="62889-129">You can read more details about [deploying multiple NICs using hello Azure CLI](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), including scripting hello process of looping through toocreate all hello NICs.</span></span>

<span data-ttu-id="62889-130">Hello следующий пример создает два сетевых адаптера с именем *myNic1* и *myNic2*, с одним сетевым Адаптером подключение tooeach подсети:</span><span class="sxs-lookup"><span data-stu-id="62889-130">hello following example creates two NICs, named *myNic1* and *myNic2*, with one NIC connecting tooeach subnet:</span></span>

```azurecli
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic1 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetFrontEnd
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic2 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetBackEnd
```

<span data-ttu-id="62889-131">Обычно также создать [сетевой группы безопасности](../../virtual-network/virtual-networks-nsg.md) или [подсистемы балансировки нагрузки](../../load-balancer/load-balancer-overview.md) toohelp управлять и распределять трафик между виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="62889-131">Typically you also create a [Network Security Group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) toohelp manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="62889-132">Hello следующий пример создает группу безопасности сети с именем *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="62889-132">hello following example creates a Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="62889-133">Привязать вашей группы безопасности сети toohello сетевых адаптеров с помощью `azure network nic set`.</span><span class="sxs-lookup"><span data-stu-id="62889-133">Bind your NICs toohello Network Security Group using `azure network nic set`.</span></span> <span data-ttu-id="62889-134">Hello следующего примера производится привязка *myNic1* и *myNic2* с *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="62889-134">hello following example binds *myNic1* and *myNic2* with *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic1 \
    --network-security-group-name myNetworkSecurityGroup
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic2 \
    --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-hello-nics"></a><span data-ttu-id="62889-135">Создайте виртуальную Машину и присоединения hello сетевых адаптеров</span><span class="sxs-lookup"><span data-stu-id="62889-135">Create a VM and attach hello NICs</span></span>
<span data-ttu-id="62889-136">При создании виртуальной Машины hello, теперь указать несколько сетевых адаптеров.</span><span class="sxs-lookup"><span data-stu-id="62889-136">When creating hello VM, you now specify multiple NICs.</span></span> <span data-ttu-id="62889-137">Вместо этого с помощью `--nic-name` tooprovide один сетевой Адаптер, вместо этого используйте `--nic-names` и указать список разделенных запятыми сетевых адаптеров.</span><span class="sxs-lookup"><span data-stu-id="62889-137">Rather using `--nic-name` tooprovide a single NIC, instead you use `--nic-names` and provide a comma-separated list of NICs.</span></span> <span data-ttu-id="62889-138">Необходимо также tootake осторожность при выборе hello размер виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="62889-138">You also need tootake care when you select hello VM size.</span></span> <span data-ttu-id="62889-139">Существуют ограничения для hello общее число сетевых адаптеров, вы можете добавить tooa виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="62889-139">There are limits for hello total number of NICs that you can add tooa VM.</span></span> <span data-ttu-id="62889-140">Прочитайте дополнительные сведения о [размерах виртуальных машин Linux](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="62889-140">Read more about [Linux VM sizes](sizes.md).</span></span> <span data-ttu-id="62889-141">Hello следующем примере показано, как toospecify несколько сетевых адаптеров, а затем виртуальной Машины размера, поддерживает использование нескольких сетевых адаптеров (*Standard_DS2_v2*):</span><span class="sxs-lookup"><span data-stu-id="62889-141">hello following example shows how toospecify multiple NICs and then a VM size that supports using multiple NICs (*Standard_DS2_v2*):</span></span>

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location eastus \
    --os-type linux \
    --nic-names myNic1,myNic2 \
    --vm-size Standard_DS2_v2 \
    --storage-account-name mystorageaccount \
    --image-urn UbuntuLTS \
    --admin-username azureuser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub
```

## <a name="create-multiple-nics-using-resource-manager-templates"></a><span data-ttu-id="62889-142">Создание нескольких сетевых карт с помощью шаблонов Resource Manager</span><span class="sxs-lookup"><span data-stu-id="62889-142">Create multiple NICs using Resource Manager templates</span></span>
<span data-ttu-id="62889-143">Шаблоны Azure Resource Manager среду использовать декларативные toodefine файлы JSON.</span><span class="sxs-lookup"><span data-stu-id="62889-143">Azure Resource Manager templates use declarative JSON files toodefine your environment.</span></span> <span data-ttu-id="62889-144">Дополнительные сведения см. в [обзоре Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="62889-144">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="62889-145">Шаблоны диспетчера ресурсов предоставить несколько экземпляров ресурса toocreate образом во время развертывания, таких как создание нескольких сетевых адаптеров.</span><span class="sxs-lookup"><span data-stu-id="62889-145">Resource Manager templates provide a way toocreate multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="62889-146">Вы используете *копирования* toospecify hello число экземпляров toocreate:</span><span class="sxs-lookup"><span data-stu-id="62889-146">You use *copy* toospecify hello number of instances toocreate:</span></span>

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="62889-147">Вы можете прочитать дополнительные сведения о [создании нескольких экземпляров с помощью объекта *copy*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="62889-147">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="62889-148">Можно также использовать `copyIndex()` toothen Добавление номеров tooa имя ресурса, позволяющий toocreate `myNic1`, `myNic2`, т. д. hello ниже показан пример добавления hello значение индекса:</span><span class="sxs-lookup"><span data-stu-id="62889-148">You can also use a `copyIndex()` toothen append a number tooa resource name, which allows you toocreate `myNic1`, `myNic2`, etc. hello following shows an example of appending hello index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="62889-149">Вы можете ознакомиться с полным примером [создания нескольких сетевых карт с помощью шаблонов Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="62889-149">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="62889-150">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="62889-150">Next steps</span></span>
<span data-ttu-id="62889-151">Убедитесь, что tooreview [размеры виртуальных Машин Linux](sizes.md) при попытке toocreating виртуальной Машины с несколькими сетевыми адаптерами.</span><span class="sxs-lookup"><span data-stu-id="62889-151">Make sure tooreview [Linux VM sizes](sizes.md) when trying toocreating a VM with multiple NICs.</span></span> <span data-ttu-id="62889-152">Обратите внимание toohello максимальное количество сетевых адаптеров, размер каждой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="62889-152">Pay attention toohello maximum number of NICs each VM size supports.</span></span> 

<span data-ttu-id="62889-153">Помните, что нельзя добавить дополнительные tooan сетевые адаптеры с существующей виртуальной Машины, при развертывании hello виртуальной Машины необходимо создать все сетевые адаптеры hello.</span><span class="sxs-lookup"><span data-stu-id="62889-153">Remember that you cannot add additional NICs tooan existing VM, you must create all hello NICs when you deploy hello VM.</span></span> <span data-ttu-id="62889-154">Будьте внимательны при планировании вашего развертывания toomake наличие всех необходимых hello сетевые соединения с самого начала hello.</span><span class="sxs-lookup"><span data-stu-id="62889-154">Take care when planning your deployments toomake sure that you have all hello required network connectivity from hello outset.</span></span>

