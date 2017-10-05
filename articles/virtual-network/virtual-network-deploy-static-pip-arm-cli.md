---
title: "Создание виртуальной машины со статическим общедоступным IP-адресом (Azure CLI 2.0) | Документация Майкрософт"
description: "Узнайте, как создать виртуальную машину со статическим общедоступным IP-адресом с помощью интерфейса командной строки Azure (CLI) версии 2.0."
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
ms.openlocfilehash: a4c32694949880037f01bb2b6b9779d2cbb9809c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-the-azure-cli-20"></a><span data-ttu-id="64ded-103">Создание виртуальной машины со статическим общедоступным IP-адресом с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="64ded-103">Create a VM with a static public IP address using the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="64ded-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="64ded-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="64ded-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="64ded-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="64ded-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="64ded-106">Azure CLI 2.0</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="64ded-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="64ded-107">Azure CLI 1.0</span></span>](virtual-network-deploy-static-pip-cli-nodejs.md)
> * [<span data-ttu-id="64ded-108">Шаблон</span><span class="sxs-lookup"><span data-stu-id="64ded-108">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="64ded-109">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="64ded-109">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

<span data-ttu-id="64ded-110">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="64ded-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="64ded-111">В этой статье описывается использование модели развертывания c помощью Resource Manager. Для большинства новых развертываний мы рекомендуем использовать эту модель вместо классической.</span><span class="sxs-lookup"><span data-stu-id="64ded-111">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <span data-ttu-id="64ded-112"><a name = "create"></a>Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="64ded-112"><a name = "create"></a>Create the VM</span></span>

<span data-ttu-id="64ded-113">Эту задачу можно выполнить с помощью Azure CLI 2.0 (в этой статье) или [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="64ded-113">You can complete this task using the Azure CLI 2.0 (this article) or the [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md).</span></span> <span data-ttu-id="64ded-114">Значения в прямых кавычках для переменных в последующих шагах позволяют создать ресурсы с параметрами из сценария.</span><span class="sxs-lookup"><span data-stu-id="64ded-114">The values in "" for the variables in the steps that follow create resources with settings from the scenario.</span></span> <span data-ttu-id="64ded-115">Подставьте соответствующие значения для своей среды.</span><span class="sxs-lookup"><span data-stu-id="64ded-115">Change the values, as appropriate, for your environment.</span></span>

1. <span data-ttu-id="64ded-116">Установите [Azure CLI 2.0](/cli/azure/install-az-cli2), если вы еще этого не сделали.</span><span class="sxs-lookup"><span data-stu-id="64ded-116">Install the [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="64ded-117">Создайте пару открытого и закрытого ключей SSH для виртуальных машин Linux, выполнив действия, описанные в [этой статье](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="64ded-117">Create an SSH public and private key pair for Linux VMs by completing the steps in the [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="64ded-118">Выполните вход из командной оболочки с помощью команды `az login`.</span><span class="sxs-lookup"><span data-stu-id="64ded-118">From a command shell, login with the command `az login`.</span></span>
4. <span data-ttu-id="64ded-119">Создайте виртуальную машину, выполнив следующий скрипт на компьютере Mac или Linux.</span><span class="sxs-lookup"><span data-stu-id="64ded-119">Create the VM by executing the script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="64ded-120">Общедоступный IP-адрес Azure, виртуальная сеть, сетевой интерфейс и виртуальная машина должны находиться в одном расположении.</span><span class="sxs-lookup"><span data-stu-id="64ded-120">The Azure public IP address, virtual network, network interface, and VM resources must all exist in the same location.</span></span> <span data-ttu-id="64ded-121">Хотя эти ресурсы и не должны находиться в одной группе ресурсов, в следующем скрипте они находятся в одной группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="64ded-121">Though the resources don't all have to exist in the same resource group, in the following script they do.</span></span>

```bash
RgName="IaaSStory"
Location="westus"

# Create a resource group.

az group create \
--name $RgName \
--location $Location

# Create a public IP address resource with a static IP address using the --allocation-method Static option.
# If you do not specify this option, the address is allocated dynamically. The address is assigned to the
# resource from a pool of IP adresses unique to each Azure region. The DnsName must be unique within the
# Azure location it's created in. Download and view the file from https://www.microsoft.com/en-us/download/details.aspx?id=41653#
# that lists the ranges for each region.

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

# Create a network interface connected to the VNet with a static private IP address and associate the public IP address
# resource to the NIC.

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

# Create a new VM with the NIC

VmName="WEB1"

# Replace the value for the VmSize variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article.
VmSize="Standard_DS1"

# Replace the value for the OsImage variable with a value for *urn* from the output returned by entering
# the `az vm image list` command. 

OsImage="credativ:Debian:8:latest"
Username='adminuser'

# Replace the following value with the path to your public key file.
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
# If creating a Windows VM, remove the previous line and you'll be prompted for the password you want to configure for the VM.
```

<span data-ttu-id="64ded-122">Помимо виртуальной машины скрипт также создает следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="64ded-122">In addition to creating a VM, the script creates:</span></span>
- <span data-ttu-id="64ded-123">Один управляемый диск уровня "Премиум" по умолчанию. Вы можете создать диск другого типа.</span><span class="sxs-lookup"><span data-stu-id="64ded-123">A single premium managed disk by default, but you have other options for the disk type you can create.</span></span> <span data-ttu-id="64ded-124">Дополнительные сведения см. в статье [Создание виртуальной машины Linux с помощью предварительной версии Azure CLI 2.0 (az.py)](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="64ded-124">Read the [Create a Linux VM using the Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="64ded-125">Виртуальная сеть, подсеть, сетевая карта и общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="64ded-125">Virtual network, subnet, NIC, and public IP address resources.</span></span> <span data-ttu-id="64ded-126">Кроме того, можно использовать *имеющиеся* виртуальные сети, подсети, сетевые карты или общедоступные IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="64ded-126">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="64ded-127">Чтобы узнать, как использовать имеющиеся сетевые ресурсы, а не создавать дополнительные, введите `az vm create -h`.</span><span class="sxs-lookup"><span data-stu-id="64ded-127">To learn how to use existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

## <span data-ttu-id="64ded-128"><a name = "validate"></a>Проверка создания виртуальной машины и общедоступного IP-адреса</span><span class="sxs-lookup"><span data-stu-id="64ded-128"><a name = "validate"></a>Validate VM creation and public IP address</span></span>

1. <span data-ttu-id="64ded-129">Введите команду `az resource list --resouce-group IaaSStory --output table`, чтобы просмотреть список ресурсов, созданных с помощью скрипта.</span><span class="sxs-lookup"><span data-stu-id="64ded-129">Enter the command `az resource list --resouce-group IaaSStory --output table` to see a list of the resources created by the script.</span></span> <span data-ttu-id="64ded-130">В результате должно отобразиться пять ресурсов: сетевой интерфейс, диск, общедоступный IP-адрес, виртуальная сеть и виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="64ded-130">There should be five resources in the returned output: network interface, disk, public IP address, virtual network, and a virtual machine.</span></span>
2. <span data-ttu-id="64ded-131">Введите команду `az network public-ip show --name PIPWEB1 --resource-group IaaSStory --output table`.</span><span class="sxs-lookup"><span data-stu-id="64ded-131">Enter the command `az network public-ip show --name PIPWEB1 --resource-group IaaSStory --output table`.</span></span> <span data-ttu-id="64ded-132">В возвращенных выходных данных обратите внимание на значение параметра **IpAddress**, а также на то, что параметр **PublicIpAllocationMethod** имеет значение *Static*.</span><span class="sxs-lookup"><span data-stu-id="64ded-132">In the returned output, note the value of **IpAddress** and that the value of **PublicIpAllocationMethod** is *Static*.</span></span>
3. <span data-ttu-id="64ded-133">Перед выполнением следующей команды удалите <> и замените *Username* именем, использованным для переменной **Username** в скрипте, а *ipAddress* — **IP-адресом** из предыдущего шага.</span><span class="sxs-lookup"><span data-stu-id="64ded-133">Before executing the following command, remove the <>, replace *Username* with the name you used for the **Username** variable in the script, and replace *ipAddress* with the **ipAddress** from the previous step.</span></span> <span data-ttu-id="64ded-134">Выполните следующую команду для подключения к виртуальной машине: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span><span class="sxs-lookup"><span data-stu-id="64ded-134">Run the following command to connect to the VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span></span> 

## <span data-ttu-id="64ded-135"><a name= "clean-up"></a>Удаление виртуальной машины и связанных с ней ресурсов</span><span class="sxs-lookup"><span data-stu-id="64ded-135"><a name= "clean-up"></a>Remove the VM and associated resources</span></span>

<span data-ttu-id="64ded-136">Если вы не планируете использовать в рабочей среде ресурсы, созданные во время этого упражнения, рекомендуется удалить их.</span><span class="sxs-lookup"><span data-stu-id="64ded-136">It's recommended that you delete the resources created in this exercise if you won't use them in production.</span></span> <span data-ttu-id="64ded-137">За виртуальную машину, общедоступный IP-адрес и диск взимается плата, пока они подготовлены.</span><span class="sxs-lookup"><span data-stu-id="64ded-137">VM, public IP address, and disk resources incur charges, as long as they're provisioned.</span></span> <span data-ttu-id="64ded-138">Чтобы удалить ресурсы, созданные во время этого упражнения, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="64ded-138">To remove the resources created during this exercise, complete the following steps:</span></span>

1. <span data-ttu-id="64ded-139">Выполните команду `az resource list --resource-group IaaSStory`, чтобы просмотреть ресурсы в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="64ded-139">To view the resources in the resource group, run the `az resource list --resource-group IaaSStory` command.</span></span>
2. <span data-ttu-id="64ded-140">Убедитесь, что в ней содержатся только ресурсы, созданные с помощью сценария в этой статье.</span><span class="sxs-lookup"><span data-stu-id="64ded-140">Confirm there are no resources in the resource group, other than the resources created by the script in this article.</span></span> 
3. <span data-ttu-id="64ded-141">Чтобы удалить все ресурсы, созданные во время этого упражнения, выполните команду `az group delete -n IaaSStory`.</span><span class="sxs-lookup"><span data-stu-id="64ded-141">To delete all resources created in this exercise, run the `az group delete -n IaaSStory` command.</span></span> <span data-ttu-id="64ded-142">Эта команда удаляет группу ресурсов и все содержащиеся в ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="64ded-142">The command deletes the resource group and all the resources it contains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64ded-143">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="64ded-143">Next steps</span></span>

<span data-ttu-id="64ded-144">Виртуальная машина, созданная в этой статье, может принимать и передавать любой сетевой трафик.</span><span class="sxs-lookup"><span data-stu-id="64ded-144">Any network traffic can flow to and from the VM created in this article.</span></span> <span data-ttu-id="64ded-145">Вы можете определить правила, ограничивающие входящий и исходящий трафик в группе безопасности сети для сетевого интерфейса, подсети или для того и другого.</span><span class="sxs-lookup"><span data-stu-id="64ded-145">You can define inbound and outbound rules within an NSG that limit the traffic that can flow to and from the network interface, the subnet, or both.</span></span> <span data-ttu-id="64ded-146">Дополнительные сведения о группах безопасности сети см. в [этой статье](virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="64ded-146">To learn more about NSGs, read the [NSG overview](virtual-networks-nsg.md) article.</span></span>