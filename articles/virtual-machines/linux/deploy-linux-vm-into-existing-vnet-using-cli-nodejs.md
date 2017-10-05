---
title: "Развертывание виртуальных машин Linux в существующей виртуальной сети с помощью Azure CLI 1.0 | Документация Майкрософт"
description: "Как развернуть виртуальную машину Linux в существующей виртуальной сети с помощью Azure CLI 1.0"
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
ms.openlocfilehash: 767a3f7cadba6b1e71e5a8f5995a9db090e419dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-the-azure-cli-10"></a><span data-ttu-id="bbdeb-103">Как развернуть виртуальную машину Linux в существующей виртуальной сети Azure с помощью Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="bbdeb-103">How to deploy a Linux virtual machine into an existing Azure Virtual Network with the Azure CLI 1.0</span></span>

<span data-ttu-id="bbdeb-104">В этой статье объясняется, как с помощью Azure CLI 1.0 развернуть виртуальную машину в существующей виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="bbdeb-104">This article shows you how to use Azure CLI 1.0 to deploy a virtual machine (VM) into an existing Virtual Network (VNet).</span></span> <span data-ttu-id="bbdeb-105">Для этого необходимы следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="bbdeb-105">The requirements are:</span></span>

- <span data-ttu-id="bbdeb-106">[учетная запись Azure](https://azure.microsoft.com/pricing/free-trial/);</span><span class="sxs-lookup"><span data-stu-id="bbdeb-106">[an Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>
- <span data-ttu-id="bbdeb-107">[файлы открытого и закрытого ключа SSH](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="bbdeb-107">[SSH public and private key files](mac-create-ssh-keys.md)</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="bbdeb-108">Версии интерфейса командной строки для выполнения задачи</span><span class="sxs-lookup"><span data-stu-id="bbdeb-108">CLI versions to complete the task</span></span>
<span data-ttu-id="bbdeb-109">Вы можете выполнить задачу, используя одну из следующих версий интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="bbdeb-109">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="bbdeb-110">[Azure CLI 1.0](#quick-commands) — интерфейс командной строки для классической модели развертывания и модели развертывания Resource Manager (в этой статье).</span><span class="sxs-lookup"><span data-stu-id="bbdeb-110">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="bbdeb-111">[Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) — интерфейс командной строки следующего поколения для модели развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bbdeb-111">[Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="bbdeb-112">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="bbdeb-112">Quick Commands</span></span>

<span data-ttu-id="bbdeb-113">Если вам необходимо быстро выполнить задачу, в следующем разделе описаны нужные команды.</span><span class="sxs-lookup"><span data-stu-id="bbdeb-113">If you need to quickly accomplish the task, the following section details the commands needed.</span></span> <span data-ttu-id="bbdeb-114">Более подробные сведения и контекст для каждого этапа можно найти в остальной части документа [начиная отсюда](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="bbdeb-114">More detailed information and context for each step can be found the rest of the document, [starting here](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).</span></span>

<span data-ttu-id="bbdeb-115">Необходимые компоненты: группа ресурсов, виртуальная сеть, группа безопасности сети с входящим трафиком SSH, подсеть.</span><span class="sxs-lookup"><span data-stu-id="bbdeb-115">Pre-requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span></span> <span data-ttu-id="bbdeb-116">Замените все примеры параметров своими параметрами.</span><span class="sxs-lookup"><span data-stu-id="bbdeb-116">Replace any examples with your own settings.</span></span>

### <a name="deploy-the-vm-into-the-virtual-network-infrastructure"></a><span data-ttu-id="bbdeb-117">Развертывание виртуальной машины в инфраструктуре виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="bbdeb-117">Deploy the VM into the virtual network infrastructure</span></span>

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

## <a name="detailed-walkthrough"></a><span data-ttu-id="bbdeb-118">Подробное пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="bbdeb-118">Detailed walkthrough</span></span>

<span data-ttu-id="bbdeb-119">Ресурсы Azure, такие как виртуальные сети и группы безопасности сети, должны быть статическими. Они должны долго храниться и редко развертываться.</span><span class="sxs-lookup"><span data-stu-id="bbdeb-119">Azure assets like the VNets and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="bbdeb-120">После развертывания виртуальной сети ее можно повторно использовать при новых развертываниях. Инфраструктура при этом не пострадает.</span><span class="sxs-lookup"><span data-stu-id="bbdeb-120">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects to the infrastructure.</span></span> <span data-ttu-id="bbdeb-121">Представьте виртуальную сеть, как сетевой коммутатор в парадигме традиционного оборудования.</span><span class="sxs-lookup"><span data-stu-id="bbdeb-121">Think about a VNet as being a traditional hardware network switch.</span></span> <span data-ttu-id="bbdeb-122">Вам не нужно настраивать новый коммутатор при каждом развертывании.</span><span class="sxs-lookup"><span data-stu-id="bbdeb-122">You would not need to configure a brand new hardware switch with each deployment.</span></span> <span data-ttu-id="bbdeb-123">Если виртуальная сеть правильно настроена, вы можете развертывать в ней новые серверы снова и снова, внося некоторые изменения во время ее использования (если они потребуются).</span><span class="sxs-lookup"><span data-stu-id="bbdeb-123">With a correctly configured VNet, you can continue to deploy new servers into that VNet over and over with few, if any, changes required over the life of the VNet.</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="bbdeb-124">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="bbdeb-124">Create the resource group</span></span>

<span data-ttu-id="bbdeb-125">Сначала создайте группу ресурсов, чтобы упорядочить все компоненты, которые будут созданы в этом пошаговом руководстве.</span><span class="sxs-lookup"><span data-stu-id="bbdeb-125">First, create a resource group to organize everything you create in this walkthrough.</span></span> <span data-ttu-id="bbdeb-126">Дополнительные сведения о группах ресурсов см. в статье [Общие сведения о диспетчере ресурсов Azure](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bbdeb-126">For more information about resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md)</span></span>

```azurecli
azure group create myResourceGroup --location eastus
```

## <a name="create-the-vnet"></a><span data-ttu-id="bbdeb-127">Создание виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="bbdeb-127">Create the VNet</span></span>

<span data-ttu-id="bbdeb-128">Сначала нужно создать виртуальную сеть для запуска виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="bbdeb-128">The first step is to build a VNet to launch the VMs into.</span></span> <span data-ttu-id="bbdeb-129">Для этого пошагового руководства виртуальная сеть содержит одну подсеть.</span><span class="sxs-lookup"><span data-stu-id="bbdeb-129">The VNet contains one subnet for this walkthrough.</span></span> <span data-ttu-id="bbdeb-130">Дополнительные сведения о виртуальных сетях Azure см. в статье [Создание виртуальной сети с помощью интерфейса командной строки Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="bbdeb-130">For more information on Azure VNets, see [Create a virtual network by using the Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)</span></span>

```azurecli
azure network vnet create myVNet \
    --resource-group myResourceGroup \
    --address-prefixes 10.10.0.0/24 \
    --location eastus
```

## <a name="create-the-network-security-group"></a><span data-ttu-id="bbdeb-131">Создание группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="bbdeb-131">Create the network security group</span></span>

<span data-ttu-id="bbdeb-132">Подсеть создается за существующей группой безопасности сети, поэтому, прежде чем создавать подсеть, создайте группу безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="bbdeb-132">The subnet is built behind an existing network security group so build the network security group before the subnet.</span></span> <span data-ttu-id="bbdeb-133">На уровне сети группы безопасности сети Azure эквивалентны брандмауэру.</span><span class="sxs-lookup"><span data-stu-id="bbdeb-133">Azure network security groups are equivalent to a firewall at the network layer.</span></span> <span data-ttu-id="bbdeb-134">Дополнительные сведения о группах безопасности сети см. в статье [Создание групп безопасности сети с помощью Azure CLI 2.0](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="bbdeb-134">For more information on Azure network security groups, see [How to create network security groups in the Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)</span></span>

```azurecli
azure network nsg create myNetworkSecurityGroup \
    --resource-group myResourceGroup \
    --location eastus
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="bbdeb-135">Добавление правила, разрешающего входящий трафик по протоколу SSH</span><span class="sxs-lookup"><span data-stu-id="bbdeb-135">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="bbdeb-136">Виртуальной машине требуется доступ к Интернету, поэтому нужно создать правило, разрешающее передачу входящего трафика в сети через порт 22 на виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="bbdeb-136">The VM needs access from the internet so a rule allowing inbound port 22 traffic to be passed through the network to port 22 on the VM is needed.</span></span>

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

## <a name="add-a-subnet-to-the-vnet"></a><span data-ttu-id="bbdeb-137">Добавление подсети в виртуальную сеть</span><span class="sxs-lookup"><span data-stu-id="bbdeb-137">Add a subnet to the VNet</span></span>

<span data-ttu-id="bbdeb-138">Виртуальные машины в виртуальной сети должны быть расположены в подсети.</span><span class="sxs-lookup"><span data-stu-id="bbdeb-138">VMs within the VNet must be located in a subnet.</span></span> <span data-ttu-id="bbdeb-139">Каждая виртуальная сеть может содержать несколько подсетей.</span><span class="sxs-lookup"><span data-stu-id="bbdeb-139">Each VNet can have multiple subnets.</span></span> <span data-ttu-id="bbdeb-140">Создайте подсеть и свяжите ее с группой безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="bbdeb-140">Create the subnet and associate with the network security group.</span></span>

```azurecli
azure network vnet subnet create mySubNet \
    --resource-group myResourceGroup \
    --vnet-name myVNet \
    --address-prefix 10.10.0.0/26 \
    --network-security-group-name myNetworkSecurityGroup
```

<span data-ttu-id="bbdeb-141">Теперь подсеть добавлена в виртуальную сеть и связана с группой безопасности сети и ее правилом.</span><span class="sxs-lookup"><span data-stu-id="bbdeb-141">The Subnet is now added inside the VNet and associated with the network security group and rule.</span></span>


## <a name="add-a-vnic-to-the-subnet"></a><span data-ttu-id="bbdeb-142">Добавление виртуальной сетевой карты в подсеть</span><span class="sxs-lookup"><span data-stu-id="bbdeb-142">Add a VNic to the subnet</span></span>

<span data-ttu-id="bbdeb-143">Виртуальные сетевые карты (VNic) имеют большое значение, так как их можно повторно использовать, подключая к разным виртуальным машинам.</span><span class="sxs-lookup"><span data-stu-id="bbdeb-143">Virtual network cards (VNics) are important as you can reuse them by connecting them to different VMs.</span></span> <span data-ttu-id="bbdeb-144">Это позволяет использовать виртуальную сетевую карту как статический ресурс, тогда как виртуальные машины могут быть временными.</span><span class="sxs-lookup"><span data-stu-id="bbdeb-144">This approach keeps the VNic as a static resource while the VMs can be temporary.</span></span> <span data-ttu-id="bbdeb-145">Создайте виртуальную сетевую карту и свяжите ее с подсетью, созданной на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="bbdeb-145">Create a VNic and associate it with the subnet created in the previous step.</span></span>

```azurecli
azure network nic create myVNic \
    --resource-group myResourceGroup \
    --location eastus \
    ---subnet-vnet-name myVNet \
    --subnet-name mySubNet
```

## <a name="deploy-the-vm-into-the-vnet-and-nsg"></a><span data-ttu-id="bbdeb-146">Развертывание виртуальной машины в виртуальной сети и группе безопасности сети</span><span class="sxs-lookup"><span data-stu-id="bbdeb-146">Deploy the VM into the VNet and NSG</span></span>

<span data-ttu-id="bbdeb-147">Теперь у вас есть виртуальная сеть, подсеть в виртуальной сети и группа безопасности сети для защиты подсети путем блокирования всего входящего трафика, кроме трафика, поступающего через порт 22 по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="bbdeb-147">You now have a VNet and subnet inside that VNet, and a network security group acting to protect the subnet by blocking all inbound traffic except port 22 for SSH.</span></span> <span data-ttu-id="bbdeb-148">Теперь виртуальную машину можно развернуть в этой существующей сетевой инфраструктуре.</span><span class="sxs-lookup"><span data-stu-id="bbdeb-148">The VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="bbdeb-149">С помощью Azure CLI и команды `azure vm create` виртуальную машину Linux можно развернуть в существующей группе ресурсов Azure, виртуальной сети, подсети и виртуальной сетевой карте.</span><span class="sxs-lookup"><span data-stu-id="bbdeb-149">Using the Azure CLI, and the `azure vm create` command, the Linux VM is deployed to the existing Azure Resource Group, VNet, Subnet, and VNic.</span></span> <span data-ttu-id="bbdeb-150">Дополнительные сведения о развертывании всех компонентов виртуальной машины с помощью интерфейса командной строки см. в статье [Создание полной среды Linux с помощью интерфейса командной строки Azure](create-cli-complete.md).</span><span class="sxs-lookup"><span data-stu-id="bbdeb-150">For more information on using the CLI to deploy a complete VM, see [Create a complete Linux environment by using the Azure CLI](create-cli-complete.md)</span></span>

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

<span data-ttu-id="bbdeb-151">Используя флаги интерфейса командной строки для вызова существующих ресурсов, дайте среде Azure инструкцию развернуть виртуальную машину в существующей сети.</span><span class="sxs-lookup"><span data-stu-id="bbdeb-151">By using the CLI flags to call out existing resources, you instruct Azure to deploy the VM inside the existing network.</span></span> <span data-ttu-id="bbdeb-152">После развертывания виртуальную сеть и подсеть можно оставить в качестве статических или постоянных ресурсов в регионе Azure.</span><span class="sxs-lookup"><span data-stu-id="bbdeb-152">Once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="bbdeb-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bbdeb-153">Next steps</span></span>

* [<span data-ttu-id="bbdeb-154">Развертывание виртуальных машин и управление ими с помощью шаблонов диспетчера ресурсов Azure и интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="bbdeb-154">Use an Azure Resource Manager template to create a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="bbdeb-155">Создание полной среды Linux с помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="bbdeb-155">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="bbdeb-156">Создание виртуальной машины Linux с помощью шаблона Azure</span><span class="sxs-lookup"><span data-stu-id="bbdeb-156">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
