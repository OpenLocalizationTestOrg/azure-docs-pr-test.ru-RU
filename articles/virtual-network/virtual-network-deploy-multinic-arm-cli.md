---
title: "виртуальную Машину с несколькими сетевыми картами - CLI Azure 2.0 aaaCreate | Документы Microsoft"
description: "Узнайте, как toocreate виртуальной Машины с несколькими сетевыми картами с помощью hello Azure CLI 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8e906a4b-8583-4a97-9416-ee34cfa09a98
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac0291a978e2c8682c69104915196cc6c4fcf8dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-hello-azure-cli-20"></a><span data-ttu-id="44e96-103">Создайте виртуальную Машину с несколькими сетевыми адаптерами, используя hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="44e96-103">Create a VM with multiple NICs using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="44e96-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="44e96-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="44e96-105">В этой статье описывается использование модели развертывания диспетчера ресурсов hello, который рекомендуется в большинстве случаев новый вместо hello [классической модели развертывания](virtual-network-deploy-multinic-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="44e96-105">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](virtual-network-deploy-multinic-classic-cli.md).</span></span>
>

## <span data-ttu-id="44e96-106"><a name="create"></a>Создание виртуальной Машины hello</span><span class="sxs-lookup"><span data-stu-id="44e96-106"><a name="create"></a>Create hello VM</span></span>

