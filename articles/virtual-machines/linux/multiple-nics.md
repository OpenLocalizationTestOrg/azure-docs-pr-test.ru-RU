---
title: "aaaCreate виртуальной Машины Linux в Azure с несколькими сетевыми адаптерами | Документы Microsoft"
description: "Узнайте, как toocreate ВМ Linux с несколькими сетевыми адаптерами присоединенного tooit с помощью шаблонов hello Azure CLI 2.0 или диспетчер ресурсов."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 5d2d04d0-fc62-45fa-88b1-61808a2bc691
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 2723405914777a5dce4354d4f5d8413e357f58e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-in-azure-with-multiple-network-interface-cards"></a><span data-ttu-id="4ef32-103">Как toocreate виртуальной машины Linux в Azure с несколькими сетевыми интерфейсные карты</span><span class="sxs-lookup"><span data-stu-id="4ef32-103">How toocreate a Linux virtual machine in Azure with multiple network interface cards</span></span>
<span data-ttu-id="4ef32-104">Можно создать виртуальную машину (ВМ) в Azure, которая имеет несколько tooit интерфейсов (NIC), подключенных виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="4ef32-104">You can create a virtual machine (VM) in Azure that has multiple virtual network interfaces (NICs) attached tooit.</span></span> <span data-ttu-id="4ef32-105">Типичный сценарий состоит в разных подсетях toohave для внешнего и внутреннего интерфейса подключения или сеть, выделенная tooa наблюдения или решение для резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="4ef32-105">A common scenario is toohave different subnets for front-end and back-end connectivity, or a network dedicated tooa monitoring or backup solution.</span></span> <span data-ttu-id="4ef32-106">В этой статье описаны процедуры tooit присоединенного toocreate виртуальной Машины с несколькими сетевыми адаптерами и tooadd или удаление сетевых адаптеров в существующей виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="4ef32-106">This article details how toocreate a VM with multiple NICs attached tooit and how tooadd or remove NICs from an existing VM.</span></span> <span data-ttu-id="4ef32-107">Подробные сведения, включая как toocreate несколько сетевых адаптеров в собственных Bash скрипты, Дополнительные сведения о [развертывание виртуальных машин multi-NIC](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="4ef32-107">For detailed information, including how toocreate multiple NICs within your own Bash scripts, read more about [deploying multi-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md).</span></span> <span data-ttu-id="4ef32-108">Различные [размеры виртуальных машин](sizes.md) поддерживают разное число сетевых карт, так что выбирайте соответствующий размер виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="4ef32-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="4ef32-109">В этой статье указаны как toocreate a виртуальной Машины с несколькими сетевыми адаптерами с hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="4ef32-109">This article details how toocreate a VM with multiple NICs with hello Azure CLI 2.0.</span></span> <span data-ttu-id="4ef32-110">Можно также выполнить следующие действия с hello [Azure CLI 1.0](multiple-nics-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="4ef32-110">You can also perform these steps with hello [Azure CLI 1.0](multiple-nics-nodejs.md).</span></span>


## <a name="create-supporting-resources"></a><span data-ttu-id="4ef32-111">Создание вспомогательных ресурсов</span><span class="sxs-lookup"><span data-stu-id="4ef32-111">Create supporting resources</span></span>
<span data-ttu-id="4ef32-112">Последняя версия hello установки [Azure CLI 2.0](/cli/azure/install-az-cli2) и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="4ef32-112">Install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="4ef32-113">В hello следующих примерах замените примеры имен параметров собственные значения.</span><span class="sxs-lookup"><span data-stu-id="4ef32-113">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="4ef32-114">Примеры имен параметров: *myResourceGroup*, *mystorageaccount* и *myVM*.</span><span class="sxs-lookup"><span data-stu-id="4ef32-114">Example parameter names included *myResourceGroup*, *mystorageaccount*, and *myVM*.</span></span>

<span data-ttu-id="4ef32-115">Сначала создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="4ef32-115">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="4ef32-116">Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение:</span><span class="sxs-lookup"><span data-stu-id="4ef32-116">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="4ef32-117">Создайте виртуальную сеть hello с [создания az сети vnet](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="4ef32-117">Create hello virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="4ef32-118">Hello следующий пример создает виртуальную сеть с именем *myVnet* и подсеть с именем *mySubnetFrontEnd*:</span><span class="sxs-lookup"><span data-stu-id="4ef32-118">hello following example creates a virtual network named *myVnet* and subnet named *mySubnetFrontEnd*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnetFrontEnd \
    --subnet-prefix 192.168.1.0/24
```

<span data-ttu-id="4ef32-119">Создайте подсеть для трафика hello серверной части с [создать подсеть виртуальной сети az сети](/cli/azure/network/vnet/subnet#create).</span><span class="sxs-lookup"><span data-stu-id="4ef32-119">Create a subnet for hello back-end traffic with [az network vnet subnet create](/cli/azure/network/vnet/subnet#create).</span></span> <span data-ttu-id="4ef32-120">Hello следующий пример создает подсеть с именем *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="4ef32-120">hello following example creates a subnet named *mySubnetBackEnd*:</span></span>

```azurecli
az network vnet subnet create \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

<span data-ttu-id="4ef32-121">Создайте группу безопасности сети с помощью команды [az network nsg create](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="4ef32-121">Create a network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="4ef32-122">Hello следующий пример создает группу безопасности сети с именем *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="4ef32-122">hello following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="create-and-configure-multiple-nics"></a><span data-ttu-id="4ef32-123">Создание и настройка нескольких сетевых карт</span><span class="sxs-lookup"><span data-stu-id="4ef32-123">Create and configure multiple NICs</span></span>
<span data-ttu-id="4ef32-124">Создайте две сетевых карты с помощью команды [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="4ef32-124">Create two NICs with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="4ef32-125">Hello следующий пример создает два сетевых адаптера с именем *myNic1* и *myNic2*, подключенной группы безопасности сети hello с одним сетевым Адаптером подключение tooeach подсети:</span><span class="sxs-lookup"><span data-stu-id="4ef32-125">hello following example creates two NICs, named *myNic1* and *myNic2*, connected hello network security group, with one NIC connecting tooeach subnet:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic1 \
    --vnet-name myVnet \
    --subnet mySubnetFrontEnd \
    --network-security-group myNetworkSecurityGroup
az network nic create \
    --resource-group myResourceGroup \
    --name myNic2 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-hello-nics"></a><span data-ttu-id="4ef32-126">Создайте виртуальную Машину и присоединения hello сетевых адаптеров</span><span class="sxs-lookup"><span data-stu-id="4ef32-126">Create a VM and attach hello NICs</span></span>
<span data-ttu-id="4ef32-127">При создании hello виртуальных Машин, укажите hello сетевые адаптеры, созданные с помощью `--nics`.</span><span class="sxs-lookup"><span data-stu-id="4ef32-127">When you create hello VM, specify hello NICs you created with `--nics`.</span></span> <span data-ttu-id="4ef32-128">Необходимо также tootake осторожность при выборе hello размер виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="4ef32-128">You also need tootake care when you select hello VM size.</span></span> <span data-ttu-id="4ef32-129">Существуют ограничения для hello общее число сетевых адаптеров, вы можете добавить tooa виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="4ef32-129">There are limits for hello total number of NICs that you can add tooa VM.</span></span> <span data-ttu-id="4ef32-130">Прочитайте дополнительные сведения о [размерах виртуальных машин Linux](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="4ef32-130">Read more about [Linux VM sizes](sizes.md).</span></span> 

<span data-ttu-id="4ef32-131">Создайте виртуальную машину с помощью команды [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="4ef32-131">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="4ef32-132">Hello следующий пример создает Виртуальную машину с именем *myVM*:</span><span class="sxs-lookup"><span data-stu-id="4ef32-132">hello following example creates a VM named *myVM*:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --size Standard_DS3_v2 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic1 myNic2
```

## <a name="add-a-nic-tooa-vm"></a><span data-ttu-id="4ef32-133">Добавить tooa сетевого Адаптера виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="4ef32-133">Add a NIC tooa VM</span></span>
<span data-ttu-id="4ef32-134">Hello предыдущие шаги создания виртуальной Машины с несколькими сетевыми адаптерами.</span><span class="sxs-lookup"><span data-stu-id="4ef32-134">hello previous steps created a VM with multiple NICs.</span></span> <span data-ttu-id="4ef32-135">Можно также добавить существующие ВМ в Azure CLI 2.0 hello tooan сетевых адаптеров.</span><span class="sxs-lookup"><span data-stu-id="4ef32-135">You can also add NICs tooan existing VM with hello Azure CLI 2.0.</span></span> 

<span data-ttu-id="4ef32-136">Создайте другую сетевую карту с помощью команды [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="4ef32-136">Create another NIC with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="4ef32-137">Hello следующий пример создает сетевой Адаптер с именем *myNic3* подключен toohello внутренней подсети и сетевой группы безопасности, созданные в предыдущих шагах hello:</span><span class="sxs-lookup"><span data-stu-id="4ef32-137">hello following example creates a NIC named *myNic3* connected toohello back-end subnet and network security group created in hello previous steps:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic3 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="4ef32-138">tooadd tooan Сетевых существующую виртуальную Машину сначала освободить hello виртуальной Машины с [deallocate az ВМ](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="4ef32-138">tooadd a NIC tooan existing VM, first deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="4ef32-139">Hello следующий пример отменяет выделение hello виртуальной Машины с именем *myVM*:</span><span class="sxs-lookup"><span data-stu-id="4ef32-139">hello following example deallocates hello VM named *myVM*:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="4ef32-140">Добавить hello сетевого Адаптера с [добавить сетевой адаптер виртуальной машины az](/cli/azure/vm/nic#add).</span><span class="sxs-lookup"><span data-stu-id="4ef32-140">Add hello NIC with [az vm nic add](/cli/azure/vm/nic#add).</span></span> <span data-ttu-id="4ef32-141">Hello следующий пример добавляет *myNic3* слишком*myVM*:</span><span class="sxs-lookup"><span data-stu-id="4ef32-141">hello following example adds *myNic3* too*myVM*:</span></span>

```azurecli
az vm nic add \
    --resource-group myResourceGroup \
    --vm-name myVM \
    --nics myNic3
```

<span data-ttu-id="4ef32-142">Запуск hello виртуальной Машины с [запуска виртуальной машины az](/cli/azure/vm#start):</span><span class="sxs-lookup"><span data-stu-id="4ef32-142">Start hello VM with [az vm start](/cli/azure/vm#start):</span></span>

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```

## <a name="remove-a-nic-from-a-vm"></a><span data-ttu-id="4ef32-143">Удаление сетевой карты с виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="4ef32-143">Remove a NIC from a VM</span></span>
<span data-ttu-id="4ef32-144">tooremove сетевой Адаптер из существующей виртуальной Машины, сначала освободить hello виртуальной Машины с [ВМ az deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="4ef32-144">tooremove a NIC from an existing VM, first deallocate hello VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="4ef32-145">Hello следующий пример отменяет выделение hello виртуальной Машины с именем *myVM*:</span><span class="sxs-lookup"><span data-stu-id="4ef32-145">hello following example deallocates hello VM named *myVM*:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="4ef32-146">Удалите hello сетевого Адаптера с [удалите сетевой адаптер виртуальной машины az](/cli/azure/vm/nic#remove).</span><span class="sxs-lookup"><span data-stu-id="4ef32-146">Remove hello NIC with [az vm nic remove](/cli/azure/vm/nic#remove).</span></span> <span data-ttu-id="4ef32-147">Hello следующий пример удаляет *myNic3* из *myVM*:</span><span class="sxs-lookup"><span data-stu-id="4ef32-147">hello following example removes *myNic3* from *myVM*:</span></span>

```azurecli
az vm nic remove \
    --resource-group myResourceGroup \
    --vm-name myVM 
    --nics myNic3
```

<span data-ttu-id="4ef32-148">Запуск hello виртуальной Машины с [запуска виртуальной машины az](/cli/azure/vm#start):</span><span class="sxs-lookup"><span data-stu-id="4ef32-148">Start hello VM with [az vm start](/cli/azure/vm#start):</span></span>

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```


## <a name="create-multiple-nics-using-resource-manager-templates"></a><span data-ttu-id="4ef32-149">Создание нескольких сетевых карт с помощью шаблонов Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4ef32-149">Create multiple NICs using Resource Manager templates</span></span>
<span data-ttu-id="4ef32-150">Шаблоны Azure Resource Manager среду использовать декларативные toodefine файлы JSON.</span><span class="sxs-lookup"><span data-stu-id="4ef32-150">Azure Resource Manager templates use declarative JSON files toodefine your environment.</span></span> <span data-ttu-id="4ef32-151">Дополнительные сведения см. в [обзоре Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4ef32-151">You can read an [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="4ef32-152">Шаблоны диспетчера ресурсов предоставить несколько экземпляров ресурса toocreate образом во время развертывания, таких как создание нескольких сетевых адаптеров.</span><span class="sxs-lookup"><span data-stu-id="4ef32-152">Resource Manager templates provide a way toocreate multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="4ef32-153">Вы используете *копирования* toospecify hello число экземпляров toocreate:</span><span class="sxs-lookup"><span data-stu-id="4ef32-153">You use *copy* toospecify hello number of instances toocreate:</span></span>

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="4ef32-154">Вы можете прочитать дополнительные сведения о [создании нескольких экземпляров с помощью объекта *copy*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="4ef32-154">Read more about [creating multiple instances using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="4ef32-155">Можно также использовать `copyIndex()` toothen Добавление номеров tooa имя ресурса, позволяющий toocreate `myNic1`, `myNic2`, т. д. hello ниже показан пример добавления hello значение индекса:</span><span class="sxs-lookup"><span data-stu-id="4ef32-155">You can also use a `copyIndex()` toothen append a number tooa resource name, which allows you toocreate `myNic1`, `myNic2`, etc. hello following shows an example of appending hello index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="4ef32-156">Вы можете ознакомиться с полным примером [создания нескольких сетевых карт с помощью шаблонов Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="4ef32-156">You can read a complete example of [creating multiple NICs using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ef32-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4ef32-157">Next steps</span></span>
<span data-ttu-id="4ef32-158">Просмотрите [размеры виртуальных Машин Linux](sizes.md) при попытке toocreating виртуальной Машины с несколькими сетевыми адаптерами.</span><span class="sxs-lookup"><span data-stu-id="4ef32-158">Review [Linux VM sizes](sizes.md) when trying toocreating a VM with multiple NICs.</span></span> <span data-ttu-id="4ef32-159">Обратите внимание toohello максимальное количество сетевых адаптеров, размер каждой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="4ef32-159">Pay attention toohello maximum number of NICs each VM size supports.</span></span> 
