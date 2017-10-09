---
title: "aaaUse внутренние DNS для виртуальной Машины имен с hello Azure CLI 2.0 | Документы Microsoft"
description: "Как карт toocreate виртуальной сети и использовать внутренние DNS для разрешения имен виртуальных Машин в Azure с hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 02/16/2017
ms.author: v-livech
ms.openlocfilehash: b3c4bfd3ab698f7b25d763ba9e60dd7984f6269d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-virtual-network-interface-cards-and-use-internal-dns-for-vm-name-resolution-on-azure"></a><span data-ttu-id="28687-103">Создание виртуальных сетевых карт и использование внутренних DNS-имен для разрешения имен виртуальных машин в Azure</span><span class="sxs-lookup"><span data-stu-id="28687-103">Create virtual network interface cards and use internal DNS for VM name resolution on Azure</span></span>
<span data-ttu-id="28687-104">В этой статье показано, как tooset статические внутренние имена DNS для виртуальных машин Linux с помощью виртуальных сетевых интерфейсных плат (vNics) и DNS-имена меток с hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="28687-104">This article shows you how tooset static internal DNS names for Linux VMs using virtual network interface cards (vNics) and DNS label names with hello Azure CLI 2.0.</span></span> <span data-ttu-id="28687-105">Можно также выполнить следующие действия с hello [Azure CLI 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="28687-105">You can also perform these steps with hello [Azure CLI 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="28687-106">Статические имена DNS используются для постоянных инфраструктурных служб, таких как сервер сборки Jenkins, который используется для этого поддержания документа, или сервер Git.</span><span class="sxs-lookup"><span data-stu-id="28687-106">Static DNS names are used for permanent infrastructure services like a Jenkins build server, which is used for this document, or a Git server.</span></span>

<span data-ttu-id="28687-107">Существуют следующие требования Hello.</span><span class="sxs-lookup"><span data-stu-id="28687-107">hello requirements are:</span></span>

* <span data-ttu-id="28687-108">[учетная запись Azure](https://azure.microsoft.com/pricing/free-trial/);</span><span class="sxs-lookup"><span data-stu-id="28687-108">[an Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>
* <span data-ttu-id="28687-109">[файлы открытого и закрытого ключа SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="28687-109">[SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="quick-commands"></a><span data-ttu-id="28687-110">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="28687-110">Quick commands</span></span>
<span data-ttu-id="28687-111">Если вам требуется tooquickly выполнения задачи hello, hello в следующем разделе подробно описываются hello команд, которые необходимы.</span><span class="sxs-lookup"><span data-stu-id="28687-111">If you need tooquickly accomplish hello task, hello following section details hello commands needed.</span></span> <span data-ttu-id="28687-112">Более подробные сведения и контекста, для каждого шага можно найти в hello остальной части документа hello [начиная здесь](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="28687-112">More detailed information and context for each step can be found in hello rest of hello document, [starting here](#detailed-walkthrough).</span></span> <span data-ttu-id="28687-113">tooperform эти шаги, необходимые hello последней [Azure CLI 2.0](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="28687-113">tooperform these steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="28687-114">Предварительные требования: группа ресурсов, виртуальная сеть и подсеть, группа безопасности сети с разрешенными входящими подключениями SSH.</span><span class="sxs-lookup"><span data-stu-id="28687-114">Pre-Requirements: Resource Group, virtual network and subnet, Network Security Group with SSH inbound.</span></span>

### <a name="create-a-virtual-network-interface-card-with-a-static-internal-dns-name"></a><span data-ttu-id="28687-115">Создание виртуальной сетевой карты со статическим внутренним DNS-именем</span><span class="sxs-lookup"><span data-stu-id="28687-115">Create a virtual network interface card with a static internal DNS name</span></span>
<span data-ttu-id="28687-116">Создание виртуального сетевого адаптера hello с [Создание сетевого адаптера сети az](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="28687-116">Create hello vNic with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="28687-117">Hello `--internal-dns-name` CLI флаг предназначен для параметра hello DNS метку, которую предоставляет hello статических DNS-имя для hello виртуальный сетевой адаптер (vNic).</span><span class="sxs-lookup"><span data-stu-id="28687-117">hello `--internal-dns-name` CLI flag is for setting hello DNS label, which provides hello static DNS name for hello virtual network interface card (vNic).</span></span> <span data-ttu-id="28687-118">Hello следующем примере создается виртуальный сетевой адаптер с именем `myNic`, подключает его toohello `myVnet` виртуальной сети и создает внутренние DNS-имя запись вызывается `jenkins`:</span><span class="sxs-lookup"><span data-stu-id="28687-118">hello following example creates a vNic named `myNic`, connects it toohello `myVnet` virtual network, and creates an internal DNS name record called `jenkins`:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

### <a name="deploy-a-vm-and-connect-hello-vnic"></a><span data-ttu-id="28687-119">Развертывание виртуальной Машины и подключение виртуального сетевого адаптера hello</span><span class="sxs-lookup"><span data-stu-id="28687-119">Deploy a VM and connect hello vNic</span></span>
<span data-ttu-id="28687-120">Создайте виртуальную машину с помощью команды [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="28687-120">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="28687-121">Hello `--nics` флаг подключается toohello hello виртуального сетевого адаптера виртуальной Машины во время развертывания tooAzure hello.</span><span class="sxs-lookup"><span data-stu-id="28687-121">hello `--nics` flag connects hello vNic toohello VM during hello deployment tooAzure.</span></span> <span data-ttu-id="28687-122">Hello следующий пример создает Виртуальную машину с именем `myVM` с дисками управляемых Azure и присоединяет виртуального сетевого адаптера hello с именем `myNic` из предыдущих шага hello:</span><span class="sxs-lookup"><span data-stu-id="28687-122">hello following example creates a VM named `myVM` with Azure Managed Disks and attaches hello vNic named `myNic` from hello preceding step:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="28687-123">Подробное пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="28687-123">Detailed walkthrough</span></span>

<span data-ttu-id="28687-124">Полная непрерывной интеграции и непрерывного развертывания (CiCd) инфраструктуру в Azure требует определенных серверов toobe статической или долгоживущие серверов.</span><span class="sxs-lookup"><span data-stu-id="28687-124">A full continuous integration and continuous deployment (CiCd) infrastructure on Azure requires certain servers toobe static or long-lived servers.</span></span> <span data-ttu-id="28687-125">Рекомендуется являются статическими активов Azure как hello виртуальных сетей и группы безопасности сети, а также долго ресурсы, которые развертываются редко.</span><span class="sxs-lookup"><span data-stu-id="28687-125">It is recommended that Azure assets like hello virtual networks and Network Security Groups are static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="28687-126">После развертывания виртуальной сети, он может быть использован в новые развертывания без инфраструктуры toohello любой негативно влияет на.</span><span class="sxs-lookup"><span data-stu-id="28687-126">Once a virtual network has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="28687-127">Позднее можно добавить сервер репозитория Git или сервер автоматизации Jenkins доставляет CiCd toothis виртуальной сети для сред разработки и тестирования.</span><span class="sxs-lookup"><span data-stu-id="28687-127">You can later add a Git repository server or a Jenkins automation server delivers CiCd toothis virtual network for your development or test environments.</span></span>  

<span data-ttu-id="28687-128">Внутренние имена DNS можно сопоставлять только внутри виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="28687-128">Internal DNS names are only resolvable inside an Azure virtual network.</span></span> <span data-ttu-id="28687-129">Так как hello DNS-имена являются внутренними, они не удается разрешить toohello за пределами Интернет, обеспечивая дополнительную безопасность инфраструктуры toohello.</span><span class="sxs-lookup"><span data-stu-id="28687-129">Because hello DNS names are internal, they are not resolvable toohello outside internet, providing additional security toohello infrastructure.</span></span>

<span data-ttu-id="28687-130">В hello следующих примерах замените примеры имен параметров собственные значения.</span><span class="sxs-lookup"><span data-stu-id="28687-130">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="28687-131">Используемые имена параметров: `myResourceGroup`, `myNic` и `myVM`.</span><span class="sxs-lookup"><span data-stu-id="28687-131">Example parameter names include `myResourceGroup`, `myNic`, and `myVM`.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="28687-132">Создать группу ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="28687-132">Create hello resource group</span></span>
<span data-ttu-id="28687-133">Во-первых, создать группу ресурсов hello с [Создание группы az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="28687-133">First, create hello resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="28687-134">Hello следующий пример создает группу ресурсов с именем `myResourceGroup` в hello `westus` расположение:</span><span class="sxs-lookup"><span data-stu-id="28687-134">hello following example creates a resource group named `myResourceGroup` in hello `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-hello-virtual-network"></a><span data-ttu-id="28687-135">Создайте виртуальную сеть hello</span><span class="sxs-lookup"><span data-stu-id="28687-135">Create hello virtual network</span></span>

<span data-ttu-id="28687-136">Hello следующим шагом является toobuild виртуальных машин в hello toolaunch виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="28687-136">hello next step is toobuild a virtual network toolaunch hello VMs into.</span></span> <span data-ttu-id="28687-137">Hello виртуальная сеть содержит одну подсеть для этого пошагового руководства.</span><span class="sxs-lookup"><span data-stu-id="28687-137">hello virtual network contains one subnet for this walkthrough.</span></span> <span data-ttu-id="28687-138">Дополнительные сведения о виртуальных сетях Azure см. в разделе [Создание виртуальной сети с помощью Azure CLI hello](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="28687-138">For more information on Azure virtual networks, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="28687-139">Создайте виртуальную сеть hello с [создания az сети vnet](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="28687-139">Create hello virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="28687-140">Hello следующий пример создает виртуальную сеть с именем `myVnet` и подсеть с именем `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="28687-140">hello following example creates a virtual network named `myVnet` and subnet named `mySubnet`:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

## <a name="create-hello-network-security-group"></a><span data-ttu-id="28687-141">Создание группы безопасности сети hello</span><span class="sxs-lookup"><span data-stu-id="28687-141">Create hello Network Security Group</span></span>
<span data-ttu-id="28687-142">Эквивалентный tooa брандмауэра на уровне сети hello являются Azure группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="28687-142">Azure Network Security Groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="28687-143">Дополнительные сведения о сетевых группах безопасности см. в разделе [как Nsg toocreate в hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="28687-143">For more information about Network Security Groups, see [How toocreate NSGs in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="28687-144">Создание группы безопасности сети hello с [создать az сети nsg](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="28687-144">Create hello network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="28687-145">Hello следующий пример создает группу безопасности сети с именем `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="28687-145">hello following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-rule-tooallow-ssh"></a><span data-ttu-id="28687-146">Добавить правило для входящего трафика tooallow SSH</span><span class="sxs-lookup"><span data-stu-id="28687-146">Add an inbound rule tooallow SSH</span></span>
<span data-ttu-id="28687-147">Добавьте правило входящего трафика для hello сетевой группы безопасности с [создать правило nsg сети az](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="28687-147">Add an inbound rule for hello network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="28687-148">Hello следующий код создает правило с именем `myRuleAllowSSH`:</span><span class="sxs-lookup"><span data-stu-id="28687-148">hello following example creates a rule named `myRuleAllowSSH`:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myRuleAllowSSH \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --source-address-prefix '*' \
    --source-port-range '*' \
    --destination-address-prefix '*' \
    --destination-port-range 22 \
    --access allow
```

## <a name="associate-hello-subnet-with-hello-network-security-group"></a><span data-ttu-id="28687-149">Свяжите hello подсеть с hello группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="28687-149">Associate hello subnet with hello Network Security Group</span></span>
<span data-ttu-id="28687-150">Используйте подсеть hello tooassociate с hello сетевой группы безопасности, [обновления подсети виртуальной сети сети az](/cli/azure/network/vnet/subnet#update).</span><span class="sxs-lookup"><span data-stu-id="28687-150">tooassociate hello subnet with hello Network Security Group, use [az network vnet subnet update](/cli/azure/network/vnet/subnet#update).</span></span> <span data-ttu-id="28687-151">Hello следующий пример сопоставляет имя подсети hello `mySubnet` с hello сетевую группу безопасности с именем `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="28687-151">hello following example associates hello subnet name `mySubnet` with hello Network Security Group named `myNetworkSecurityGroup`:</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```


## <a name="create-hello-virtual-network-interface-card-and-static-dns-names"></a><span data-ttu-id="28687-152">Создайте виртуальный сетевой адаптер hello и статические имена DNS</span><span class="sxs-lookup"><span data-stu-id="28687-152">Create hello virtual network interface card and static DNS names</span></span>
<span data-ttu-id="28687-153">Azure обладает большой гибкостью, однако toouse DNS-имен для разрешения имен виртуальных Машин, требуют toocreate виртуальных сетевых картах (vNics), включающие метка DNS.</span><span class="sxs-lookup"><span data-stu-id="28687-153">Azure is very flexible, but toouse DNS names for VM name resolution, you need toocreate virtual network interface cards (vNics) that include a DNS label.</span></span> <span data-ttu-id="28687-154">vNics являются важными, как можно повторно использовать их, подключив их виртуальные машины toodifferent над жизненным циклом инфраструктуры hello.</span><span class="sxs-lookup"><span data-stu-id="28687-154">vNics are important as you can reuse them by connecting them toodifferent VMs over hello infrastructure lifecycle.</span></span> <span data-ttu-id="28687-155">Этот подход позволяет hello виртуального сетевого адаптера как статический ресурс, пока hello виртуальные машины могут быть как временными.</span><span class="sxs-lookup"><span data-stu-id="28687-155">This approach keeps hello vNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="28687-156">С помощью DNS, пометки hello виртуальный сетевой адаптер, не может tooenable простое имя разрешения из других виртуальных машин в виртуальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="28687-156">By using DNS labeling on hello vNic, we are able tooenable simple name resolution from other VMs in hello VNet.</span></span> <span data-ttu-id="28687-157">С помощью разрешения имен включает другие виртуальные машины сервера автоматизации hello tooaccess hello DNS-именем `Jenkins` или сервера hello Git в качестве `gitrepo`.</span><span class="sxs-lookup"><span data-stu-id="28687-157">Using resolvable names enables other VMs tooaccess hello automation server by hello DNS name `Jenkins` or hello Git server as `gitrepo`.</span></span>  

<span data-ttu-id="28687-158">Создание виртуального сетевого адаптера hello с [Создание сетевого адаптера сети az](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="28687-158">Create hello vNic with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="28687-159">Hello следующем примере создается виртуальный сетевой адаптер с именем `myNic`, подключает его toohello `myVnet` виртуальная сеть с именем `myVnet`и создает внутренние DNS-имя запись вызывается `jenkins`:</span><span class="sxs-lookup"><span data-stu-id="28687-159">hello following example creates a vNic named `myNic`, connects it toohello `myVnet` virtual network named `myVnet`, and creates an internal DNS name record called `jenkins`:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="28687-160">Развертывание hello виртуальных Машин в инфраструктуре виртуальной сети hello</span><span class="sxs-lookup"><span data-stu-id="28687-160">Deploy hello VM into hello virtual network infrastructure</span></span>
<span data-ttu-id="28687-161">Теперь имеется виртуальной сети и подсети, группы безопасности сети, выступающего в качестве tooprotect брандмауэра нашей подсети, блокируя весь входящий трафик, за исключением порт 22 для SSH и виртуального сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="28687-161">We now have a virtual network and subnet, a Network Security Group acting as a firewall tooprotect our subnet by blocking all inbound traffic except port 22 for SSH, and a vNic.</span></span> <span data-ttu-id="28687-162">Теперь вы можете развернуть виртуальную машину в этой созданной сетевой инфраструктуре.</span><span class="sxs-lookup"><span data-stu-id="28687-162">You can now deploy a VM inside this existing network infrastructure.</span></span>

<span data-ttu-id="28687-163">Создайте виртуальную машину с помощью команды [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="28687-163">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="28687-164">Hello следующий пример создает Виртуальную машину с именем `myVM` с дисками управляемых Azure и присоединяет виртуального сетевого адаптера hello с именем `myNic` из предыдущих шага hello:</span><span class="sxs-lookup"><span data-stu-id="28687-164">hello following example creates a VM named `myVM` with Azure Managed Disks and attaches hello vNic named `myNic` from hello preceding step:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

<span data-ttu-id="28687-165">С помощью hello CLI флаги toocall существующие ресурсы мы поручить Azure toodeploy hello виртуальных Машин в существующей сети hello.</span><span class="sxs-lookup"><span data-stu-id="28687-165">By using hello CLI flags toocall out existing resources, we instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="28687-166">tooreiterate, после развертывания виртуальной сети и подсети они могут остаться статические или постоянным ресурсов в ваш регион Azure.</span><span class="sxs-lookup"><span data-stu-id="28687-166">tooreiterate, once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="28687-167">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="28687-167">Next steps</span></span>
* [<span data-ttu-id="28687-168">Создание полной среды Linux с помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="28687-168">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="28687-169">Создание виртуальной машины Linux с помощью шаблона Azure</span><span class="sxs-lookup"><span data-stu-id="28687-169">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
