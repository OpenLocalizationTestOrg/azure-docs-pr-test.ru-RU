---
title: "aaaVM несколько IP-адресов с помощью Azure CLI 1.0 hello | Документы Microsoft"
description: "Узнайте, как tooassign несколько IP-адресов tooa виртуальную машину с помощью Azure CLI 1.0 \"hello\" | Диспетчер ресурсов."
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
ms.openlocfilehash: 83ad48e67309fb21d5aca967d4f2c01afdc0b5cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-azure-cli-10"></a><span data-ttu-id="06c96-103">Назначить несколько IP-адресов с помощью Azure CLI 1.0 машины toovirtual</span><span class="sxs-lookup"><span data-stu-id="06c96-103">Assign multiple IP addresses toovirtual machines using Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="06c96-104">В этой статье объясняется, как toocreate виртуальной машины (VM) с помощью hello Azure Resource Manager развертывания модели с помощью hello Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="06c96-104">This article explains how toocreate a virtual machine (VM) through hello Azure Resource Manager deployment model using hello Azure CLI 1.0.</span></span> <span data-ttu-id="06c96-105">Несколько IP-адресов нельзя назначить tooresources, созданные с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="06c96-105">Multiple IP addresses cannot be assigned tooresources created through hello classic deployment model.</span></span> <span data-ttu-id="06c96-106">Дополнительные сведения о моделях развертывания Azure, чтение hello toolearn [понять модели развертывания](../resource-manager-deployment-model.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="06c96-106">toolearn more about Azure deployment models, read hello [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="06c96-107"><a name = "create"></a>Создание виртуальной машины с несколькими IP-адресами</span><span class="sxs-lookup"><span data-stu-id="06c96-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="06c96-108">Выполнить эту задачу с помощью hello Azure CLI 1.0 (Эта статья) или hello [Azure CLI 2.0](virtual-network-multiple-ip-addresses-cli.md).</span><span class="sxs-lookup"><span data-stu-id="06c96-108">You can complete this task using hello Azure CLI 1.0 (this article) or hello [Azure CLI 2.0](virtual-network-multiple-ip-addresses-cli.md).</span></span> <span data-ttu-id="06c96-109">Привет, описанных ниже объясняется, как toocreate пример виртуальной Машины с несколькими IP-адресов, как описано в сценарии hello.</span><span class="sxs-lookup"><span data-stu-id="06c96-109">hello steps that follow explain how toocreate an example VM with multiple IP addresses, as described in hello scenario.</span></span> <span data-ttu-id="06c96-110">Измените имена переменных и типы IP-адресов в соответствии с требованиями этой реализации.</span><span class="sxs-lookup"><span data-stu-id="06c96-110">Change variable names and IP address types as required for your implementation.</span></span>

1. <span data-ttu-id="06c96-111">Установка и настройка hello Azure CLI 1.0 с hello следующие шаги в hello [Установка и настройка hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) статью и войдите в учетную запись Azure с hello `azure-login` команды.</span><span class="sxs-lookup"><span data-stu-id="06c96-111">Install and configure hello Azure CLI 1.0 by following hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article and log into your Azure account with hello `azure-login` command.</span></span>

2. <span data-ttu-id="06c96-112">Создайте группу ресурсов:</span><span class="sxs-lookup"><span data-stu-id="06c96-112">Create a resource group:</span></span>
    
    ```azurecli
    RgName=myResourceGroup
    Location=westcentralus
    azure group create --name $RgName --location $Location
    ```
3. <span data-ttu-id="06c96-113">Создайте виртуальную сеть:</span><span class="sxs-lookup"><span data-stu-id="06c96-113">Create a virtual network:</span></span>

    ```azurecli
    azure network vnet create --resource-group $RgName --location $Location --name myVNet \
    --address-prefixes 10.0.0.0/16
    ```
4. <span data-ttu-id="06c96-114">Создание подсети в виртуальной сети hello:</span><span class="sxs-lookup"><span data-stu-id="06c96-114">Create a subnet in hello virtual network:</span></span>

    ```azurecli
    azure network vnet subnet create --name mySubnet --resource-group $RgName --vnet-name myVNet \
    --address-prefix 10.0.0.0/24
    ```
    