<span data-ttu-id="44e96-107">Выполнить эту задачу с помощью hello Azure CLI 2.0 (Эта статья) или hello [Azure CLI 1.0](virtual-network-deploy-multinic-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="44e96-107">You can complete this task using hello Azure CLI 2.0 (this article) or hello [Azure CLI 1.0](virtual-network-deploy-multinic-cli-nodejs.md).</span></span> <span data-ttu-id="44e96-108">Здравствуйте, значения в «» для переменных hello в hello описанных ниже создать ресурсы с параметрами из сценария hello.</span><span class="sxs-lookup"><span data-stu-id="44e96-108">hello values in "" for hello variables in hello steps that follow create resources with settings from hello scenario.</span></span> <span data-ttu-id="44e96-109">Измените значения hello, в зависимости от среды.</span><span class="sxs-lookup"><span data-stu-id="44e96-109">Change hello values, as appropriate, for your environment.</span></span>

1. <span data-ttu-id="44e96-110">Установка hello [Azure CLI 2.0](/cli/azure/install-az-cli2) если его нет.</span><span class="sxs-lookup"><span data-stu-id="44e96-110">Install hello [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="44e96-111">Создание открытого и закрытого пару ключей SSH для виртуальных машин Linux, выполнив шаги hello в hello [создать открытый и закрытый пару ключей SSH для виртуальных машин Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="44e96-111">Create an SSH public and private key pair for Linux VMs by completing hello steps in hello [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="44e96-112">В командной оболочке входа с помощью команды hello `az login`.</span><span class="sxs-lookup"><span data-stu-id="44e96-112">From a command shell, login with hello command `az login`.</span></span>
4. <span data-ttu-id="44e96-113">Создайте hello виртуальной Машины, выполнив скрипт hello на компьютере Mac или Linux.</span><span class="sxs-lookup"><span data-stu-id="44e96-113">Create hello VM by executing hello script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="44e96-114">Hello скрипт создает группу ресурсов tooit присоединенного одной виртуальной сети (VNet) с двумя подсетями, двумя сетевыми адаптерами и виртуальной Машины с hello двух сетевых адаптеров.</span><span class="sxs-lookup"><span data-stu-id="44e96-114">hello script creates a resource group, one virtual network (VNet) with two subnets, two NICs, and a VM with hello two NICs attached tooit.</span></span> <span data-ttu-id="44e96-115">Одно из hello сетевых адаптеров — подключенных tooone подсети и присваивается статический IP-адрес открытого и закрытого.</span><span class="sxs-lookup"><span data-stu-id="44e96-115">One of hello NICs is connected tooone subnet and is assigned a static public and private IP address.</span></span> <span data-ttu-id="44e96-116">Hello другой сетевой Адаптер имеет подключенного toohello другие подсети и назначается статический частный IP-адрес, а не общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="44e96-116">hello other NIC is connected toohello other subnet and is assigned a static private IP address and no public IP address.</span></span> <span data-ttu-id="44e96-117">Здравствуйте, сетевой Адаптер, общедоступный IP-адрес, виртуальной сети и ресурсы виртуальной Машины должны существовать в hello же местоположение и подписку.</span><span class="sxs-lookup"><span data-stu-id="44e96-117">hello NIC, public IP address, virtual network, and VM resources must all exist in hello same location and subscription.</span></span> <span data-ttu-id="44e96-118">Хотя ресурсы hello все еще нет tooexist в hello одну группу ресурсов, в следующий сценарий, как и hello.</span><span class="sxs-lookup"><span data-stu-id="44e96-118">Though hello resources don't all have tooexist in hello same resource group, in hello following script they do.</span></span>

```bash
#!/bin/sh

RgName="Multi-NIC-VM"
Location="westus"

# Create a resource group.
az group create \
--name $RgName \
--location $Location

# hello address is assigned toohello resource from a pool of IP adresses unique tooeach Azure region. 
# Download and view hello file from https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists
# hello ranges for each region.

PipName="PIP-WEB"
az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--allocation-method Static

# Create a virtual network with one subnet

VnetName="VNet1"
VnetPrefix="10.0.0.0/16"
VnetSubnet1Name="Front-End"
VnetSubnet1Prefix="10.0.0.0/24"
az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $VnetSubnet1Name \
--subnet-prefix $VnetSubnet1Prefix

# Create a second subnet within hello VNet

VnetSubnet2Name="Back-end"
VnetSubnet2Prefix="10.0.1.0/24"
az network vnet subnet create \
--vnet-name $VnetName \
--resource-group $RgName \
--name $VnetSubnet2Name \
--address-prefix $VnetSubnet2Prefix

# Create a network interface connected tooone of hello subnets. hello NIC is assigned a single dynamic private and
# public IP address by default, but you can instead, assign static addresses, or no public IP address at all.
# You can also assign multiple private or public IP addresses tooeach NIC. toolearn more about IP addressing
# options for NICs, enter hello az network nic create -h command.

Nic1Name="NIC-FE"
PrivateIpAddress1="10.0.0.5"

az network nic create \
--name $Nic1Name \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress1 \
--public-ip-address $PipName

# Create a second network interface and connect it toohello other subnet. Though multiple NICs attached toohello same
# VM can be connected toodifferent subnets, hello subnets must all be within hello same VNet. Add additional NICs as necessary.

Nic2Name="NIC-BE"
PrivateIpAddress2="10.0.1.5"

az network nic create \
--name $Nic2Name \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet2Name \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress2

# Create a VM and attach hello two NICs.

VmName="WEB"

# Replace hello value for hello following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article. Not all VM sizes support
# more than one NIC, so be sure tooselect a VM size that supports hello number of NICs you want tooattach toohello VM.
# You must create hello VM with at least two NICs if you want tooadd more after VM creation. If you create a VM with
# only one NIC, you can't add additional NICs toohello VM after VM creation, regardless of how many NICs hello VM supports.
# hello VM size specified in hello following variable supports two NICs.

VmSize="Standard_DS2"

# Replace hello value for hello OsImage variable value with a value for *urn* from hello output returned by entering the
# az vm image list command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace hello following value with hello path tooyour public key file.

SshKeyValue="~/.ssh/id_rsa.pub"

# Before executing hello following command, add variable names of additional NICs you may have added toohello script that
# you want tooattach toohello VM. If creating a Windows VM, remove hello **ssh-key-value** line and you'll be prompted for
# hello password you want tooconfigure for hello VM.

az vm create \
--name $VmName \
--resource-group $RgName \
--image $OsImage \
--location $Location \
--size $VmSize \
--nics $Nic1Name $Nic2Name \
--admin-username $Username \
--ssh-key-value $SshKeyValue
```

<span data-ttu-id="44e96-119">В дополнение к этому toocreating ВМ с двумя сетевыми адаптерами hello скрипт создает:</span><span class="sxs-lookup"><span data-stu-id="44e96-119">In addition toocreating a VM with two NICs, hello script creates:</span></span>
- <span data-ttu-id="44e96-120">Один premium управлять диска по умолчанию, но наличия других параметров для hello тип диска, которые можно создать.</span><span class="sxs-lookup"><span data-stu-id="44e96-120">A single premium managed disk by default, but you have other options for hello disk type you can create.</span></span> <span data-ttu-id="44e96-121">Чтение hello [создания ВМ Linux с помощью Azure CLI 2.0 hello](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Дополнительные сведения см.</span><span class="sxs-lookup"><span data-stu-id="44e96-121">Read hello [Create a Linux VM using hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="44e96-122">Виртуальная сеть с двумя подсетями и одним общедоступным IP-адресом.</span><span class="sxs-lookup"><span data-stu-id="44e96-122">A virtual network with two subnets and a single public IP address.</span></span> <span data-ttu-id="44e96-123">Кроме того, можно использовать *имеющиеся* виртуальные сети, подсети, сетевые карты или общедоступные IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="44e96-123">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="44e96-124">toolearn как toouse существующие сетевые ресурсы, вместо создания дополнительных ресурсов, введите `az vm create -h`.</span><span class="sxs-lookup"><span data-stu-id="44e96-124">toolearn how toouse existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

## <span data-ttu-id="44e96-125"><a name = "validate"></a>Проверка создания виртуальной машины и сетевых карт</span><span class="sxs-lookup"><span data-stu-id="44e96-125"><a name = "validate"></a>Validate VM creation and NICs</span></span>

1. <span data-ttu-id="44e96-126">Введите команду hello `az resource list --resouce-group Multi-NIC-VM --output table` toosee список ресурсов hello создан с помощью сценария hello.</span><span class="sxs-lookup"><span data-stu-id="44e96-126">Enter hello command `az resource list --resouce-group Multi-NIC-VM --output table` toosee a list of hello resources created by hello script.</span></span> <span data-ttu-id="44e96-127">В выходные данные возвращаются hello должно быть шесть ресурсы: два сетевых адаптера, один диск, общедоступный IP-адрес, одну виртуальную сеть и виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="44e96-127">There should be six resources in hello returned output: Two NICs, one disk, one public IP address, one virtual network, and a virtual machine.</span></span>
2. <span data-ttu-id="44e96-128">Введите команду hello `az network public-ip show --name PIP-WEB --resource-group Multi-NIC-VM --output table`.</span><span class="sxs-lookup"><span data-stu-id="44e96-128">Enter hello command `az network public-ip show --name PIP-WEB --resource-group Multi-NIC-VM --output table`.</span></span> <span data-ttu-id="44e96-129">Выходные данные возвращаются hello, обратите внимание, в значение hello **IP-адрес** и что значение hello **PublicIpAllocationMethod** — *статических*.</span><span class="sxs-lookup"><span data-stu-id="44e96-129">In hello returned output, note hello value of **IpAddress** and that hello value of **PublicIpAllocationMethod** is *Static*.</span></span>
3. <span data-ttu-id="44e96-130">Прежде чем запускать следующую команду hello, удалите hello <>, замените *Username* с именем hello, который использовался для hello **Username** переменной в скрипт hello и заменить *IP-адрес* с hello **IP-адрес** из предыдущего шага hello.</span><span class="sxs-lookup"><span data-stu-id="44e96-130">Before running hello following command, remove hello <>, replace *Username* with hello name you used for hello **Username** variable in hello script, and replace *ipAddress* with hello **ipAddress** from hello previous step.</span></span> <span data-ttu-id="44e96-131">Выполнения hello следующая команда tooconnect toohello виртуальной Машины: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span><span class="sxs-lookup"><span data-stu-id="44e96-131">Run hello following command tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span></span> 
4. <span data-ttu-id="44e96-132">После подключения toohello виртуальных Машин, запустите hello `sudo ifconfig` toosee команда *eth0* и *eth1* интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="44e96-132">Once connected toohello VM, run hello `sudo ifconfig` command toosee *eth0* and *eth1* interfaces.</span></span> <span data-ttu-id="44e96-133">Каждый сетевой Адаптер был присвоен hello статических частных IP-адресов указывается в скрипте hello hello Azure DHCP-серверами.</span><span class="sxs-lookup"><span data-stu-id="44e96-133">Each NIC has been assigned hello static private IP addresses specified in hello script by hello Azure DHCP servers.</span></span> <span data-ttu-id="44e96-134">Hello IP- и MAC адресов, назначенных toohello сетевых адаптеров не изменяйте до hello виртуальная машина удаляется.</span><span class="sxs-lookup"><span data-stu-id="44e96-134">hello IP and MAC addresses assigned toohello NICs do not change until hello VM is deleted.</span></span> <span data-ttu-id="44e96-135">Рекомендуется не изменять IP-адреса в операционной системе, как его можно отключить компьютер toohello подключения.</span><span class="sxs-lookup"><span data-stu-id="44e96-135">We recommend that you do not change IP addressing within an operating system, as it can disable connectivity toohello computer.</span></span> <span data-ttu-id="44e96-136">Общедоступные IP-адреса не отображаются в операционной системе hello, как они являются tooand сетевой адрес преобразуется из hello частный IP-адрес с hello инфраструктуры Azure.</span><span class="sxs-lookup"><span data-stu-id="44e96-136">Public IP addresses do not appear within hello operating system, as they are network address translated tooand from hello private IP address by hello Azure infrastructure.</span></span>

## <span data-ttu-id="44e96-137"><a name= "clean-up"></a>Удалите hello ВМ и связанные ресурсы</span><span class="sxs-lookup"><span data-stu-id="44e96-137"><a name= "clean-up"></a>Remove hello VM and associated resources</span></span>

<span data-ttu-id="44e96-138">Рекомендуется удалить hello ресурсы, созданные в этом упражнении, если не использовать их в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="44e96-138">It's recommended that you delete hello resources created in this exercise if you won't use them in production.</span></span> <span data-ttu-id="44e96-139">За виртуальную машину, общедоступный IP-адрес и диск взимается плата, пока они подготовлены.</span><span class="sxs-lookup"><span data-stu-id="44e96-139">VM, public IP address, and disk resources incur charges, as long as they're provisioned.</span></span> <span data-ttu-id="44e96-140">tooremove hello ресурсы, созданные во время этого упражнения завершения hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="44e96-140">tooremove hello resources created during this exercise, complete hello following steps:</span></span>
1. <span data-ttu-id="44e96-141">tooview hello ресурсы в группе ресурсов hello, запустите hello `az resource list --resource-group Multi-NIC-VM` команды.</span><span class="sxs-lookup"><span data-stu-id="44e96-141">tooview hello resources in hello resource group, run hello `az resource list --resource-group Multi-NIC-VM` command.</span></span>
2. <span data-ttu-id="44e96-142">Убедитесь, что нет ресурсов в группе ресурсов hello, за исключением hello ресурсов создан с помощью сценария hello в этой статье.</span><span class="sxs-lookup"><span data-stu-id="44e96-142">Confirm there are no resources in hello resource group, other than hello resources created by hello script in this article.</span></span> 
3. <span data-ttu-id="44e96-143">все ресурсы, созданные в этом упражнении запуска hello toodelete `az group delete --name Multi-NIC-VM` команды.</span><span class="sxs-lookup"><span data-stu-id="44e96-143">toodelete all resources created in this exercise, run hello `az group delete --name Multi-NIC-VM` command.</span></span> <span data-ttu-id="44e96-144">Hello команда удаляет группу ресурсов hello и все ресурсы hello, содержащихся в нем.</span><span class="sxs-lookup"><span data-stu-id="44e96-144">hello command deletes hello resource group and all hello resources it contains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44e96-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="44e96-145">Next steps</span></span>

<span data-ttu-id="44e96-146">Любой сетевой трафик могут передаваться tooand из hello создания виртуальной Машины в этой статье.</span><span class="sxs-lookup"><span data-stu-id="44e96-146">Any network traffic can flow tooand from hello VM created in this article.</span></span> <span data-ttu-id="44e96-147">Можно определить правила входящих и исходящих подключений в NSG, ограничить объем трафика hello, который может осуществляться tooand из каждого сетевого интерфейса и/или в каждой подсети.</span><span class="sxs-lookup"><span data-stu-id="44e96-147">You can define inbound and outbound rules within an NSG that limit hello traffic that can flow tooand from each network interface, each subnet, or both.</span></span> <span data-ttu-id="44e96-148">Дополнительные сведения о Nsg, чтение hello toolearn [NSG Обзор](virtual-networks-nsg.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="44e96-148">toolearn more about NSGs, read hello [NSG overview](virtual-networks-nsg.md) article.</span></span>
