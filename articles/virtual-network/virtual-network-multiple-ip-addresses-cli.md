---
title: "Виртуальная машина с несколькими сетевыми картами (Azure CLI 2.0) | Документация Майкрософт"
description: "Назначение виртуальной машине нескольких IP-адресов с помощью Azure CLI 2.0 | Resource Manager"
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/17/2016
ms.author: annahar
ms.openlocfilehash: 0e9b2ef89ca39a7988a7b2573496a605dfc604b4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="assign-multiple-ip-addresses-to-virtual-machines-using-the-azure-cli-20"></a><span data-ttu-id="c6fc0-103">Назначение виртуальным машинам нескольких IP-адресов с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c6fc0-103">Assign multiple IP addresses to virtual machines using the Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="c6fc0-104">В этой статье описывается создание виртуальной машины с помощью модели развертывания Azure Resource Manager с использованием Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-104">This article explains how to create a virtual machine (VM) through the Azure Resource Manager deployment model using the Azure CLI 2.0.</span></span> <span data-ttu-id="c6fc0-105">Для ресурсов, созданных с помощью классической модели развертывания, нельзя назначить несколько IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-105">Multiple IP addresses cannot be assigned to resources created through the classic deployment model.</span></span> <span data-ttu-id="c6fc0-106">Дополнительные сведения о моделях развертывания Azure см. в статье [Azure Resource Manager vs. classic deployment: Understand deployment models and the state of your resources](../resource-manager-deployment-model.md) (Развертывание с помощью Azure Resource Manager и классическое развертывание. Общие сведения о моделях развертывания и состоянии ресурсов).</span><span class="sxs-lookup"><span data-stu-id="c6fc0-106">To learn more about Azure deployment models, read the [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="c6fc0-107"><a name = "create"></a>Создание виртуальной машины с несколькими IP-адресами</span><span class="sxs-lookup"><span data-stu-id="c6fc0-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="c6fc0-108">Эту задачу можно выполнить с помощью Azure CLI 2.0 (в этой статье) или [Azure CLI 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="c6fc0-108">You can complete this task using the Azure CLI 2.0 (this article) or the [Azure CLI 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md).</span></span> <span data-ttu-id="c6fc0-109">Подставьте соответствующие значения для своей среды.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-109">Change the values, as appropriate, for your environment.</span></span> <span data-ttu-id="c6fc0-110">Вы можете создать пример виртуальной машины с несколькими IP-адресами, как описано в нашем сценарии.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-110">The steps that follow explain how to create an example VM with multiple IP addresses, as described in the scenario.</span></span> <span data-ttu-id="c6fc0-111">Измените имена переменных в прямых кавычках и типы IP-адресов в соответствии с требованиями своей реализации.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-111">Change variable values in "" and IP address types as required for your implementation.</span></span> 

1. <span data-ttu-id="c6fc0-112">Установите [Azure CLI 2.0](/cli/azure/install-az-cli2), если вы еще этого не сделали.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-112">Install the [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="c6fc0-113">Создайте пару открытого и закрытого ключей SSH для виртуальных машин Linux, выполнив действия, описанные в [этой статье](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c6fc0-113">Create an SSH public and private key pair for Linux VMs by completing the steps in the [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="c6fc0-114">Выполните вход из командной оболочки, применив команду `az login`, и выберите используемую подписку.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-114">From a command shell, login with the command `az login` and select the subscription you're using.</span></span>
4. <span data-ttu-id="c6fc0-115">Создайте виртуальную машину, выполнив следующий скрипт на компьютере Mac или Linux.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-115">Create the VM by executing the script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="c6fc0-116">Скрипт создает группу ресурсов, одну виртуальную сеть, одну сетевую карту с тремя конфигурациями IP-адреса и виртуальную машину с двумя подключенными сетевыми картами.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-116">The script creates a resource group, one virtual network (VNet), one NIC with three IP configurations, and a VM with the two NICs attached to it.</span></span> <span data-ttu-id="c6fc0-117">Сетевая карта, общедоступный IP-адрес, виртуальная сеть и виртуальная машина должны находиться в одном расположении и в одной подписке.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-117">The NIC, public IP address, virtual network, and VM resources must all exist in the same location and subscription.</span></span> <span data-ttu-id="c6fc0-118">Хотя эти ресурсы и не должны находиться в одной группе ресурсов, в следующем скрипте они находятся в одной группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-118">Though the resources don't all have to exist in the same resource group, in the following script they do.</span></span>

```bash
    
#!/bin/sh
    
RgName="myResourceGroup"
Location="westcentralus"
az group create --name $RgName --location $Location
    
# Create a public IP address resource with a static IP address using the `--allocation-method Static` option. If you
# do not specify this option, the address is allocated dynamically. The address is assigned to the resource from a pool
# of IP adresses unique to each Azure region. Download and view the file from
# https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists the ranges for each region.

PipName="myPublicIP"

# This name must be unique within an Azure location.
DnsName="myDNSName"

az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--dns-name $DnsName\
--allocation-method Static

# Create a virtual network with one subnet

VnetName="myVnet"
VnetPrefix="10.0.0.0/16"
VnetSubnetName="mySubnet"
VnetSubnetPrefix="10.0.0.0/24"

az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $VnetSubnetName \
--subnet-prefix $VnetSubnetPrefix

# Create a network interface connected to the subnet and associate the public IP address to it. Azure will create the
# first IP configuration with a static private IP address and will associate the public IP address resource to it.

NicName="MyNic1"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--private-ip-address 10.0.0.4
--vnet-name $VnetName \
--public-ip-address $PipName
    
# Create a second public IP address, a second IP configuration, and associate it to the NIC. This configuration has a
# static public IP address and a static private IP address.

az network public-ip create \
--resource-group $RgName \
--location $Location \
--name myPublicIP2 \
--dns-name mypublicdns2 \
--allocation-method Static

az network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--name IPConfig-2 \
--private-ip-address 10.0.0.5 \
--public-ip-name myPublicIP2

# Create a third IP configuration, and associate it to the NIC. This configuration has  static private IP address and   # no public IP address.

azure network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--private-ip-address 10.0.0.6 \
--name IPConfig-3

# Note: Though this article assigns all IP configurations to a single NIC, you can also assign multiple IP configurations
# to any NIC in a VM. To learn how to create a VM with multiple NICs, read the Create a VM with multiple NICs 
# article: https://docs.microsoft.com/azure/virtual-network/virtual-network-deploy-multinic-arm-cli.

# Create a VM and attach the NIC.

VmName="myVm"

# Replace the value for the following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes rticle. The script fails if the VM size
# is not supported in the location you select. Run the `azure vm sizes --location estcentralus` command to get a full list
# of VMs in US West Central, for example.

VmSize="Standard_DS1"

# Replace the value for the OsImage variable value with a value for *urn* from the utput returned by entering the
# `az vm image list` command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace the following value with the path to your public key file. If you're creating a Windows VM, remove the following
# line and you'll be prompted for the password you want to configure for the VM.

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
```

<span data-ttu-id="c6fc0-119">Помимо виртуальной машины с сетевой картой и конфигураций из трех IP-адресов сценарий также создает следующие ресурсы.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-119">In addition to creating a VM with a NIC with 3 IP configurations, the script creates:</span></span>

- <span data-ttu-id="c6fc0-120">Один управляемый диск уровня "Премиум" по умолчанию. Вы можете создать диск другого типа.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-120">A single premium managed disk by default, but you have other options for the disk type you can create.</span></span> <span data-ttu-id="c6fc0-121">Дополнительные сведения см. в статье [Создание виртуальной машины Linux с помощью предварительной версии Azure CLI 2.0 (az.py)](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c6fc0-121">Read the [Create a Linux VM using the Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="c6fc0-122">Виртуальная сеть с одной подсетью и двумя общедоступными IP-адресами.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-122">A virtual network with one subnet and two public IP addresses.</span></span> <span data-ttu-id="c6fc0-123">Кроме того, можно использовать *имеющиеся* виртуальные сети, подсети, сетевые карты или общедоступные IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-123">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="c6fc0-124">Чтобы узнать, как использовать имеющиеся сетевые ресурсы, а не создавать дополнительные, введите `az vm create -h`.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-124">To learn how to use existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

<span data-ttu-id="c6fc0-125">За общедоступные IP-адреса взимается номинальная плата.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-125">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="c6fc0-126">Дополнительные сведения о ценах на IP-адреса см. на странице [Цены на IP-адреса](https://azure.microsoft.com/pricing/details/ip-addresses).</span><span class="sxs-lookup"><span data-stu-id="c6fc0-126">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="c6fc0-127">Число общедоступных IP-адресов, которые можно использовать в одной подписке, ограничено.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-127">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="c6fc0-128">Сведения об ограничениях см. в статье [Подписка Azure, границы, квоты и ограничения службы](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="c6fc0-128">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

<span data-ttu-id="c6fc0-129">Создав виртуальную машину, введите команду `az network nic show --name MyNic1 --resource-group myResourceGroup`, чтобы просмотреть конфигурацию сетевой карты.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-129">After the VM is created, enter the `az network nic show --name MyNic1 --resource-group myResourceGroup` command to view the NIC configuration.</span></span> <span data-ttu-id="c6fc0-130">Введите команду `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` для просмотра списка конфигураций IP-адресов, связанных с сетевой картой.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-130">Enter the `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` to view a list of the IP configurations associated to the NIC.</span></span>

<span data-ttu-id="c6fc0-131">Добавьте в операционную систему виртуальной машины частные IP-адреса, выполнив действия, соответствующие вашей операционной системе, как описано в разделе [Добавление IP-адресов в операционную систему виртуальной машины](#os-config) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-131">Add the private IP addresses to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span>

## <span data-ttu-id="c6fc0-132"><a name="add"></a>Добавление IP-адресов в виртуальную машину</span><span class="sxs-lookup"><span data-stu-id="c6fc0-132"><a name="add"></a>Add IP addresses to a VM</span></span>

<span data-ttu-id="c6fc0-133">Выполнив следующие шаги, вы сможете назначить дополнительные частные или общедоступные IP-адреса существующим сетевым адаптерам.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-133">You can add additional private and public IP addresses to an existing NIC by completing the steps that follow.</span></span> <span data-ttu-id="c6fc0-134">Примеры созданы на основе [сценария](#Scenario), описанного в этой статье.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-134">The examples build upon the [scenario](#Scenario) described in this article.</span></span>

1. <span data-ttu-id="c6fc0-135">Откройте командную оболочку и в рамках одного сеанса командной строки выполните все действия, описанные в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-135">Open a command shell and complete the remaining steps in this section within a single session.</span></span> <span data-ttu-id="c6fc0-136">Если Azure CLI еще не установлен и не настроен, выполните инструкции из статьи по [установке Azure CLI 2.0](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json), а затем войдите в учетную запись Azure, выполнив команду `az-login`.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-136">If you don't already have Azure CLI installed and configured, complete the steps in the [Azure CLI 2.0 installation](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json) article and login to your Azure account with the `az-login` command.</span></span>

2. <span data-ttu-id="c6fc0-137">Выполните действия, описанные в одном из следующих разделов, с учетом задач.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-137">Complete the steps in one of the following sections, based on your requirements:</span></span>

    <span data-ttu-id="c6fc0-138">**Добавление частного IP-адреса**</span><span class="sxs-lookup"><span data-stu-id="c6fc0-138">**Add a private IP address**</span></span>
    
    <span data-ttu-id="c6fc0-139">Чтобы добавить к сетевой карте частный IP-адрес, создайте конфигурацию IP-адресов с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-139">To add a private IP address to a NIC, you must create an IP configuration using the command that follows.</span></span> <span data-ttu-id="c6fc0-140">Статический IP-адрес должен быть свободен в используемой подсети.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-140">The static IP address must be an unused address for the subnet.</span></span>

    ```bash
    az network nic ip-config create \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --private-ip-address 10.0.0.7 \
    --name IPConfig-4
    ```
    
    <span data-ttu-id="c6fc0-141">Вы можете создать любое количество конфигураций, указывая для них уникальные имена и уникальные частные IP-адреса (если используются статические IP-адреса).</span><span class="sxs-lookup"><span data-stu-id="c6fc0-141">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    <span data-ttu-id="c6fc0-142">**Добавление общедоступного IP-адреса**</span><span class="sxs-lookup"><span data-stu-id="c6fc0-142">**Add a public IP address**</span></span>
    
    <span data-ttu-id="c6fc0-143">Чтобы добавить общедоступный IP-адрес, его нужно связать с новой или имеющейся IP-конфигурацией.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-143">A public IP address is added by associating it to either a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="c6fc0-144">Выполните шаги, описанные в одном из следующих разделов, в соответствии с задачами.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-144">Complete the steps in one of the sections that follow, as you require.</span></span>

    <span data-ttu-id="c6fc0-145">За общедоступные IP-адреса взимается номинальная плата.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-145">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="c6fc0-146">Дополнительные сведения о ценах на IP-адреса см. на странице [Цены на IP-адреса](https://azure.microsoft.com/pricing/details/ip-addresses).</span><span class="sxs-lookup"><span data-stu-id="c6fc0-146">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="c6fc0-147">Число общедоступных IP-адресов, которые можно использовать в одной подписке, ограничено.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-147">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="c6fc0-148">Сведения об ограничениях см. в статье [Подписка Azure, границы, квоты и ограничения службы](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="c6fc0-148">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

    - <span data-ttu-id="c6fc0-149">**Связывание ресурса с новой IP-конфигурацией**</span><span class="sxs-lookup"><span data-stu-id="c6fc0-149">**Associate the resource to a new IP configuration**</span></span>
    
        <span data-ttu-id="c6fc0-150">Чтобы добавить общедоступный IP-адрес в новую IP-конфигурацию, необходимо добавить и частный IP-адрес, так как все IP-конфигурации должны иметь частный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-150">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="c6fc0-151">В конфигурацию можно добавить имеющийся ресурс общедоступного IP-адреса или создать новый.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-151">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="c6fc0-152">Чтобы создать ресурс, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c6fc0-152">To create a new one, enter the following command:</span></span>
    
        ```bash
        az network public-ip create \
        --resource-group myResourceGroup \
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3
        ```

        <span data-ttu-id="c6fc0-153">Чтобы создать новую конфигурацию IP с частным статическим IP-адресом и связанным ресурсом общедоступного IP-адреса *myPublicIP3*, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c6fc0-153">To create a new IP configuration with a static private IP address and the associated *myPublicIP3* public IP address resource, enter the following command:</span></span>

        ```bash
        az network nic ip-config create \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-5 \
        --private-ip-address 10.0.0.8
        --public-ip-address myPublicIP3
        ```

    - <span data-ttu-id="c6fc0-154">**Свяжите ресурс к существующей конфигурации IP** открытого ресурса IP-адреса может быть связан только на IP-конфигурацию, в котором уже не связан.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-154">**Associate the resource to an existing IP configuration** A public IP address resource can only be associated to an IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="c6fc0-155">Чтобы определить, связан ли с конкретной IP-конфигурацией какой-либо общедоступный IP-адрес, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c6fc0-155">You can determine whether an IP configuration has an associated public IP address by entering the following command:</span></span>

        ```bash
        az network nic ip-config list \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --query "[?provisioningState=='Succeeded'].{ Name: name, PublicIpAddressId: publicIpAddress.id }" --output table
        ```

        <span data-ttu-id="c6fc0-156">Возвращаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="c6fc0-156">Returned output:</span></span>
    
            Name        PublicIpAddressId
            
            ipconfig1   /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
            IPConfig-2  /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
            IPConfig-3

        <span data-ttu-id="c6fc0-157">Столбец **PublicIpAddressId** для конфигурации *IpConfig-3* в выходных данных пуст. Это означает, что в настоящее время с этой конфигурацией не связан никакой общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-157">Since the **PublicIpAddressId** column for *IpConfig-3* is blank in the output, no public IP address resource is currently associated to it.</span></span> <span data-ttu-id="c6fc0-158">Вы можете добавить к конфигурации IpConfig-3 имеющийся ресурс общедоступного IP-адреса или создать новый ресурс, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c6fc0-158">You can add an existing public IP address resource to IpConfig-3, or enter the following command to create one:</span></span>

        ```bash
        az network public-ip create \
        --resource-group  myResourceGroup
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3 \
        --allocation-method Static
        ```
    
        <span data-ttu-id="c6fc0-159">Чтобы связать ресурс общедоступного IP-адреса с имеющейся IP-конфигурацией с именем *IPConfig-3*, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c6fc0-159">Enter the following command to associate the public IP address resource to the existing IP configuration named *IPConfig-3*:</span></span>
    
        ```bash
        az network nic ip-config update \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-3 \
        --public-ip myPublicIP3
        ```

3. <span data-ttu-id="c6fc0-160">Просмотрите идентификаторы ресурсов частных и общедоступных IP-адресов, назначенных сетевой карте. Для этого введите следующую команду.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-160">View the private IP addresses and the public IP address resource Ids assigned to the NIC by entering the following command:</span></span>

    ```bash
    az network nic ip-config list \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --query "[?provisioningState=='Succeeded'].{ Name: name, PrivateIpAddress: privateIpAddress, PrivateIpAllocationMethod: privateIpAllocationMethod, PublicIpAddressId: publicIpAddress.id }" --output table
    ```

    <span data-ttu-id="c6fc0-161">Возвращаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="c6fc0-161">Returned output:</span></span> <br>
    
        Name        PrivateIpAddress    PrivateIpAllocationMethod   PublicIpAddressId
        
        ipconfig1   10.0.0.4            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
        IPConfig-2  10.0.0.5            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
        IPConfig-3  10.0.0.6            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP3
    

4. <span data-ttu-id="c6fc0-162">Добавьте в операционную систему виртуальной машины частные IP-адреса, которые вы ранее назначили сетевой карте. Для этого выполните инструкции из раздела [Добавление IP-адресов в операционную систему виртуальной машины](#os-config) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-162">Add the private IP addresses you added to the NIC to the VM operating system by following the instructions in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="c6fc0-163">Не добавляйте в операционную систему общедоступные IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="c6fc0-163">Do not add the public IP addresses to the operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
