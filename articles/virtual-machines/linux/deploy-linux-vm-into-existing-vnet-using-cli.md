---
title: "aaaDeploy виртуальных машин Linux в существующей сети с помощью Azure CLI 2.0 | Документы Microsoft"
description: "Узнайте, как toodeploy виртуальной машины Linux в существующей виртуальной сети с помощью hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 0df44b3437002df050db56f3b3899083fb49d803
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli"></a><span data-ttu-id="b40b5-103">Как toodeploy виртуальной машины Linux в существующей виртуальной сети Azure с hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b40b5-103">How toodeploy a Linux virtual machine into an existing Azure Virtual Network with hello Azure CLI</span></span>

<span data-ttu-id="b40b5-104">В этой статье показано, как toouse hello Azure CLI 2.0 toodeploy виртуальной машины (VM) в рамках существующей виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="b40b5-104">This article shows you how toouse hello Azure CLI 2.0 toodeploy a virtual machine (VM) into an existing virtual network.</span></span> <span data-ttu-id="b40b5-105">Существуют следующие требования Hello.</span><span class="sxs-lookup"><span data-stu-id="b40b5-105">hello requirements are:</span></span>

- <span data-ttu-id="b40b5-106">[учетная запись Azure](https://azure.microsoft.com/pricing/free-trial/);</span><span class="sxs-lookup"><span data-stu-id="b40b5-106">[an Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>
- <span data-ttu-id="b40b5-107">[файлы открытого и закрытого ключа SSH](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="b40b5-107">[SSH public and private key files](mac-create-ssh-keys.md)</span></span>

<span data-ttu-id="b40b5-108">Можно также выполнить следующие действия с hello [Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="b40b5-108">You can also perform these steps with hello [Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md).</span></span>


## <a name="quick-commands"></a><span data-ttu-id="b40b5-109">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="b40b5-109">Quick Commands</span></span>
<span data-ttu-id="b40b5-110">Если вам требуется tooquickly выполнения задачи hello, hello в следующем разделе подробно описываются hello команд, которые необходимы.</span><span class="sxs-lookup"><span data-stu-id="b40b5-110">If you need tooquickly accomplish hello task, hello following section details hello  commands needed.</span></span> <span data-ttu-id="b40b5-111">Более подробные сведения и контекста, для каждого шага можно найти hello остальной части документа hello [начиная здесь](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="b40b5-111">More detailed information and context for each step can be found hello rest of hello document, [starting here](#detailed-walkthrough).</span></span>

<span data-ttu-id="b40b5-112">toocreate этой пользовательской среды hello требуется последняя версия [Azure CLI 2.0](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="b40b5-112">toocreate this custom environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="b40b5-113">В hello следующих примерах замените примеры имен параметров собственные значения.</span><span class="sxs-lookup"><span data-stu-id="b40b5-113">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="b40b5-114">Примеры имен параметров: *myResourceGroup*, *myVnet* и *myVM*.</span><span class="sxs-lookup"><span data-stu-id="b40b5-114">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

<span data-ttu-id="b40b5-115">**Предварительные требования:** группа ресурсов Azure, виртуальная сеть и подсеть, группа безопасности сети с разрешенными входящими подключениями SSH и виртуальная сетевая карта.</span><span class="sxs-lookup"><span data-stu-id="b40b5-115">**Pre-requirements:** Azure resource group, virtual network and subnet, network security group with SSH inbound, and a virtual network interface card.</span></span>

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="b40b5-116">Развертывание hello виртуальных Машин в инфраструктуре виртуальной сети hello</span><span class="sxs-lookup"><span data-stu-id="b40b5-116">Deploy hello VM into hello virtual network infrastructure</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="b40b5-117">Подробное пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="b40b5-117">Detailed walkthrough</span></span>

<span data-ttu-id="b40b5-118">Ресурсы Azure, такие как виртуальные сети и группы безопасности сети, должны быть статическими. Они должны долго храниться и редко развертываться.</span><span class="sxs-lookup"><span data-stu-id="b40b5-118">Azure assets like virtual networks and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="b40b5-119">После развертывания виртуальной сети, он может быть использован в новые развертывания без инфраструктуры toohello любой негативно влияет на.</span><span class="sxs-lookup"><span data-stu-id="b40b5-119">Once a virtual network has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="b40b5-120">Подумайте о виртуальной сети как сетевой коммутатор традиционных оборудования - не потребовалось бы tooconfigure нового оборудования переключиться с каждым развертыванием.</span><span class="sxs-lookup"><span data-stu-id="b40b5-120">Think about a virtual network as being a traditional hardware network switch - you would not need tooconfigure a brand new hardware switch with each deployment.</span></span> <span data-ttu-id="b40b5-121">С правильно настроенной виртуальной сети, вы можете продолжить toodeploy новые виртуальные машины в виртуальной сети с минимальными снова и снова при его наличии, изменения требуются протяжении hello hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="b40b5-121">With a correctly configured virtual network, you can continue toodeploy new VMs into that virtual network over and over with few, if any, changes required over hello life of hello virtual network.</span></span>

<span data-ttu-id="b40b5-122">toocreate этой пользовательской среды hello требуется последняя версия [Azure CLI 2.0](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="b40b5-122">toocreate this custom environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="b40b5-123">В hello следующих примерах замените примеры имен параметров собственные значения.</span><span class="sxs-lookup"><span data-stu-id="b40b5-123">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="b40b5-124">Примеры имен параметров: *myResourceGroup*, *myVnet* и *myVM*.</span><span class="sxs-lookup"><span data-stu-id="b40b5-124">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="b40b5-125">Создать группу ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="b40b5-125">Create hello resource group</span></span>

<span data-ttu-id="b40b5-126">Во-первых создайте tooorganize группы ресурсов Azure все данные, создаваемые в данном пошаговом руководстве.</span><span class="sxs-lookup"><span data-stu-id="b40b5-126">First, create an Azure resource group tooorganize everything you create in this walkthrough.</span></span> <span data-ttu-id="b40b5-127">Дополнительные сведения о группах ресурсов см. в статье [Общие сведения об Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b40b5-127">For more information on resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="b40b5-128">Создать группу ресурсов hello с [Создание группы az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="b40b5-128">Create hello resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="b40b5-129">Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение:</span><span class="sxs-lookup"><span data-stu-id="b40b5-129">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

## <a name="create-hello-virtual-network"></a><span data-ttu-id="b40b5-130">Создайте виртуальную сеть hello</span><span class="sxs-lookup"><span data-stu-id="b40b5-130">Create hello virtual network</span></span>

<span data-ttu-id="b40b5-131">Позволяет построения виртуальных машин в виртуальной сети Azure toolaunch hello.</span><span class="sxs-lookup"><span data-stu-id="b40b5-131">Lets build an Azure virtual network toolaunch hello VMs into.</span></span> <span data-ttu-id="b40b5-132">Дополнительные сведения о виртуальных сетях см. в разделе [Создание виртуальной сети с помощью Azure CLI hello](../../virtual-network/virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b40b5-132">For more information on virtual networks, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md).</span></span> <span data-ttu-id="b40b5-133">Создайте виртуальную сеть hello с [создания az сети vnet](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="b40b5-133">Create hello virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="b40b5-134">Hello следующий пример создает виртуальную сеть с именем *myVnet* и подсеть с именем *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="b40b5-134">hello following example creates a virtual network named *myVnet* and subnet named *mySubnet*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefix 10.10.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 10.10.1.0/24
```

## <a name="create-hello-network-security-group"></a><span data-ttu-id="b40b5-135">Создание группы безопасности сети hello</span><span class="sxs-lookup"><span data-stu-id="b40b5-135">Create hello network security group</span></span>

<span data-ttu-id="b40b5-136">Эквивалентный tooa брандмауэра на уровне сети hello являются группы безопасности сети Azure.</span><span class="sxs-lookup"><span data-stu-id="b40b5-136">Azure network security groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="b40b5-137">Дополнительные сведения о группах сетевой безопасности см. в разделе [Сопоставление групп безопасности сети toocreate в hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b40b5-137">For more information on network security groups, see [How toocreate network security groups in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span></span> <span data-ttu-id="b40b5-138">Создание группы безопасности сети hello с [создать az сети nsg](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="b40b5-138">Create hello network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="b40b5-139">Hello следующий пример создает группу безопасности сети с именем *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="b40b5-139">hello following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="b40b5-140">Добавление правила, разрешающего входящий трафик по протоколу SSH</span><span class="sxs-lookup"><span data-stu-id="b40b5-140">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="b40b5-141">Hello виртуальной Машины требуется доступ из hello необходима Интернета, поэтому правило, разрешающее трафик toobe входящий порт 22 передаются через tooport сети hello 22 hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="b40b5-141">hello VM needs access from hello internet, so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello VM is needed.</span></span> <span data-ttu-id="b40b5-142">Добавьте правило входящего трафика для hello сетевой группы безопасности с [создать правило nsg сети az](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="b40b5-142">Add an inbound rule for hello network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="b40b5-143">Hello следующий код создает правило с именем *myNetworkSecurityGroupRuleSSH*:</span><span class="sxs-lookup"><span data-stu-id="b40b5-143">hello following example creates a rule named *myNetworkSecurityGroupRuleSSH*:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --priority 1000 \
    --protocol tcp \
    --destination-port-range 22 \
```

## <a name="attach-hello-subnet-toohello-network-security-group"></a><span data-ttu-id="b40b5-144">Присоединение группы безопасности сети toohello подсети hello</span><span class="sxs-lookup"><span data-stu-id="b40b5-144">Attach hello subnet toohello network security group</span></span>

<span data-ttu-id="b40b5-145">правила группы сетевой безопасности Hello может быть применен tooa подсети или определенного виртуального сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="b40b5-145">hello network security group rules can be applied tooa subnet or a specific virtual network interface.</span></span> <span data-ttu-id="b40b5-146">Позволяет присоединить подсеть tooour группы безопасности сети hello.</span><span class="sxs-lookup"><span data-stu-id="b40b5-146">Lets attach hello network security group tooour subnet.</span></span> <span data-ttu-id="b40b5-147">Присоединение к подсети toohello сетевой группы безопасности с [обновления подсети виртуальной сети сети az](/cli/azure/network/vnet/subnet#update):</span><span class="sxs-lookup"><span data-stu-id="b40b5-147">Attach your subnet toohello network security group with [az network vnet subnet update](/cli/azure/network/vnet/subnet#update):</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="add-a-virtual-network-interface-card-toohello-subnet"></a><span data-ttu-id="b40b5-148">Добавить подсеть toohello карты виртуального сетевого интерфейса</span><span class="sxs-lookup"><span data-stu-id="b40b5-148">Add a virtual network interface card toohello subnet</span></span>

<span data-ttu-id="b40b5-149">Виртуальных сетевых картах (VNics) являются важной, так как можно повторно использовать их, подключив их toodifferent виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="b40b5-149">Virtual network interface cards (VNics) are important as you can reuse them by connecting them toodifferent VMs.</span></span> <span data-ttu-id="b40b5-150">Повторное использование позволяет tookeep hello виртуального сетевого адаптера как статический ресурс, а hello виртуальные машины могут быть как временными.</span><span class="sxs-lookup"><span data-stu-id="b40b5-150">This reuse allows you tookeep hello VNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="b40b5-151">Создание виртуального сетевого адаптера и связать его с hello подсети с [Создание сетевого адаптера сети az](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="b40b5-151">Create a VNic and associate it with hello subnet with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="b40b5-152">Hello следующем примере создается виртуальный сетевой адаптер с именем *myNic*:</span><span class="sxs-lookup"><span data-stu-id="b40b5-152">hello following example creates a VNic named *myNic*:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="b40b5-153">Развертывание hello виртуальных Машин в инфраструктуре виртуальной сети hello</span><span class="sxs-lookup"><span data-stu-id="b40b5-153">Deploy hello VM into hello virtual network infrastructure</span></span>

<span data-ttu-id="b40b5-154">Теперь у вас есть виртуальная сеть и подсеть и подсеть hello tooprotect группы безопасности сети, блокируя весь входящий трафик, за исключением порт 22 для SSH.</span><span class="sxs-lookup"><span data-stu-id="b40b5-154">You now have a virtual network and subnet, and a network security group tooprotect hello subnet by blocking all inbound traffic except port 22 for SSH.</span></span> <span data-ttu-id="b40b5-155">Теперь может быть развернут Hello виртуальной Машины внутри этой существующей сетевой инфраструктуре.</span><span class="sxs-lookup"><span data-stu-id="b40b5-155">hello VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="b40b5-156">Создайте виртуальную машину с помощью команды [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="b40b5-156">Create your VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="b40b5-157">Дополнительные сведения о hello флаги toouse с toodeploy hello Azure CLI 2.0 завершения виртуальной Машины, см. в разделе [создать полную среду Linux с помощью Azure CLI hello](create-cli-complete.md).</span><span class="sxs-lookup"><span data-stu-id="b40b5-157">For more information on hello flags toouse with hello Azure CLI 2.0 toodeploy a complete VM, see [Create a complete Linux environment by using hello Azure CLI](create-cli-complete.md).</span></span>

<span data-ttu-id="b40b5-158">Следующий пример Hello создает виртуальную Машину с помощью управляемых дисков Azure.</span><span class="sxs-lookup"><span data-stu-id="b40b5-158">hello following example creates a VM using Azure Managed Disks.</span></span> <span data-ttu-id="b40b5-159">Эти диски обрабатываются hello платформы Azure и не требуют toostore любые предварительные и место их.</span><span class="sxs-lookup"><span data-stu-id="b40b5-159">These disks are handled by hello Azure platform and do not require any preparation or location toostore them.</span></span> <span data-ttu-id="b40b5-160">Дополнительные сведения об управляемых дисках Azure см. в [этой статье](../../storage/storage-managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b40b5-160">For more information about managed disks, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md).</span></span> <span data-ttu-id="b40b5-161">При желании toouse неуправляемого дисков см. Примечание дополнительных hello ниже.</span><span class="sxs-lookup"><span data-stu-id="b40b5-161">If you wish toouse unmanaged disks, see hello additional note below.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

<span data-ttu-id="b40b5-162">Если вы используете управляемые диски, пропустите этот шаг.</span><span class="sxs-lookup"><span data-stu-id="b40b5-162">If you use managed disks, skip this step.</span></span> <span data-ttu-id="b40b5-163">При желании toouse неуправляемого дисков требуется hello tooadd следующие дополнительные параметры toohello продолжением команда toocreate неуправляемого дисков в hello учетной записи хранилища с именем `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="b40b5-163">If you wish toouse unmanaged disks, you need tooadd hello following additional parameters toohello proceeding command toocreate unmanaged disks in hello storage account named `mystorageaccount`:</span></span> 

```azurecli
    --use-unmanaged-disk \
    --storage-account mystorageaccount
```

<span data-ttu-id="b40b5-164">С помощью hello CLI флаги toocall существующие ресурсы, вы указываете hello Azure toodeploy виртуальных Машин в существующей сети hello.</span><span class="sxs-lookup"><span data-stu-id="b40b5-164">By using hello CLI flags toocall out existing resources, you instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="b40b5-165">После развертывания виртуальную сеть и подсеть можно оставить в качестве статических или постоянных ресурсов в регионе Azure.</span><span class="sxs-lookup"><span data-stu-id="b40b5-165">Once a virtual network and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span> <span data-ttu-id="b40b5-166">В этом примере не не создать и назначить открытый IP адрес toohello виртуального сетевого адаптера, поэтому эту виртуальную Машину не доступен из Интернета через Интернет hello.</span><span class="sxs-lookup"><span data-stu-id="b40b5-166">In this example, you did not create and assign a public IP address toohello VNic, so this VM is not publicly accessible over hello Internet.</span></span> <span data-ttu-id="b40b5-167">Дополнительные сведения см. в разделе [Создание ВМ с статический общедоступный IP-адрес с помощью Azure CLI hello](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b40b5-167">For more information, see [Create a VM with a static public IP using hello Azure CLI](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b40b5-168">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b40b5-168">Next steps</span></span>
<span data-ttu-id="b40b5-169">Дополнительные сведения о способах toocreate виртуальных машин в Azure см. в разделе hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="b40b5-169">For more information about ways toocreate virtual machines in Azure, see hello following resources:</span></span>

* [<span data-ttu-id="b40b5-170">Использовать toocreate шаблона диспетчера ресурсов Azure конкретного развертывания</span><span class="sxs-lookup"><span data-stu-id="b40b5-170">Use an Azure Resource Manager template toocreate a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="b40b5-171">Создание полной среды Linux с помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="b40b5-171">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="b40b5-172">Создание виртуальной машины Linux с помощью шаблона Azure</span><span class="sxs-lookup"><span data-stu-id="b40b5-172">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
