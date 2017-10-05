---
title: "Развертывание виртуальных машин Linux в существующей виртуальной сети с помощью Azure CLI 2.0 | Документация Майкрософт"
description: "Узнайте, как развернуть виртуальную машину Linux в существующей виртуальной сети с помощью Azure CLI 2.0"
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
ms.openlocfilehash: 932fd74ec83f43b604382346ee2c273f5453fcd0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-the-azure-cli"></a><span data-ttu-id="593b3-103">Как развернуть виртуальную машину Linux в существующей виртуальной сети Azure с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="593b3-103">How to deploy a Linux virtual machine into an existing Azure Virtual Network with the Azure CLI</span></span>

<span data-ttu-id="593b3-104">В этой статье показано, как с помощью Azure CLI 2.0 развернуть виртуальную машину в существующей виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="593b3-104">This article shows you how to use the Azure CLI 2.0 to deploy a virtual machine (VM) into an existing virtual network.</span></span> <span data-ttu-id="593b3-105">Для этого необходимы следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="593b3-105">The requirements are:</span></span>

- <span data-ttu-id="593b3-106">[учетная запись Azure](https://azure.microsoft.com/pricing/free-trial/);</span><span class="sxs-lookup"><span data-stu-id="593b3-106">[an Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>
- <span data-ttu-id="593b3-107">[файлы открытого и закрытого ключа SSH](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="593b3-107">[SSH public and private key files](mac-create-ssh-keys.md)</span></span>

<span data-ttu-id="593b3-108">Эти действия можно также выполнить с помощью [Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="593b3-108">You can also perform these steps with the [Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md).</span></span>


## <a name="quick-commands"></a><span data-ttu-id="593b3-109">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="593b3-109">Quick Commands</span></span>
<span data-ttu-id="593b3-110">Если вам необходимо быстро выполнить задачу, в следующем разделе описаны нужные команды.</span><span class="sxs-lookup"><span data-stu-id="593b3-110">If you need to quickly accomplish the task, the following section details the  commands needed.</span></span> <span data-ttu-id="593b3-111">Более подробные сведения и контекст для каждого этапа можно найти в остальной части документа [начиная отсюда](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="593b3-111">More detailed information and context for each step can be found the rest of the document, [starting here](#detailed-walkthrough).</span></span>

<span data-ttu-id="593b3-112">Для создания этой настраиваемой среды необходимо установить последнюю версию [Azure CLI 2.0](/cli/azure/install-az-cli2) и войти в учетную запись Azure с помощью команды [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="593b3-112">To create this custom environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="593b3-113">В следующих примерах замените имена параметров собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="593b3-113">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="593b3-114">Примеры имен параметров: *myResourceGroup*, *myVnet* и *myVM*.</span><span class="sxs-lookup"><span data-stu-id="593b3-114">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

<span data-ttu-id="593b3-115">**Предварительные требования:** группа ресурсов Azure, виртуальная сеть и подсеть, группа безопасности сети с разрешенными входящими подключениями SSH и виртуальная сетевая карта.</span><span class="sxs-lookup"><span data-stu-id="593b3-115">**Pre-requirements:** Azure resource group, virtual network and subnet, network security group with SSH inbound, and a virtual network interface card.</span></span>

### <a name="deploy-the-vm-into-the-virtual-network-infrastructure"></a><span data-ttu-id="593b3-116">Развертывание виртуальной машины в инфраструктуре виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="593b3-116">Deploy the VM into the virtual network infrastructure</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="593b3-117">Подробное пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="593b3-117">Detailed walkthrough</span></span>

<span data-ttu-id="593b3-118">Ресурсы Azure, такие как виртуальные сети и группы безопасности сети, должны быть статическими. Они должны долго храниться и редко развертываться.</span><span class="sxs-lookup"><span data-stu-id="593b3-118">Azure assets like virtual networks and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="593b3-119">После развертывания виртуальной сети ее можно повторно использовать при новых развертываниях. Инфраструктура при этом не пострадает.</span><span class="sxs-lookup"><span data-stu-id="593b3-119">Once a virtual network has been deployed, it can be reused by new deployments without any adverse affects to the infrastructure.</span></span> <span data-ttu-id="593b3-120">Воспринимайте виртуальную сеть в качестве традиционного аппаратного сетевого коммутатора. Вам не понадобится настраивать новый аппаратный коммутатор с каждым развертыванием.</span><span class="sxs-lookup"><span data-stu-id="593b3-120">Think about a virtual network as being a traditional hardware network switch - you would not need to configure a brand new hardware switch with each deployment.</span></span> <span data-ttu-id="593b3-121">Если виртуальная сеть настроена правильно, в ней можно продолжать развертывать новые виртуальные машины снова и снова, при необходимости внося малочисленные изменения во время ее использования.</span><span class="sxs-lookup"><span data-stu-id="593b3-121">With a correctly configured virtual network, you can continue to deploy new VMs into that virtual network over and over with few, if any, changes required over the life of the virtual network.</span></span>

<span data-ttu-id="593b3-122">Для создания этой настраиваемой среды необходимо установить последнюю версию [Azure CLI 2.0](/cli/azure/install-az-cli2) и войти в учетную запись Azure с помощью команды [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="593b3-122">To create this custom environment, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="593b3-123">В следующих примерах замените имена параметров собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="593b3-123">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="593b3-124">Примеры имен параметров: *myResourceGroup*, *myVnet* и *myVM*.</span><span class="sxs-lookup"><span data-stu-id="593b3-124">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="593b3-125">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="593b3-125">Create the resource group</span></span>

<span data-ttu-id="593b3-126">Сначала создайте группу ресурсов Azure для упорядочения всех компонентов, которые будут созданы в этом пошаговом руководстве.</span><span class="sxs-lookup"><span data-stu-id="593b3-126">First, create an Azure resource group to organize everything you create in this walkthrough.</span></span> <span data-ttu-id="593b3-127">Дополнительные сведения о группах ресурсов см. в статье [Общие сведения об Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="593b3-127">For more information on resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="593b3-128">Создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="593b3-128">Create the resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="593b3-129">В следующем примере создается группа ресурсов с именем *myResourceGroup* в расположении *eastus*.</span><span class="sxs-lookup"><span data-stu-id="593b3-129">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

## <a name="create-the-virtual-network"></a><span data-ttu-id="593b3-130">Создание виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="593b3-130">Create the virtual network</span></span>

<span data-ttu-id="593b3-131">Давайте создадим виртуальную сеть Azure для запуска виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="593b3-131">Lets build an Azure virtual network to launch the VMs into.</span></span> <span data-ttu-id="593b3-132">Дополнительные сведения о виртуальных сетях см. в статье [Создание виртуальной сети с помощью интерфейса командной строки Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="593b3-132">For more information on virtual networks, see [Create a virtual network by using the Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md).</span></span> <span data-ttu-id="593b3-133">Создайте виртуальную сеть с помощью команды [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="593b3-133">Create the virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="593b3-134">В следующем примере создаются виртуальная сеть *myVnet* и подсеть *mySubnet*.</span><span class="sxs-lookup"><span data-stu-id="593b3-134">The following example creates a virtual network named *myVnet* and subnet named *mySubnet*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefix 10.10.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 10.10.1.0/24
```

## <a name="create-the-network-security-group"></a><span data-ttu-id="593b3-135">Создание группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="593b3-135">Create the network security group</span></span>

<span data-ttu-id="593b3-136">На уровне сети группы безопасности сети Azure эквивалентны брандмауэру.</span><span class="sxs-lookup"><span data-stu-id="593b3-136">Azure network security groups are equivalent to a firewall at the network layer.</span></span> <span data-ttu-id="593b3-137">Дополнительные сведения о группах безопасности сети см. в статье [Создание групп безопасности сети с помощью интерфейса командной строки Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="593b3-137">For more information on network security groups, see [How to create network security groups in the Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span></span> <span data-ttu-id="593b3-138">Создайте группу безопасности сети с помощью команды [az network nsg create](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="593b3-138">Create the network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="593b3-139">В следующем примере создается группа безопасности сети *myNetworkSecurityGroup*.</span><span class="sxs-lookup"><span data-stu-id="593b3-139">The following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="593b3-140">Добавление правила, разрешающего входящий трафик по протоколу SSH</span><span class="sxs-lookup"><span data-stu-id="593b3-140">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="593b3-141">Виртуальной машине нужен доступ к Интернету, поэтому требуется правило, разрешающее передачу входящего трафика в сети через порт 22 на виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="593b3-141">The VM needs access from the internet, so a rule allowing inbound port 22 traffic to be passed through the network to port 22 on the VM is needed.</span></span> <span data-ttu-id="593b3-142">Добавьте в группу безопасности сети правило входящего трафика с помощью команды [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="593b3-142">Add an inbound rule for the network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="593b3-143">В следующем примере создается правило *myNetworkSecurityGroupRuleSSH*.</span><span class="sxs-lookup"><span data-stu-id="593b3-143">The following example creates a rule named *myNetworkSecurityGroupRuleSSH*:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --priority 1000 \
    --protocol tcp \
    --destination-port-range 22 \
```

## <a name="attach-the-subnet-to-the-network-security-group"></a><span data-ttu-id="593b3-144">Подключение подсети к группе безопасности сети</span><span class="sxs-lookup"><span data-stu-id="593b3-144">Attach the subnet to the network security group</span></span>

<span data-ttu-id="593b3-145">Правила группы безопасности сети можно применять к подсети или определенному виртуальному сетевому интерфейсу.</span><span class="sxs-lookup"><span data-stu-id="593b3-145">The network security group rules can be applied to a subnet or a specific virtual network interface.</span></span> <span data-ttu-id="593b3-146">Давайте подключим группу безопасности сети к нашей подсети.</span><span class="sxs-lookup"><span data-stu-id="593b3-146">Lets attach the network security group to our subnet.</span></span> <span data-ttu-id="593b3-147">Подключите подсеть к группе безопасности сети с помощью команды [az network vnet subnet update](/cli/azure/network/vnet/subnet#update).</span><span class="sxs-lookup"><span data-stu-id="593b3-147">Attach your subnet to the network security group with [az network vnet subnet update](/cli/azure/network/vnet/subnet#update):</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="add-a-virtual-network-interface-card-to-the-subnet"></a><span data-ttu-id="593b3-148">Добавление виртуальной сетевой карты в подсеть</span><span class="sxs-lookup"><span data-stu-id="593b3-148">Add a virtual network interface card to the subnet</span></span>

<span data-ttu-id="593b3-149">Виртуальные сетевые карты (VNic) имеют большое значение, так как их можно повторно использовать, подключая к разным виртуальным машинам.</span><span class="sxs-lookup"><span data-stu-id="593b3-149">Virtual network interface cards (VNics) are important as you can reuse them by connecting them to different VMs.</span></span> <span data-ttu-id="593b3-150">Это позволяет использовать виртуальную сетевую карту как статический ресурс, тогда как виртуальные машины могут быть временными.</span><span class="sxs-lookup"><span data-stu-id="593b3-150">This reuse allows you to keep the VNic as a static resource while the VMs can be temporary.</span></span> <span data-ttu-id="593b3-151">Создайте виртуальную сетевую карту и свяжите ее с подсетью, выполнив команду [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="593b3-151">Create a VNic and associate it with the subnet with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="593b3-152">В следующем примере создается виртуальная сетевая карта *myNic*.</span><span class="sxs-lookup"><span data-stu-id="593b3-152">The following example creates a VNic named *myNic*:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet
```

## <a name="deploy-the-vm-into-the-virtual-network-infrastructure"></a><span data-ttu-id="593b3-153">Развертывание виртуальной машины в инфраструктуре виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="593b3-153">Deploy the VM into the virtual network infrastructure</span></span>

<span data-ttu-id="593b3-154">Теперь у вас есть виртуальная сеть, подсеть и группа безопасности сети для защиты подсети путем блокирования всего входящего трафика, кроме трафика, поступающего через порт 22 по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="593b3-154">You now have a virtual network and subnet, and a network security group to protect the subnet by blocking all inbound traffic except port 22 for SSH.</span></span> <span data-ttu-id="593b3-155">Теперь виртуальную машину можно развернуть в этой существующей сетевой инфраструктуре.</span><span class="sxs-lookup"><span data-stu-id="593b3-155">The VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="593b3-156">Создайте виртуальную машину с помощью команды [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="593b3-156">Create your VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="593b3-157">Дополнительные сведения о флагах, используемых в Azure CLI 2.0 для полного развертывания виртуальной машины, см. в статье [Создание полной среды Linux с помощью Azure CLI](create-cli-complete.md).</span><span class="sxs-lookup"><span data-stu-id="593b3-157">For more information on the flags to use with the Azure CLI 2.0 to deploy a complete VM, see [Create a complete Linux environment by using the Azure CLI](create-cli-complete.md).</span></span>

<span data-ttu-id="593b3-158">В следующем примере создается виртуальная машина с помощью управляемых дисков.</span><span class="sxs-lookup"><span data-stu-id="593b3-158">The following example creates a VM using Azure Managed Disks.</span></span> <span data-ttu-id="593b3-159">Эти диски полностью контролируются платформой Azure и не требуют никакой подготовки или хранилища.</span><span class="sxs-lookup"><span data-stu-id="593b3-159">These disks are handled by the Azure platform and do not require any preparation or location to store them.</span></span> <span data-ttu-id="593b3-160">Дополнительные сведения об управляемых дисках Azure см. в [этой статье](../../storage/storage-managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="593b3-160">For more information about managed disks, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md).</span></span> <span data-ttu-id="593b3-161">Если вы хотите использовать неуправляемые диски, см. дополнительное примечание ниже.</span><span class="sxs-lookup"><span data-stu-id="593b3-161">If you wish to use unmanaged disks, see the additional note below.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

<span data-ttu-id="593b3-162">Если вы используете управляемые диски, пропустите этот шаг.</span><span class="sxs-lookup"><span data-stu-id="593b3-162">If you use managed disks, skip this step.</span></span> <span data-ttu-id="593b3-163">Если вы хотите использовать неуправляемые диски, необходимо добавить следующие дополнительные параметры к команде, чтобы создать неуправляемые диски в учетной записи хранения с именем `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="593b3-163">If you wish to use unmanaged disks, you need to add the following additional parameters to the proceeding command to create unmanaged disks in the storage account named `mystorageaccount`:</span></span> 

```azurecli
    --use-unmanaged-disk \
    --storage-account mystorageaccount
```

<span data-ttu-id="593b3-164">Используя флаги интерфейса командной строки для вызова существующих ресурсов, дайте среде Azure инструкцию развернуть виртуальную машину в существующей сети.</span><span class="sxs-lookup"><span data-stu-id="593b3-164">By using the CLI flags to call out existing resources, you instruct Azure to deploy the VM inside the existing network.</span></span> <span data-ttu-id="593b3-165">После развертывания виртуальную сеть и подсеть можно оставить в качестве статических или постоянных ресурсов в регионе Azure.</span><span class="sxs-lookup"><span data-stu-id="593b3-165">Once a virtual network and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span> <span data-ttu-id="593b3-166">В этом примере вы не создали общедоступный IP-адрес и не назначили его виртуальной сетевой карте. Следовательно, эта виртуальная машина не является общедоступной через Интернет.</span><span class="sxs-lookup"><span data-stu-id="593b3-166">In this example, you did not create and assign a public IP address to the VNic, so this VM is not publicly accessible over the Internet.</span></span> <span data-ttu-id="593b3-167">Дополнительные сведения см. в разделе [Развертывание виртуальной машины со статическим общедоступным IP-адресом с использованием портала Azure CLI](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="593b3-167">For more information, see [Create a VM with a static public IP using the Azure CLI](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="593b3-168">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="593b3-168">Next steps</span></span>
<span data-ttu-id="593b3-169">Дополнительные сведения о способах создания виртуальных машин в Azure доступны в следующих материалах:</span><span class="sxs-lookup"><span data-stu-id="593b3-169">For more information about ways to create virtual machines in Azure, see the following resources:</span></span>

* [<span data-ttu-id="593b3-170">Развертывание виртуальных машин и управление ими с помощью шаблонов диспетчера ресурсов Azure и интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="593b3-170">Use an Azure Resource Manager template to create a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="593b3-171">Создание полной среды Linux с помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="593b3-171">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="593b3-172">Создание виртуальной машины Linux с помощью шаблона Azure</span><span class="sxs-lookup"><span data-stu-id="593b3-172">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
