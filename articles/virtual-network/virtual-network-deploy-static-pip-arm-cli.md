---
title: "aaaCreate виртуальную Машину с статический общедоступный IP-адрес - CLI Azure 2.0 | Документы Microsoft"
description: "Узнайте, как toocreate ВМ с статических открытый IP адрес с помощью hello Azure командной строки (CLI) 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 55bc21b0-2a45-4943-a5e7-8d785d0d015c
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 486060463486462dd8336734a7ad23c4a2cba452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-cli-20"></a><span data-ttu-id="53697-103">Создайте виртуальную Машину с помощью hello Azure CLI 2.0 статический общедоступный IP-адрес</span><span class="sxs-lookup"><span data-stu-id="53697-103">Create a VM with a static public IP address using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="53697-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="53697-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="53697-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="53697-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="53697-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="53697-106">Azure CLI 2.0</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="53697-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="53697-107">Azure CLI 1.0</span></span>](virtual-network-deploy-static-pip-cli-nodejs.md)
> * [<span data-ttu-id="53697-108">Шаблон</span><span class="sxs-lookup"><span data-stu-id="53697-108">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="53697-109">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="53697-109">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

<span data-ttu-id="53697-110">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="53697-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="53697-111">В этой статье описан с помощью модели развертывания диспетчера ресурсов hello, который рекомендуется в большинстве случаев новый вместо hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="53697-111">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <span data-ttu-id="53697-112"><a name = "create"></a>Создание виртуальной Машины hello</span><span class="sxs-lookup"><span data-stu-id="53697-112"><a name = "create"></a>Create hello VM</span></span>

<span data-ttu-id="53697-113">Выполнить эту задачу с помощью hello Azure CLI 2.0 (Эта статья) или hello [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="53697-113">You can complete this task using hello Azure CLI 2.0 (this article) or hello [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md).</span></span> <span data-ttu-id="53697-114">Здравствуйте, значения в «» для переменных hello в hello описанных ниже создать ресурсы с параметрами из сценария hello.</span><span class="sxs-lookup"><span data-stu-id="53697-114">hello values in "" for hello variables in hello steps that follow create resources with settings from hello scenario.</span></span> <span data-ttu-id="53697-115">Измените значения hello, в зависимости от среды.</span><span class="sxs-lookup"><span data-stu-id="53697-115">Change hello values, as appropriate, for your environment.</span></span>

1. <span data-ttu-id="53697-116">Установка hello [Azure CLI 2.0](/cli/azure/install-az-cli2) если его нет.</span><span class="sxs-lookup"><span data-stu-id="53697-116">Install hello [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="53697-117">Создание открытого и закрытого пару ключей SSH для виртуальных машин Linux, выполнив шаги hello в hello [создать открытый и закрытый пару ключей SSH для виртуальных машин Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="53697-117">Create an SSH public and private key pair for Linux VMs by completing hello steps in hello [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="53697-118">В командной оболочке входа с помощью команды hello `az login`.</span><span class="sxs-lookup"><span data-stu-id="53697-118">From a command shell, login with hello command `az login`.</span></span>
4. <span data-ttu-id="53697-119">Создайте hello виртуальной Машины, выполнив скрипт hello на компьютере Mac или Linux.</span><span class="sxs-lookup"><span data-stu-id="53697-119">Create hello VM by executing hello script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="53697-120">Hello Azure общедоступный IP-адрес, виртуальная сеть, сетевой интерфейс и ресурсы виртуальной Машины должны существовать в hello же расположение.</span><span class="sxs-lookup"><span data-stu-id="53697-120">hello Azure public IP address, virtual network, network interface, and VM resources must all exist in hello same location.</span></span> <span data-ttu-id="53697-121">Хотя ресурсы hello все еще нет tooexist в hello одну группу ресурсов, в следующий сценарий, как и hello.</span><span class="sxs-lookup"><span data-stu-id="53697-121">Though hello resources don't all have tooexist in hello same resource group, in hello following script they do.</span></span>

```bash
RgName="IaaSStory"
Location="westus"

# Create a resource group.

az group create \
--name $RgName \
--location $Location

# Create a public IP address resource with a static IP address using hello --allocation-method Static option.
# If you do not specify this option, hello address is allocated dynamically. hello address is assigned toothe
# resource from a pool of IP adresses unique tooeach Azure region. hello DnsName must be unique within the
# Azure location it's created in. Download and view hello file from https://www.microsoft.com/en-us/download/details.aspx?id=41653#
# that lists hello ranges for each region.

PipName="PIPWEB1"
DnsName="iaasstoryws1"
az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--allocation-method Static \
--dns-name $DnsName

# Create a virtual network with one subnet

VnetName="TestVNet"
VnetPrefix="192.168.0.0/16"
SubnetName="FrontEnd"
SubnetPrefix="192.168.1.0/24"
az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $SubnetName \
--subnet-prefix $SubnetPrefix

# Create a network interface connected toohello VNet with a static private IP address and associate hello public IP address
# resource toohello NIC.

NicName="NICWEB1"
PrivateIpAddress="192.168.1.101"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $SubnetName \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress \
--public-ip-address $PipName

# Create a new VM with hello NIC

VmName="WEB1"

# Replace hello value for hello VmSize variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article.
VmSize="Standard_DS1"

# Replace hello value for hello OsImage variable with a value for *urn* from hello output returned by entering
# hello `az vm image list` command. 

OsImage="credativ:Debian:8:latest"
Username='adminuser'

# Replace hello following value with hello path tooyour public key file.
SshKeyValue="~/.ssh/id_rsa.pub"

az vm create \
--name $VmName \
--resource-group $RgName \
--image $OsImage \
--location $Location \
--size $VmSize \
--nics $NicName \
--admin-username $Username \
--ssh-key-value $SshKeyValue
# If creating a Windows VM, remove hello previous line and you'll be prompted for hello password you want tooconfigure for hello VM.
```

<span data-ttu-id="53697-122">В дополнение к этому toocreating ВМ hello скрипт создает:</span><span class="sxs-lookup"><span data-stu-id="53697-122">In addition toocreating a VM, hello script creates:</span></span>
- <span data-ttu-id="53697-123">Один premium управлять диска по умолчанию, но наличия других параметров для hello тип диска, которые можно создать.</span><span class="sxs-lookup"><span data-stu-id="53697-123">A single premium managed disk by default, but you have other options for hello disk type you can create.</span></span> <span data-ttu-id="53697-124">Чтение hello [создания ВМ Linux с помощью Azure CLI 2.0 hello](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Дополнительные сведения см.</span><span class="sxs-lookup"><span data-stu-id="53697-124">Read hello [Create a Linux VM using hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="53697-125">Виртуальная сеть, подсеть, сетевая карта и общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="53697-125">Virtual network, subnet, NIC, and public IP address resources.</span></span> <span data-ttu-id="53697-126">Кроме того, можно использовать *имеющиеся* виртуальные сети, подсети, сетевые карты или общедоступные IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="53697-126">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="53697-127">toolearn как toouse существующие сетевые ресурсы, вместо создания дополнительных ресурсов, введите `az vm create -h`.</span><span class="sxs-lookup"><span data-stu-id="53697-127">toolearn how toouse existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

## <span data-ttu-id="53697-128"><a name = "validate"></a>Проверка создания виртуальной машины и общедоступного IP-адреса</span><span class="sxs-lookup"><span data-stu-id="53697-128"><a name = "validate"></a>Validate VM creation and public IP address</span></span>

1. <span data-ttu-id="53697-129">Введите команду hello `az resource list --resouce-group IaaSStory --output table` toosee список ресурсов hello создан с помощью сценария hello.</span><span class="sxs-lookup"><span data-stu-id="53697-129">Enter hello command `az resource list --resouce-group IaaSStory --output table` toosee a list of hello resources created by hello script.</span></span> <span data-ttu-id="53697-130">В выходные данные возвращаются hello должно быть пять ресурсы: сетевого интерфейса, диск, общедоступный IP-адрес, виртуальной сети и виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="53697-130">There should be five resources in hello returned output: network interface, disk, public IP address, virtual network, and a virtual machine.</span></span>
2. <span data-ttu-id="53697-131">Введите команду hello `az network public-ip show --name PIPWEB1 --resource-group IaaSStory --output table`.</span><span class="sxs-lookup"><span data-stu-id="53697-131">Enter hello command `az network public-ip show --name PIPWEB1 --resource-group IaaSStory --output table`.</span></span> <span data-ttu-id="53697-132">Выходные данные возвращаются hello, обратите внимание, в значение hello **IP-адрес** и что значение hello **PublicIpAllocationMethod** — *статических*.</span><span class="sxs-lookup"><span data-stu-id="53697-132">In hello returned output, note hello value of **IpAddress** and that hello value of **PublicIpAllocationMethod** is *Static*.</span></span>
3. <span data-ttu-id="53697-133">Перед выполнением hello следующую команду, удалите hello <>, замените *Username* с именем hello, который использовался для hello **Username** переменных в скрипт hello и заменить *IP-адрес* с hello **IP-адрес** из предыдущего шага hello.</span><span class="sxs-lookup"><span data-stu-id="53697-133">Before executing hello following command, remove hello <>, replace *Username* with hello name you used for hello **Username** variable in hello script, and replace *ipAddress* with hello **ipAddress** from hello previous step.</span></span> <span data-ttu-id="53697-134">Выполнения hello следующая команда tooconnect toohello виртуальной Машины: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span><span class="sxs-lookup"><span data-stu-id="53697-134">Run hello following command tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span></span> 

## <span data-ttu-id="53697-135"><a name= "clean-up"></a>Удалите hello ВМ и связанные ресурсы</span><span class="sxs-lookup"><span data-stu-id="53697-135"><a name= "clean-up"></a>Remove hello VM and associated resources</span></span>

<span data-ttu-id="53697-136">Рекомендуется удалить hello ресурсы, созданные в этом упражнении, если не использовать их в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="53697-136">It's recommended that you delete hello resources created in this exercise if you won't use them in production.</span></span> <span data-ttu-id="53697-137">За виртуальную машину, общедоступный IP-адрес и диск взимается плата, пока они подготовлены.</span><span class="sxs-lookup"><span data-stu-id="53697-137">VM, public IP address, and disk resources incur charges, as long as they're provisioned.</span></span> <span data-ttu-id="53697-138">tooremove hello ресурсы, созданные во время этого упражнения завершения hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="53697-138">tooremove hello resources created during this exercise, complete hello following steps:</span></span>

1. <span data-ttu-id="53697-139">tooview hello ресурсы в группе ресурсов hello, запустите hello `az resource list --resource-group IaaSStory` команды.</span><span class="sxs-lookup"><span data-stu-id="53697-139">tooview hello resources in hello resource group, run hello `az resource list --resource-group IaaSStory` command.</span></span>
2. <span data-ttu-id="53697-140">Убедитесь, что нет ресурсов в группе ресурсов hello, за исключением hello ресурсов создан с помощью сценария hello в этой статье.</span><span class="sxs-lookup"><span data-stu-id="53697-140">Confirm there are no resources in hello resource group, other than hello resources created by hello script in this article.</span></span> 
3. <span data-ttu-id="53697-141">все ресурсы, созданные в этом упражнении запуска hello toodelete `az group delete -n IaaSStory` команды.</span><span class="sxs-lookup"><span data-stu-id="53697-141">toodelete all resources created in this exercise, run hello `az group delete -n IaaSStory` command.</span></span> <span data-ttu-id="53697-142">Hello команда удаляет группу ресурсов hello и все ресурсы hello, содержащихся в нем.</span><span class="sxs-lookup"><span data-stu-id="53697-142">hello command deletes hello resource group and all hello resources it contains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="53697-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="53697-143">Next steps</span></span>

<span data-ttu-id="53697-144">Любой сетевой трафик могут передаваться tooand из hello создания виртуальной Машины в этой статье.</span><span class="sxs-lookup"><span data-stu-id="53697-144">Any network traffic can flow tooand from hello VM created in this article.</span></span> <span data-ttu-id="53697-145">Можно определить правила входящих и исходящих подключений в NSG, ограничить объем трафика hello, который может осуществляться tooand из сетевого интерфейса hello и подсети hello.</span><span class="sxs-lookup"><span data-stu-id="53697-145">You can define inbound and outbound rules within an NSG that limit hello traffic that can flow tooand from hello network interface, hello subnet, or both.</span></span> <span data-ttu-id="53697-146">Дополнительные сведения о Nsg, чтение hello toolearn [NSG Обзор](virtual-networks-nsg.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="53697-146">toolearn more about NSGs, read hello [NSG overview](virtual-networks-nsg.md) article.</span></span>
