---
title: "aaaDeploy виртуальных машин Linux в существующей сети с помощью Azure CLI 1.0 | Документы Microsoft"
description: "Как toodeploy виртуальной Машины Linux в существующей виртуальной сети с помощью hello Azure CLI 1.0"
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
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: e660f1563d386efc7788bd236f8b067145ea09bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli-10"></a><span data-ttu-id="76c3e-103">Как toodeploy виртуальной машины Linux в существующей виртуальной сети Azure с hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="76c3e-103">How toodeploy a Linux virtual machine into an existing Azure Virtual Network with hello Azure CLI 1.0</span></span>

<span data-ttu-id="76c3e-104">В этой статье показано, как toodeploy toouse Azure CLI 1.0 виртуальной машины (VM) в существующей виртуальной сети (VNet).</span><span class="sxs-lookup"><span data-stu-id="76c3e-104">This article shows you how toouse Azure CLI 1.0 toodeploy a virtual machine (VM) into an existing Virtual Network (VNet).</span></span> <span data-ttu-id="76c3e-105">Существуют следующие требования Hello.</span><span class="sxs-lookup"><span data-stu-id="76c3e-105">hello requirements are:</span></span>

- <span data-ttu-id="76c3e-106">[учетная запись Azure](https://azure.microsoft.com/pricing/free-trial/);</span><span class="sxs-lookup"><span data-stu-id="76c3e-106">[an Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>
- <span data-ttu-id="76c3e-107">[файлы открытого и закрытого ключа SSH](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="76c3e-107">[SSH public and private key files](mac-create-ssh-keys.md)</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="76c3e-108">Задача hello toocomplete версии CLI</span><span class="sxs-lookup"><span data-stu-id="76c3e-108">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="76c3e-109">Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.</span><span class="sxs-lookup"><span data-stu-id="76c3e-109">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="76c3e-110">[Azure CLI 1.0](#quick-commands) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)</span><span class="sxs-lookup"><span data-stu-id="76c3e-110">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="76c3e-111">[Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) -нашей нового поколения CLI для модели развертывания hello ресурсов управления</span><span class="sxs-lookup"><span data-stu-id="76c3e-111">[Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="76c3e-112">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="76c3e-112">Quick Commands</span></span>

<span data-ttu-id="76c3e-113">Если вам требуется tooquickly выполнения задачи hello, hello в следующем разделе подробно описываются hello команд, которые необходимы.</span><span class="sxs-lookup"><span data-stu-id="76c3e-113">If you need tooquickly accomplish hello task, hello following section details hello commands needed.</span></span> <span data-ttu-id="76c3e-114">Более подробные сведения и контекста, для каждого шага можно найти hello остальной части документа hello [начиная здесь](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="76c3e-114">More detailed information and context for each step can be found hello rest of hello document, [starting here](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).</span></span>

<span data-ttu-id="76c3e-115">Необходимые компоненты: группа ресурсов, виртуальная сеть, группа безопасности сети с входящим трафиком SSH, подсеть.</span><span class="sxs-lookup"><span data-stu-id="76c3e-115">Pre-requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span></span> <span data-ttu-id="76c3e-116">Замените все примеры параметров своими параметрами.</span><span class="sxs-lookup"><span data-stu-id="76c3e-116">Replace any examples with your own settings.</span></span>

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="76c3e-117">Развертывание hello виртуальных Машин в инфраструктуре виртуальной сети hello</span><span class="sxs-lookup"><span data-stu-id="76c3e-117">Deploy hello VM into hello virtual network infrastructure</span></span>

```azurecli
azure vm create myVM \
    -g myResourceGroup \
    -l eastus \
    -y linux \
    -Q Debian \
    -o mystorageaccount \
    -u myAdminUser \
    -M ~/.ssh/id_rsa.pub \
    -n myVM \
    -F myVNet \
    -j mySubnet \
    -N myVNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="76c3e-118">Подробное пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="76c3e-118">Detailed walkthrough</span></span>

<span data-ttu-id="76c3e-119">Активов Azure, такие как hello виртуальных сетей и группы безопасности сети должен быть статическим и долго ресурсы, которые развертываются редко.</span><span class="sxs-lookup"><span data-stu-id="76c3e-119">Azure assets like hello VNets and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="76c3e-120">После развертывания виртуальной сети, он может быть использован в новые развертывания без инфраструктуры toohello любой негативно влияет на.</span><span class="sxs-lookup"><span data-stu-id="76c3e-120">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="76c3e-121">Представьте виртуальную сеть, как сетевой коммутатор в парадигме традиционного оборудования.</span><span class="sxs-lookup"><span data-stu-id="76c3e-121">Think about a VNet as being a traditional hardware network switch.</span></span> <span data-ttu-id="76c3e-122">Вы не должны были tooconfigure нового оборудования переключиться с каждым развертыванием.</span><span class="sxs-lookup"><span data-stu-id="76c3e-122">You would not need tooconfigure a brand new hardware switch with each deployment.</span></span> <span data-ttu-id="76c3e-123">С правильно настроенной виртуальной сети можно будет продолжить toodeploy новых серверов в этой виртуальной сети и снова несколько, если таковые имеются, изменения, необходимые протяжении hello hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="76c3e-123">With a correctly configured VNet, you can continue toodeploy new servers into that VNet over and over with few, if any, changes required over hello life of hello VNet.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="76c3e-124">Создать группу ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="76c3e-124">Create hello resource group</span></span>

<span data-ttu-id="76c3e-125">Сначала необходимо создаете группы ресурсов tooorganize все данные, создаваемые в данном пошаговом руководстве.</span><span class="sxs-lookup"><span data-stu-id="76c3e-125">First, create a resource group tooorganize everything you create in this walkthrough.</span></span> <span data-ttu-id="76c3e-126">Дополнительные сведения о группах ресурсов см. в статье [Общие сведения о диспетчере ресурсов Azure](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="76c3e-126">For more information about resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md)</span></span>

```azurecli
azure group create myResourceGroup --location eastus
```

## <a name="create-hello-vnet"></a><span data-ttu-id="76c3e-127">Создать hello виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="76c3e-127">Create hello VNet</span></span>

<span data-ttu-id="76c3e-128">Hello первым шагом является toobuild виртуальных машин в hello toolaunch виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="76c3e-128">hello first step is toobuild a VNet toolaunch hello VMs into.</span></span> <span data-ttu-id="76c3e-129">Hello виртуальная сеть содержит одну подсеть для этого пошагового руководства.</span><span class="sxs-lookup"><span data-stu-id="76c3e-129">hello VNet contains one subnet for this walkthrough.</span></span> <span data-ttu-id="76c3e-130">Дополнительные сведения о виртуальных сетях Azure см. в разделе [Создание виртуальной сети с помощью hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)</span><span class="sxs-lookup"><span data-stu-id="76c3e-130">For more information on Azure VNets, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)</span></span>

```azurecli
azure network vnet create myVNet \
    --resource-group myResourceGroup \
    --address-prefixes 10.10.0.0/24 \
    --location eastus
```

## <a name="create-hello-network-security-group"></a><span data-ttu-id="76c3e-131">Создание группы безопасности сети hello</span><span class="sxs-lookup"><span data-stu-id="76c3e-131">Create hello network security group</span></span>

<span data-ttu-id="76c3e-132">подсети Hello построена за существующей сетевой группы безопасности таким образом построить hello сетевой группы безопасности перед hello подсети.</span><span class="sxs-lookup"><span data-stu-id="76c3e-132">hello subnet is built behind an existing network security group so build hello network security group before hello subnet.</span></span> <span data-ttu-id="76c3e-133">Эквивалентный tooa брандмауэра на уровне сети hello являются группы безопасности сети Azure.</span><span class="sxs-lookup"><span data-stu-id="76c3e-133">Azure network security groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="76c3e-134">Дополнительные сведения о группах безопасности сети Azure см. в разделе [Сопоставление групп безопасности сети toocreate в hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)</span><span class="sxs-lookup"><span data-stu-id="76c3e-134">For more information on Azure network security groups, see [How toocreate network security groups in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)</span></span>

```azurecli
azure network nsg create myNetworkSecurityGroup \
    --resource-group myResourceGroup \
    --location eastus
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="76c3e-135">Добавление правила, разрешающего входящий трафик по протоколу SSH</span><span class="sxs-lookup"><span data-stu-id="76c3e-135">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="76c3e-136">Hello виртуальной Машины требуется доступ из hello необходима Интернета, правило, разрешающее трафик toobe входящий порт 22 передаются через tooport сети hello 22 hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="76c3e-136">hello VM needs access from hello internet so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello VM is needed.</span></span>

```azurecli
azure network nsg rule create inboundSSH \
    --resource-group myResourceGroup \
    --nsg-name myNSG \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix Internet \
    --source-port-range 22 \
    --destination-address-prefix 10.10.0.0/24 \
    --destination-port-range 22
```

## <a name="add-a-subnet-toohello-vnet"></a><span data-ttu-id="76c3e-137">Добавить toohello подсети виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="76c3e-137">Add a subnet toohello VNet</span></span>

<span data-ttu-id="76c3e-138">Виртуальные машины в виртуальной сети hello должна находиться в подсети.</span><span class="sxs-lookup"><span data-stu-id="76c3e-138">VMs within hello VNet must be located in a subnet.</span></span> <span data-ttu-id="76c3e-139">Каждая виртуальная сеть может содержать несколько подсетей.</span><span class="sxs-lookup"><span data-stu-id="76c3e-139">Each VNet can have multiple subnets.</span></span> <span data-ttu-id="76c3e-140">Создать подсеть hello и связать с группой безопасности сети hello.</span><span class="sxs-lookup"><span data-stu-id="76c3e-140">Create hello subnet and associate with hello network security group.</span></span>

```azurecli
azure network vnet subnet create mySubNet \
    --resource-group myResourceGroup \
    --vnet-name myVNet \
    --address-prefix 10.10.0.0/26 \
    --network-security-group-name myNetworkSecurityGroup
```

<span data-ttu-id="76c3e-141">Теперь Hello подсети добавляется внутри hello виртуальной сети и связанные с группой безопасности сети hello и правила.</span><span class="sxs-lookup"><span data-stu-id="76c3e-141">hello Subnet is now added inside hello VNet and associated with hello network security group and rule.</span></span>


## <a name="add-a-vnic-toohello-subnet"></a><span data-ttu-id="76c3e-142">Добавить подсеть toohello виртуального сетевого адаптера</span><span class="sxs-lookup"><span data-stu-id="76c3e-142">Add a VNic toohello subnet</span></span>

<span data-ttu-id="76c3e-143">Виртуальные сетевые адаптеры (VNics) являются важными, как можно повторно использовать их, подключив их toodifferent виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="76c3e-143">Virtual network cards (VNics) are important as you can reuse them by connecting them toodifferent VMs.</span></span> <span data-ttu-id="76c3e-144">Этот подход позволяет hello виртуального сетевого адаптера как статический ресурс, пока hello виртуальные машины могут быть как временными.</span><span class="sxs-lookup"><span data-stu-id="76c3e-144">This approach keeps hello VNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="76c3e-145">Создание виртуального сетевого адаптера и связать его с подсетью hello на предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="76c3e-145">Create a VNic and associate it with hello subnet created in hello previous step.</span></span>

```azurecli
azure network nic create myVNic \
    --resource-group myResourceGroup \
    --location eastus \
    ---subnet-vnet-name myVNet \
    --subnet-name mySubNet
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a><span data-ttu-id="76c3e-146">Развертывание hello виртуальной Машины в виртуальной сети hello и NSG</span><span class="sxs-lookup"><span data-stu-id="76c3e-146">Deploy hello VM into hello VNet and NSG</span></span>

<span data-ttu-id="76c3e-147">Теперь у вас есть виртуальная сеть и подсети в этой виртуальной сети и группа безопасности сети выступает tooprotect hello подсети, блокируя весь входящий трафик, за исключением порт 22 для SSH.</span><span class="sxs-lookup"><span data-stu-id="76c3e-147">You now have a VNet and subnet inside that VNet, and a network security group acting tooprotect hello subnet by blocking all inbound traffic except port 22 for SSH.</span></span> <span data-ttu-id="76c3e-148">Теперь может быть развернут Hello виртуальной Машины внутри этой существующей сетевой инфраструктуре.</span><span class="sxs-lookup"><span data-stu-id="76c3e-148">hello VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="76c3e-149">С помощью Azure CLI hello и hello `azure vm create` команды hello виртуальных Машин Linux — развернутой toohello существующие группы ресурсов Azure, виртуальной сети, подсети и виртуального сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="76c3e-149">Using hello Azure CLI, and hello `azure vm create` command, hello Linux VM is deployed toohello existing Azure Resource Group, VNet, Subnet, and VNic.</span></span> <span data-ttu-id="76c3e-150">Дополнительные сведения об использовании toodeploy CLI hello завершения виртуальной Машины в разделе [создать полную среду Linux с помощью hello Azure CLI](create-cli-complete.md)</span><span class="sxs-lookup"><span data-stu-id="76c3e-150">For more information on using hello CLI toodeploy a complete VM, see [Create a complete Linux environment by using hello Azure CLI](create-cli-complete.md)</span></span>

```azurecli
azure vm create myVM \
    --resource-group myResourceGroup \
    --location eastus \
    --os-type linux \
    --image-urn Debian \
    --storage-account-name mystorageaccount \
    --admin-username myAdminUser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --vnet-name myVNet \
    --vnet-subnet-name mySubnet \
    --nic-name myVNic
```

<span data-ttu-id="76c3e-151">С помощью hello CLI флаги toocall существующие ресурсы, вы указываете hello Azure toodeploy виртуальных Машин в существующей сети hello.</span><span class="sxs-lookup"><span data-stu-id="76c3e-151">By using hello CLI flags toocall out existing resources, you instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="76c3e-152">После развертывания виртуальную сеть и подсеть можно оставить в качестве статических или постоянных ресурсов в регионе Azure.</span><span class="sxs-lookup"><span data-stu-id="76c3e-152">Once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="76c3e-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="76c3e-153">Next steps</span></span>

* [<span data-ttu-id="76c3e-154">Использовать toocreate шаблона диспетчера ресурсов Azure конкретного развертывания</span><span class="sxs-lookup"><span data-stu-id="76c3e-154">Use an Azure Resource Manager template toocreate a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="76c3e-155">Создание полной среды Linux с помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="76c3e-155">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="76c3e-156">Создание виртуальной машины Linux с помощью шаблона Azure</span><span class="sxs-lookup"><span data-stu-id="76c3e-156">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