5. <span data-ttu-id="06c96-115">Создайте учетную запись хранилища для hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="06c96-115">Create  a storage account for hello VM.</span></span> <span data-ttu-id="06c96-116">Перед запуском hello следующую команду, замените *mystorageaccount* с уникальным именем.</span><span class="sxs-lookup"><span data-stu-id="06c96-116">Before running hello following command, replace *mystorageaccount* with a unique name.</span></span> <span data-ttu-id="06c96-117">Hello имя должно быть уникальным в пределах Azure:</span><span class="sxs-lookup"><span data-stu-id="06c96-117">hello name must be unique across Azure:</span></span>

    ```azurecli
    az storage account create --resource-group $RgName --location $Location --name mystorageaccount \
    --kind Storage --sku Standard_LRS
    ```

6. <span data-ttu-id="06c96-118">Создайте hello IP-конфигурации, сетевой Адаптер и назначьте hello IP конфигураций toohello сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="06c96-118">Create hello IP configurations, a NIC, and assign hello IP configurations toohello NIC.</span></span> <span data-ttu-id="06c96-119">Можно добавить, удалить или изменить hello конфигурации при необходимости.</span><span class="sxs-lookup"><span data-stu-id="06c96-119">You can add, remove, or change hello configurations as necessary.</span></span> <span data-ttu-id="06c96-120">Hello конфигурации описаны в сценарии hello:</span><span class="sxs-lookup"><span data-stu-id="06c96-120">hello following configurations are described in hello scenario:</span></span>

    <span data-ttu-id="06c96-121">**IPConfig-1**</span><span class="sxs-lookup"><span data-stu-id="06c96-121">**IPConfig-1**</span></span>

    <span data-ttu-id="06c96-122">Введите команды hello, следующие за toocreate:</span><span class="sxs-lookup"><span data-stu-id="06c96-122">Enter hello commands that follow toocreate:</span></span>

    - <span data-ttu-id="06c96-123">ресурс общедоступного IP-адреса с общедоступным статическим IP-адресом;</span><span class="sxs-lookup"><span data-stu-id="06c96-123">A public IP address resource with a static public IP address</span></span>
    - <span data-ttu-id="06c96-124">Сетевой Адаптер, назначение hello общедоступный IP-адрес и статические tooit частного IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="06c96-124">A NIC, assigning hello public IP address and a static private IP address tooit.</span></span>
    
    <span data-ttu-id="06c96-125">Замените *mypublicdns* с именем, которое является уникальным в пределах hello расположение Azure.</span><span class="sxs-lookup"><span data-stu-id="06c96-125">Replace *mypublicdns* with a name that is unique within hello Azure location.</span></span>

      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP1 \
      --domain-name-label mypublicdns --allocation-method Static
        
      azure network nic create --resource-group $RgName --location $Location --name myNic1 \
      --private-ip-address 10.0.0.4 --subnet-name mySubnet --subnet-vnet-name myVNet \
      --subnet-name mySubnet --public-ip-name myPublicIP1
      ```

      > [!NOTE]
      > <span data-ttu-id="06c96-126">За общедоступные IP-адреса взимается номинальная плата.</span><span class="sxs-lookup"><span data-stu-id="06c96-126">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="06c96-127">Дополнительные сведения о IP-адресов цен, toolearn чтения hello [цены IP адрес](https://azure.microsoft.com/pricing/details/ip-addresses) страницы.</span><span class="sxs-lookup"><span data-stu-id="06c96-127">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="06c96-128">Нет toohello предельное число общих IP-адресов, которые могут использоваться в подписке.</span><span class="sxs-lookup"><span data-stu-id="06c96-128">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="06c96-129">Дополнительные об ограничениях hello, чтение hello toolearn [Azure ограничивает](../azure-subscription-service-limits.md#networking-limits) статьи.</span><span class="sxs-lookup"><span data-stu-id="06c96-129">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

    <span data-ttu-id="06c96-130">**IPConfig-2**</span><span class="sxs-lookup"><span data-stu-id="06c96-130">**IPConfig-2**</span></span>

     <span data-ttu-id="06c96-131">Введите следующие команды toocreate hello ресурс открытый IP-адреса и новой конфигурации IP с статический общедоступный IP-адрес и статический частный IP-адрес:</span><span class="sxs-lookup"><span data-stu-id="06c96-131">Enter hello following commands toocreate a new public IP address resource and a new IP configuration with a static public IP address and a static private IP address:</span></span>
    
      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP2
      --domain-name-label mypublicdns2 --allocation-method Static

      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --name IPConfig-2
      --private-ip-address 10.0.0.5 --public-ip-name myPublicIP2
      ```

    <span data-ttu-id="06c96-132">**IPConfig-3**</span><span class="sxs-lookup"><span data-stu-id="06c96-132">**IPConfig-3**</span></span>

    <span data-ttu-id="06c96-133">Введите следующие команды toocreate IP-адрес с статический частный IP-адрес и не общедоступный IP-адрес hello:</span><span class="sxs-lookup"><span data-stu-id="06c96-133">Enter hello following commands toocreate an IP configuration with a static private IP address and no public IP address:</span></span>

      ```azurecli
      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --private-ip-address 10.0.0.6 \
      --name IPConfig-3
      ```

    >[!NOTE] 
    ><span data-ttu-id="06c96-134">Хотя в данной статье назначает все tooa IP-конфигурации один сетевой Адаптер, также можно назначить несколько tooany конфигурации IP сетевого Адаптера на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="06c96-134">Though this article assigns all IP configurations tooa single NIC, you can also assign multiple IP configurations tooany NIC in a VM.</span></span> <span data-ttu-id="06c96-135">toolearn как прочитано виртуальной Машины с несколькими сетевыми картами toocreate hello Создание виртуальной Машины с помощью нескольких сетевых адаптеров в статье.</span><span class="sxs-lookup"><span data-stu-id="06c96-135">toolearn how toocreate a VM with multiple NICs, read hello Create a VM with multiple NICs article.</span></span>

