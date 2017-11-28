---
title: "aaaVM несколько IP-адресов с помощью Azure CLI 2.0 hello | Документы Microsoft"
description: "Узнайте, как tooassign несколько IP-адресов tooa виртуальную машину с помощью Azure CLI 2.0 \"hello\" | Диспетчер ресурсов."
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
ms.openlocfilehash: 15efd853cc7c31bacb64ed052dabedd3fe4d3079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-hello-azure-cli-20"></a><span data-ttu-id="05734-103">Назначить несколько IP-адресов машин toovirtual, с помощью Azure CLI 2.0 hello</span><span class="sxs-lookup"><span data-stu-id="05734-103">Assign multiple IP addresses toovirtual machines using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="05734-104">В этой статье объясняется, как toocreate виртуальной машины (VM) с помощью hello Azure Resource Manager развертывания модели с помощью hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="05734-104">This article explains how toocreate a virtual machine (VM) through hello Azure Resource Manager deployment model using hello Azure CLI 2.0.</span></span> <span data-ttu-id="05734-105">Несколько IP-адресов нельзя назначить tooresources, созданные с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="05734-105">Multiple IP addresses cannot be assigned tooresources created through hello classic deployment model.</span></span> <span data-ttu-id="05734-106">Дополнительные сведения о моделях развертывания Azure, чтение hello toolearn [понять модели развертывания](../resource-manager-deployment-model.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="05734-106">toolearn more about Azure deployment models, read hello [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="05734-107"><a name = "create"></a>Создание виртуальной машины с несколькими IP-адресами</span><span class="sxs-lookup"><span data-stu-id="05734-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="05734-108">Выполнить эту задачу с помощью hello Azure CLI 2.0 (Эта статья) или hello [Azure CLI 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="05734-108">You can complete this task using hello Azure CLI 2.0 (this article) or hello [Azure CLI 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md).</span></span> <span data-ttu-id="05734-109">Измените значения hello, в зависимости от среды.</span><span class="sxs-lookup"><span data-stu-id="05734-109">Change hello values, as appropriate, for your environment.</span></span> <span data-ttu-id="05734-110">Привет, описанных ниже объясняется, как toocreate пример виртуальной Машины с несколькими IP-адресов, как описано в сценарии hello.</span><span class="sxs-lookup"><span data-stu-id="05734-110">hello steps that follow explain how toocreate an example VM with multiple IP addresses, as described in hello scenario.</span></span> <span data-ttu-id="05734-111">Измените имена переменных в прямых кавычках и типы IP-адресов в соответствии с требованиями своей реализации.</span><span class="sxs-lookup"><span data-stu-id="05734-111">Change variable values in "" and IP address types as required for your implementation.</span></span> 

1. <span data-ttu-id="05734-112">Установка hello [Azure CLI 2.0](/cli/azure/install-az-cli2) если его нет.</span><span class="sxs-lookup"><span data-stu-id="05734-112">Install hello [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="05734-113">Создание открытого и закрытого пару ключей SSH для виртуальных машин Linux, выполнив шаги hello в hello [создать открытый и закрытый пару ключей SSH для виртуальных машин Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="05734-113">Create an SSH public and private key pair for Linux VMs by completing hello steps in hello [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="05734-114">В командной оболочке входа с помощью команды hello `az login` и выберите hello подписку, которую вы используете.</span><span class="sxs-lookup"><span data-stu-id="05734-114">From a command shell, login with hello command `az login` and select hello subscription you're using.</span></span>
4. <span data-ttu-id="05734-115">Создайте hello виртуальной Машины, выполнив скрипт hello на компьютере Mac или Linux.</span><span class="sxs-lookup"><span data-stu-id="05734-115">Create hello VM by executing hello script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="05734-116">Hello скрипт создает группу ресурсов, одной виртуальной сети (VNet), один сетевой Адаптер с тремя IP-конфигурации и виртуальной Машины с tooit hello двух сетевых адаптеров присоединен.</span><span class="sxs-lookup"><span data-stu-id="05734-116">hello script creates a resource group, one virtual network (VNet), one NIC with three IP configurations, and a VM with hello two NICs attached tooit.</span></span> <span data-ttu-id="05734-117">Здравствуйте, сетевой Адаптер, общедоступный IP-адрес, виртуальной сети и ресурсы виртуальной Машины должны существовать в hello же местоположение и подписку.</span><span class="sxs-lookup"><span data-stu-id="05734-117">hello NIC, public IP address, virtual network, and VM resources must all exist in hello same location and subscription.</span></span> <span data-ttu-id="05734-118">Хотя ресурсы hello все еще нет tooexist в hello одну группу ресурсов, в следующий сценарий, как и hello.</span><span class="sxs-lookup"><span data-stu-id="05734-118">Though hello resources don't all have tooexist in hello same resource group, in hello following script they do.</span></span>

```bash
    
#!/bin/sh
    
RgName="myResourceGroup"
Location="westcentralus"
az group create --name $RgName --location $Location
    
# Create a public IP address resource with a static IP address using hello `--allocation-method Static` option. If you
# do not specify this option, hello address is allocated dynamically. hello address is assigned toohello resource from a pool
# of IP adresses unique tooeach Azure region. Download and view hello file from
# https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists hello ranges for each region.

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

# Create a network interface connected toohello subnet and associate hello public IP address tooit. Azure will create the
# first IP configuration with a static private IP address and will associate hello public IP address resource tooit.

NicName="MyNic1"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--private-ip-address 10.0.0.4
--vnet-name $VnetName \
--public-ip-address $PipName
    
# Create a second public IP address, a second IP configuration, and associate it toohello NIC. This configuration has a
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

# Create a third IP configuration, and associate it toohello NIC. This configuration has  static private IP address and # no public IP address.

azure network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--private-ip-address 10.0.0.6 \
--name IPConfig-3

# Note: Though this article assigns all IP configurations tooa single NIC, you can also assign multiple IP configurations
# tooany NIC in a VM. toolearn how toocreate a VM with multiple NICs, read hello Create a VM with multiple NICs 
# article: https://docs.microsoft.com/azure/virtual-network/virtual-network-deploy-multinic-arm-cli.

# Create a VM and attach hello NIC.

VmName="myVm"

# Replace hello value for hello following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes rticle. hello script fails if hello VM size
# is not supported in hello location you select. Run hello `azure vm sizes --location estcentralus` command tooget a full list
# of VMs in US West Central, for example.

VmSize="Standard_DS1"

# Replace hello value for hello OsImage variable value with a value for *urn* from hello utput returned by entering the
# `az vm image list` command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace hello following value with hello path tooyour public key file. If you're creating a Windows VM, remove hello following
# line and you'll be prompted for hello password you want tooconfigure for hello VM.

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

<span data-ttu-id="05734-119">В дополнение к этому toocreating ВМ с сетевой КАРТОЙ с 3 IP-конфигурации hello скрипт создает:</span><span class="sxs-lookup"><span data-stu-id="05734-119">In addition toocreating a VM with a NIC with 3 IP configurations, hello script creates:</span></span>

- <span data-ttu-id="05734-120">Один premium управлять диска по умолчанию, но наличия других параметров для hello тип диска, которые можно создать.</span><span class="sxs-lookup"><span data-stu-id="05734-120">A single premium managed disk by default, but you have other options for hello disk type you can create.</span></span> <span data-ttu-id="05734-121">Чтение hello [создания ВМ Linux с помощью Azure CLI 2.0 hello](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Дополнительные сведения см.</span><span class="sxs-lookup"><span data-stu-id="05734-121">Read hello [Create a Linux VM using hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="05734-122">Виртуальная сеть с одной подсетью и двумя общедоступными IP-адресами.</span><span class="sxs-lookup"><span data-stu-id="05734-122">A virtual network with one subnet and two public IP addresses.</span></span> <span data-ttu-id="05734-123">Кроме того, можно использовать *имеющиеся* виртуальные сети, подсети, сетевые карты или общедоступные IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="05734-123">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="05734-124">toolearn как toouse существующие сетевые ресурсы, вместо создания дополнительных ресурсов, введите `az vm create -h`.</span><span class="sxs-lookup"><span data-stu-id="05734-124">toolearn how toouse existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

<span data-ttu-id="05734-125">За общедоступные IP-адреса взимается номинальная плата.</span><span class="sxs-lookup"><span data-stu-id="05734-125">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="05734-126">Дополнительные сведения о IP-адресов цен, toolearn чтения hello [цены IP адрес](https://azure.microsoft.com/pricing/details/ip-addresses) страницы.</span><span class="sxs-lookup"><span data-stu-id="05734-126">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="05734-127">Нет toohello предельное число общих IP-адресов, которые могут использоваться в подписке.</span><span class="sxs-lookup"><span data-stu-id="05734-127">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="05734-128">Дополнительные об ограничениях hello, чтение hello toolearn [Azure ограничивает](../azure-subscription-service-limits.md#networking-limits) статьи.</span><span class="sxs-lookup"><span data-stu-id="05734-128">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

<span data-ttu-id="05734-129">После создания виртуальной Машины hello введите hello `az network nic show --name MyNic1 --resource-group myResourceGroup` конфигурацию сетевого Адаптера hello tooview команды.</span><span class="sxs-lookup"><span data-stu-id="05734-129">After hello VM is created, enter hello `az network nic show --name MyNic1 --resource-group myResourceGroup` command tooview hello NIC configuration.</span></span> <span data-ttu-id="05734-130">Введите hello `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` tooview список IP-конфигурации hello связанные toohello сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="05734-130">Enter hello `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` tooview a list of hello IP configurations associated toohello NIC.</span></span>

<span data-ttu-id="05734-131">Добавить hello частного IP адресов toohello ВМ операционной системы, выполнив шаги hello для вашей операционной системы в hello [добавить IP-адресов операционной системы виртуальной Машины tooa](#os-config) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="05734-131">Add hello private IP addresses toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span>

## <span data-ttu-id="05734-132"><a name="add"></a>Добавьте IP адресов tooa виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="05734-132"><a name="add"></a>Add IP addresses tooa VM</span></span>

<span data-ttu-id="05734-133">Можно добавить дополнительные частных и общедоступных IP адресов tooan существующего сетевого Адаптера, выполнив hello, описанных ниже.</span><span class="sxs-lookup"><span data-stu-id="05734-133">You can add additional private and public IP addresses tooan existing NIC by completing hello steps that follow.</span></span> <span data-ttu-id="05734-134">Hello примеры созданы на основе hello [сценарий](#Scenario) описано в этой статье.</span><span class="sxs-lookup"><span data-stu-id="05734-134">hello examples build upon hello [scenario](#Scenario) described in this article.</span></span>

1. <span data-ttu-id="05734-135">Откройте командную строку и завершения hello оставшиеся шаги в этом разделе в одном сеансе.</span><span class="sxs-lookup"><span data-stu-id="05734-135">Open a command shell and complete hello remaining steps in this section within a single session.</span></span> <span data-ttu-id="05734-136">Если у вас еще нет Azure CLI установлен и настроен, hello завершения шагов в hello [установки Azure CLI 2.0](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json) tooyour статьи и входа учетная запись Azure с hello `az-login` команды.</span><span class="sxs-lookup"><span data-stu-id="05734-136">If you don't already have Azure CLI installed and configured, complete hello steps in hello [Azure CLI 2.0 installation](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json) article and login tooyour Azure account with hello `az-login` command.</span></span>

2. <span data-ttu-id="05734-137">Выполните действия hello в одном из следующих разделах, в зависимости от требований hello.</span><span class="sxs-lookup"><span data-stu-id="05734-137">Complete hello steps in one of hello following sections, based on your requirements:</span></span>

    <span data-ttu-id="05734-138">**Добавление частного IP-адреса**</span><span class="sxs-lookup"><span data-stu-id="05734-138">**Add a private IP address**</span></span>
    
    <span data-ttu-id="05734-139">tooadd закрытый tooa адрес IP сетевого Адаптера, необходимо создать IP-конфигурации, с помощью команды hello ниже.</span><span class="sxs-lookup"><span data-stu-id="05734-139">tooadd a private IP address tooa NIC, you must create an IP configuration using hello command that follows.</span></span> <span data-ttu-id="05734-140">Hello статический IP-адрес должен быть неиспользуемый адрес для подсети hello.</span><span class="sxs-lookup"><span data-stu-id="05734-140">hello static IP address must be an unused address for hello subnet.</span></span>

    ```bash
    az network nic ip-config create \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --private-ip-address 10.0.0.7 \
    --name IPConfig-4
    ```
    
    <span data-ttu-id="05734-141">Вы можете создать любое количество конфигураций, указывая для них уникальные имена и уникальные частные IP-адреса (если используются статические IP-адреса).</span><span class="sxs-lookup"><span data-stu-id="05734-141">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    <span data-ttu-id="05734-142">**Добавление общедоступного IP-адреса**</span><span class="sxs-lookup"><span data-stu-id="05734-142">**Add a public IP address**</span></span>
    
    <span data-ttu-id="05734-143">Общедоступный IP-адрес будет добавлен, связав ее tooeither новой конфигурации IP или существующей конфигурации IP.</span><span class="sxs-lookup"><span data-stu-id="05734-143">A public IP address is added by associating it tooeither a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="05734-144">Этапы hello в одном hello следующих разделах, сколько требуется.</span><span class="sxs-lookup"><span data-stu-id="05734-144">Complete hello steps in one of hello sections that follow, as you require.</span></span>

    <span data-ttu-id="05734-145">За общедоступные IP-адреса взимается номинальная плата.</span><span class="sxs-lookup"><span data-stu-id="05734-145">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="05734-146">Дополнительные сведения о IP-адресов цен, toolearn чтения hello [цены IP адрес](https://azure.microsoft.com/pricing/details/ip-addresses) страницы.</span><span class="sxs-lookup"><span data-stu-id="05734-146">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="05734-147">Нет toohello предельное число общих IP-адресов, которые могут использоваться в подписке.</span><span class="sxs-lookup"><span data-stu-id="05734-147">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="05734-148">Дополнительные об ограничениях hello, чтение hello toolearn [Azure ограничивает](../azure-subscription-service-limits.md#networking-limits) статьи.</span><span class="sxs-lookup"><span data-stu-id="05734-148">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

    - <span data-ttu-id="05734-149">**Связать новую конфигурацию IP hello ресурсов tooa**</span><span class="sxs-lookup"><span data-stu-id="05734-149">**Associate hello resource tooa new IP configuration**</span></span>
    
        <span data-ttu-id="05734-150">Чтобы добавить общедоступный IP-адрес в новую IP-конфигурацию, необходимо добавить и частный IP-адрес, так как все IP-конфигурации должны иметь частный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="05734-150">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="05734-151">В конфигурацию можно добавить имеющийся ресурс общедоступного IP-адреса или создать новый.</span><span class="sxs-lookup"><span data-stu-id="05734-151">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="05734-152">toocreate новый, введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="05734-152">toocreate a new one, enter hello following command:</span></span>
    
        ```bash
        az network public-ip create \
        --resource-group myResourceGroup \
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3
        ```

        <span data-ttu-id="05734-153">toocreate новой конфигурации IP с статический частный IP-адрес и связанные hello *myPublicIP3* общедоступный IP-адрес адрес ресурса, введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="05734-153">toocreate a new IP configuration with a static private IP address and hello associated *myPublicIP3* public IP address resource, enter hello following command:</span></span>

        ```bash
        az network nic ip-config create \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-5 \
        --private-ip-address 10.0.0.8
        --public-ip-address myPublicIP3
        ```

    - <span data-ttu-id="05734-154">**Существующую конфигурацию IP связан hello ресурсов tooan** открытого ресурса IP-адреса можно только связанные tooan IP-конфигурации, уже не связан.</span><span class="sxs-lookup"><span data-stu-id="05734-154">**Associate hello resource tooan existing IP configuration** A public IP address resource can only be associated tooan IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="05734-155">Можно определить, имеет ли связанный общий IP-адрес IP-адрес, введя следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="05734-155">You can determine whether an IP configuration has an associated public IP address by entering hello following command:</span></span>

        ```bash
        az network nic ip-config list \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --query "[?provisioningState=='Succeeded'].{ Name: name, PublicIpAddressId: publicIpAddress.id }" --output table
        ```

        <span data-ttu-id="05734-156">Возвращаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="05734-156">Returned output:</span></span>
    
            Name        PublicIpAddressId
            
            ipconfig1   /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
            IPConfig-2  /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
            IPConfig-3

        <span data-ttu-id="05734-157">С момента hello **PublicIpAddressId** столбца для *IpConfig 3* является пустым в hello выходные данные, не открытого ресурса IP-адреса является в настоящее время связаны tooit.</span><span class="sxs-lookup"><span data-stu-id="05734-157">Since hello **PublicIpAddressId** column for *IpConfig-3* is blank in hello output, no public IP address resource is currently associated tooit.</span></span> <span data-ttu-id="05734-158">Можно добавить существующие открытый IP адрес ресурса tooIpConfig-3, или введите hello, следующая команда toocreate один:</span><span class="sxs-lookup"><span data-stu-id="05734-158">You can add an existing public IP address resource tooIpConfig-3, or enter hello following command toocreate one:</span></span>

        ```bash
        az network public-ip create \
        --resource-group  myResourceGroup
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3 \
        --allocation-method Static
        ```
    
        <span data-ttu-id="05734-159">Введите следующую команду, общедоступный IP-адрес tooassociate hello адресов toohello существующие IP конфигурации ресурса с именем hello *IPConfig 3*:</span><span class="sxs-lookup"><span data-stu-id="05734-159">Enter hello following command tooassociate hello public IP address resource toohello existing IP configuration named *IPConfig-3*:</span></span>
    
        ```bash
        az network nic ip-config update \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-3 \
        --public-ip myPublicIP3
        ```

3. <span data-ttu-id="05734-160">Представление hello частных IP-адресов и hello открытый IP-адресов идентификаторы ресурсов, назначенных toohello hello сетевого Адаптера, введя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="05734-160">View hello private IP addresses and hello public IP address resource Ids assigned toohello NIC by entering hello following command:</span></span>

    ```bash
    az network nic ip-config list \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --query "[?provisioningState=='Succeeded'].{ Name: name, PrivateIpAddress: privateIpAddress, PrivateIpAllocationMethod: privateIpAllocationMethod, PublicIpAddressId: publicIpAddress.id }" --output table
    ```

    <span data-ttu-id="05734-161">Возвращаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="05734-161">Returned output:</span></span> <br>
    
        Name        PrivateIpAddress    PrivateIpAllocationMethod   PublicIpAddressId
        
        ipconfig1   10.0.0.4            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
        IPConfig-2  10.0.0.5            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
        IPConfig-3  10.0.0.6            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP3
    

4. <span data-ttu-id="05734-162">Добавить hello частных IP-адресов вы добавили операционной системы ВМ toohello toohello сетевой Адаптер, следуя инструкциям hello hello [добавить IP-адресов операционной системы виртуальной Машины tooa](#os-config) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="05734-162">Add hello private IP addresses you added toohello NIC toohello VM operating system by following hello instructions in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="05734-163">Не добавляйте hello открытый IP адресов toohello операционной системы.</span><span class="sxs-lookup"><span data-stu-id="05734-163">Do not add hello public IP addresses toohello operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