7. <span data-ttu-id="06c96-136">Создание виртуальной машины Linux</span><span class="sxs-lookup"><span data-stu-id="06c96-136">Create a Linux VM</span></span> 

    ```azurecli
    az vm create --resource-group $RgName --name myVM1 --location $Location --nics myNic1 \
    --image UbuntuLTS --ssh-key-value ~/.ssh/id_rsa.pub --admin-username azureuser
    ```

    <span data-ttu-id="06c96-137">toochange hello v2 tooStandard DS2 размер виртуальной Машины, например, просто добавьте следующие свойства hello `--vm-size Standard_DS3_v2` toohello `azure vm create` команду на шаге 6.</span><span class="sxs-lookup"><span data-stu-id="06c96-137">toochange hello VM size tooStandard DS2 v2, for example, simply add hello following property `--vm-size Standard_DS3_v2` toohello `azure vm create` command in step 6.</span></span>

8. <span data-ttu-id="06c96-138">Введите следующая команда tooview hello Сетевых hello и hello связанные IP-конфигурации:</span><span class="sxs-lookup"><span data-stu-id="06c96-138">Enter hello following command tooview hello NIC and hello associated IP configurations:</span></span>

    ```azurecli
    azure network nic show --resource-group $RgName --name myNic1
    ```
9. <span data-ttu-id="06c96-139">Добавить hello частного IP адресов toohello ВМ операционной системы, выполнив шаги hello для вашей операционной системы в hello [добавить IP-адресов операционной системы виртуальной Машины tooa](#os-config) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="06c96-139">Add hello private IP addresses toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span>

## <span data-ttu-id="06c96-140"><a name="add"></a>Добавьте IP адресов tooa виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="06c96-140"><a name="add"></a>Add IP addresses tooa VM</span></span>

<span data-ttu-id="06c96-141">Можно добавить дополнительные частных и общедоступных IP адресов tooan существующего сетевого Адаптера, выполнив hello, описанных ниже.</span><span class="sxs-lookup"><span data-stu-id="06c96-141">You can add additional private and public IP addresses tooan existing NIC by completing hello steps that follow.</span></span> <span data-ttu-id="06c96-142">Hello примеры созданы на основе hello [сценарий](#Scenario) описано в этой статье.</span><span class="sxs-lookup"><span data-stu-id="06c96-142">hello examples build upon hello [scenario](#Scenario) described in this article.</span></span>

1. <span data-ttu-id="06c96-143">Откройте Azure CLI и завершения hello, оставшиеся шаги в этом разделе в одном сеансе CLI.</span><span class="sxs-lookup"><span data-stu-id="06c96-143">Open Azure CLI and complete hello remaining steps in this section within a single CLI session.</span></span> <span data-ttu-id="06c96-144">Если у вас еще нет Azure CLI установлен и настроен, hello завершения шагов в hello [Установка и настройка hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) статью и войдите в учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="06c96-144">If you don't already have Azure CLI installed and configured, complete hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article and log into your Azure account.</span></span>

2. <span data-ttu-id="06c96-145">Выполните действия hello в одном из следующих разделах, в зависимости от требований hello.</span><span class="sxs-lookup"><span data-stu-id="06c96-145">Complete hello steps in one of hello following sections, based on your requirements:</span></span>

    - <span data-ttu-id="06c96-146">**Добавление частного IP-адреса**</span><span class="sxs-lookup"><span data-stu-id="06c96-146">**Add a private IP address**</span></span>
    
        <span data-ttu-id="06c96-147">tooadd закрытый tooa адрес IP сетевого Адаптера, необходимо создать IP-конфигурации, с помощью следующей команды hello.</span><span class="sxs-lookup"><span data-stu-id="06c96-147">tooadd a private IP address tooa NIC, you must create an IP configuration using hello command below.</span></span> <span data-ttu-id="06c96-148">Hello статический адрес должен быть неиспользуемый адрес для подсети hello.</span><span class="sxs-lookup"><span data-stu-id="06c96-148">hello static address must be an unused address for hello subnet.</span></span>

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic1 \
        --private-ip-address 10.0.0.7 --name IPConfig-4
        ```
        <span data-ttu-id="06c96-149">Вы можете создать любое количество конфигураций, указывая для них уникальные имена и уникальные частные IP-адреса (если используются статические IP-адреса).</span><span class="sxs-lookup"><span data-stu-id="06c96-149">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    - <span data-ttu-id="06c96-150">**Добавление общедоступного IP-адреса**</span><span class="sxs-lookup"><span data-stu-id="06c96-150">**Add a public IP address**</span></span>
    
        <span data-ttu-id="06c96-151">Общедоступный IP-адрес будет добавлен, связав ее tooeither новой конфигурации IP или существующей конфигурации IP.</span><span class="sxs-lookup"><span data-stu-id="06c96-151">A public IP address is added by associating it tooeither a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="06c96-152">Этапы hello в одном hello следующих разделах, сколько требуется.</span><span class="sxs-lookup"><span data-stu-id="06c96-152">Complete hello steps in one of hello sections that follow, as you require.</span></span>

        > [!NOTE]
        > <span data-ttu-id="06c96-153">За общедоступные IP-адреса взимается номинальная плата.</span><span class="sxs-lookup"><span data-stu-id="06c96-153">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="06c96-154">Дополнительные сведения о IP-адресов цен, toolearn чтения hello [цены IP адрес](https://azure.microsoft.com/pricing/details/ip-addresses) страницы.</span><span class="sxs-lookup"><span data-stu-id="06c96-154">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="06c96-155">Нет toohello предельное число общих IP-адресов, которые могут использоваться в подписке.</span><span class="sxs-lookup"><span data-stu-id="06c96-155">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="06c96-156">Дополнительные об ограничениях hello, чтение hello toolearn [Azure ограничивает](../azure-subscription-service-limits.md#networking-limits) статьи.</span><span class="sxs-lookup"><span data-stu-id="06c96-156">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
        >

        <span data-ttu-id="06c96-157">**Связать новую конфигурацию IP hello ресурсов tooa**</span><span class="sxs-lookup"><span data-stu-id="06c96-157">**Associate hello resource tooa new IP configuration**</span></span>
    
        <span data-ttu-id="06c96-158">Чтобы добавить общедоступный IP-адрес в новую IP-конфигурацию, необходимо добавить и частный IP-адрес, так как все IP-конфигурации должны иметь частный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="06c96-158">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="06c96-159">В конфигурацию можно добавить имеющийся ресурс общедоступного IP-адреса или создать новый.</span><span class="sxs-lookup"><span data-stu-id="06c96-159">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="06c96-160">toocreate новый, введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="06c96-160">toocreate a new one, enter hello following command:</span></span>

        ```azurecli
        azure network public-ip create --resource-group myResourceGroup --location westcentralus --name myPublicIP3 \
        --domain-name-label mypublicdns3
        ```

        <span data-ttu-id="06c96-161">toocreate новой конфигурации IP с статический частный IP-адрес и связанные hello *myPublicIP3* общедоступный IP-адрес адрес ресурса, введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="06c96-161">toocreate a new IP configuration with a static private IP address and hello associated *myPublicIP3* public IP address resource, enter hello following command:</span></span>

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic --name IPConfig-4 \
        --private-ip-address 10.0.0.8 --public-ip-name myPublicIP3
        ```

        <span data-ttu-id="06c96-162">**Связать существующую конфигурацию IP hello ресурсов tooan**</span><span class="sxs-lookup"><span data-stu-id="06c96-162">**Associate hello resource tooan existing IP configuration**</span></span>

        <span data-ttu-id="06c96-163">Открытый ресурс IP-адреса можно только связанные tooan IP-конфигурации, уже не связан.</span><span class="sxs-lookup"><span data-stu-id="06c96-163">A public IP address resource can only be associated tooan IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="06c96-164">Можно определить, имеет ли связанный общий IP-адрес IP-адрес, введя следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="06c96-164">You can determine whether an IP configuration has an associated public IP address by entering hello following command:</span></span>

        ```azurecli
        azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
        ```

        <span data-ttu-id="06c96-165">Поиск строки аналогично toohello, том, что следует для IPConfig 3 в hello, возвращаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="06c96-165">Look for a line similar toohello one that follows for IPConfig-3 in hello returned output:</span></span>

        ```         
        Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
        IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
        IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet
        ```
          
        <span data-ttu-id="06c96-166">С момента hello **общедоступный IP-адрес** столбца для *IpConfig 3* является пустым, не открытого ресурса IP-адреса является в настоящее время связаны tooit.</span><span class="sxs-lookup"><span data-stu-id="06c96-166">Since hello **Public IP** column for *IpConfig-3* is blank, no public IP address resource is currently associated tooit.</span></span> <span data-ttu-id="06c96-167">Можно добавить существующие открытый IP адрес ресурса tooIpConfig-3, или введите hello, следующая команда toocreate один:</span><span class="sxs-lookup"><span data-stu-id="06c96-167">You can add an existing public IP address resource tooIpConfig-3, or enter hello following command toocreate one:</span></span>

        ```azurecli
        azure network public-ip create --resource-group  myResourceGroup --location westcentralus \
        --name myPublicIP3 --domain-name-label mypublicdns3 --allocation-method Static
        ```

        <span data-ttu-id="06c96-168">Введите следующую команду, общедоступный IP-адрес tooassociate hello адресов toohello существующие IP конфигурации ресурса с именем hello *IPConfig 3*:</span><span class="sxs-lookup"><span data-stu-id="06c96-168">Enter hello following command tooassociate hello public IP address resource toohello existing IP configuration named *IPConfig-3*:</span></span>
        ```azurecli
        azure network nic ip-config set --resource-group myResourceGroup --nic-name myNic1 --name IPConfig-3 \
        --public-ip-name myPublicIP3
        ```

3. <span data-ttu-id="06c96-169">Просмотр hello частных IP-адресов и hello открытый IP адрес ресурсы назначенного toohello hello сетевого Адаптера, введя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="06c96-169">View hello private IP addresses and hello public IP address resources assigned toohello NIC by entering hello following command:</span></span>

    ```azurecli
    azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
    ```

      <span data-ttu-id="06c96-170">Hello возвращено выходные данные выглядят аналогично toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="06c96-170">hello returned output is similar toohello following:</span></span>
      ```
      Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        
      default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
      IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
      IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet  myPublicIP3
      ```
4. <span data-ttu-id="06c96-171">Добавить hello частных IP-адресов вы добавили операционной системы ВМ toohello toohello сетевой Адаптер, следуя инструкциям hello hello [добавить IP-адресов операционной системы виртуальной Машины tooa](#os-config) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="06c96-171">Add hello private IP addresses you added toohello NIC toohello VM operating system by following hello instructions in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="06c96-172">Не добавляйте hello открытый IP адресов toohello операционной системы.</span><span class="sxs-lookup"><span data-stu-id="06c96-172">Do not add hello public IP addresses toohello operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
