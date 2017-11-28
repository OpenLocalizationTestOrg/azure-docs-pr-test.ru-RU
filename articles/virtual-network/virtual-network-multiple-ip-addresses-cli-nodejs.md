---
title: "Виртуальная машина с несколькими сетевыми картами (Azure CLI 1.0) | Документация Майкрософт"
description: "Назначение виртуальной машине нескольких IP-адресов с помощью Azure CLI 1.0 | Resource Manager"
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
ms.openlocfilehash: 9f085dfa1fe4db36d58cb976bb550a46bf241ac7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="assign-multiple-ip-addresses-to-virtual-machines-using-azure-cli-10"></a><span data-ttu-id="cc211-103">Назначение виртуальным машинам нескольких IP-адресов с помощью Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="cc211-103">Assign multiple IP addresses to virtual machines using Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="cc211-104">В этой статье описывается создание виртуальной машины с помощью модели развертывания Azure Resource Manager с использованием Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="cc211-104">This article explains how to create a virtual machine (VM) through the Azure Resource Manager deployment model using the Azure CLI 1.0.</span></span> <span data-ttu-id="cc211-105">Для ресурсов, созданных с помощью классической модели развертывания, нельзя назначить несколько IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="cc211-105">Multiple IP addresses cannot be assigned to resources created through the classic deployment model.</span></span> <span data-ttu-id="cc211-106">Дополнительные сведения о моделях развертывания Azure см. в статье [Azure Resource Manager vs. classic deployment: Understand deployment models and the state of your resources](../resource-manager-deployment-model.md) (Развертывание с помощью Azure Resource Manager и классическое развертывание. Общие сведения о моделях развертывания и состоянии ресурсов).</span><span class="sxs-lookup"><span data-stu-id="cc211-106">To learn more about Azure deployment models, read the [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="cc211-107"><a name = "create"></a>Создание виртуальной машины с несколькими IP-адресами</span><span class="sxs-lookup"><span data-stu-id="cc211-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="cc211-108">Эту задачу можно выполнить с помощью Azure CLI 1.0 (в этой статье) или [Azure CLI 2.0](virtual-network-multiple-ip-addresses-cli.md).</span><span class="sxs-lookup"><span data-stu-id="cc211-108">You can complete this task using the Azure CLI 1.0 (this article) or the [Azure CLI 2.0](virtual-network-multiple-ip-addresses-cli.md).</span></span> <span data-ttu-id="cc211-109">Вы можете создать пример виртуальной машины с несколькими IP-адресами, как описано в нашем сценарии.</span><span class="sxs-lookup"><span data-stu-id="cc211-109">The steps that follow explain how to create an example VM with multiple IP addresses, as described in the scenario.</span></span> <span data-ttu-id="cc211-110">Измените имена переменных и типы IP-адресов в соответствии с требованиями этой реализации.</span><span class="sxs-lookup"><span data-stu-id="cc211-110">Change variable names and IP address types as required for your implementation.</span></span>

1. <span data-ttu-id="cc211-111">Установите и настройте Azure CLI 1.0, следуя инструкциям из [этой статьи](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), а затем войдите в учетную запись Azure, выполнив команду `azure-login`.</span><span class="sxs-lookup"><span data-stu-id="cc211-111">Install and configure the Azure CLI 1.0 by following the steps in the [Install and Configure the Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article and log into your Azure account with the `azure-login` command.</span></span>

2. <span data-ttu-id="cc211-112">Создайте группу ресурсов:</span><span class="sxs-lookup"><span data-stu-id="cc211-112">Create a resource group:</span></span>
    
    ```azurecli
    RgName=myResourceGroup
    Location=westcentralus
    azure group create --name $RgName --location $Location
    ```
3. <span data-ttu-id="cc211-113">Создайте виртуальную сеть:</span><span class="sxs-lookup"><span data-stu-id="cc211-113">Create a virtual network:</span></span>

    ```azurecli
    azure network vnet create --resource-group $RgName --location $Location --name myVNet \
    --address-prefixes 10.0.0.0/16
    ```
4. <span data-ttu-id="cc211-114">Создайте подсеть в виртуальной сети:</span><span class="sxs-lookup"><span data-stu-id="cc211-114">Create a subnet in the virtual network:</span></span>

    ```azurecli
    azure network vnet subnet create --name mySubnet --resource-group $RgName --vnet-name myVNet \
    --address-prefix 10.0.0.0/24
    ```
    
5. <span data-ttu-id="cc211-115">Создайте учетную запись хранения для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="cc211-115">Create  a storage account for the VM.</span></span> <span data-ttu-id="cc211-116">Перед выполнением следующей команды замените *mystorageaccount* на уникальное имя.</span><span class="sxs-lookup"><span data-stu-id="cc211-116">Before running the following command, replace *mystorageaccount* with a unique name.</span></span> <span data-ttu-id="cc211-117">Это имя должно быть уникальным в Azure.</span><span class="sxs-lookup"><span data-stu-id="cc211-117">The name must be unique across Azure:</span></span>

    ```azurecli
    az storage account create --resource-group $RgName --location $Location --name mystorageaccount \
    --kind Storage --sku Standard_LRS
    ```

6. <span data-ttu-id="cc211-118">Создайте конфигурации IP, сетевую карту и присвойте конфигурации IP сетевой карте.</span><span class="sxs-lookup"><span data-stu-id="cc211-118">Create the IP configurations, a NIC, and assign the IP configurations to the NIC.</span></span> <span data-ttu-id="cc211-119">Конфигурации можно добавлять, удалять или изменять по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="cc211-119">You can add, remove, or change the configurations as necessary.</span></span> <span data-ttu-id="cc211-120">В сценарии описаны следующие конфигурации.</span><span class="sxs-lookup"><span data-stu-id="cc211-120">The following configurations are described in the scenario:</span></span>

    <span data-ttu-id="cc211-121">**IPConfig-1**</span><span class="sxs-lookup"><span data-stu-id="cc211-121">**IPConfig-1**</span></span>

    <span data-ttu-id="cc211-122">Выполните указанные ниже команды, чтобы создать:</span><span class="sxs-lookup"><span data-stu-id="cc211-122">Enter the commands that follow to create:</span></span>

    - <span data-ttu-id="cc211-123">ресурс общедоступного IP-адреса с общедоступным статическим IP-адресом;</span><span class="sxs-lookup"><span data-stu-id="cc211-123">A public IP address resource with a static public IP address</span></span>
    - <span data-ttu-id="cc211-124">сетевую карту, назначив ей общедоступный IP-адрес и статический частный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="cc211-124">A NIC, assigning the public IP address and a static private IP address to it.</span></span>
    
    <span data-ttu-id="cc211-125">Замените *mypublicdns* именем, которое является уникальным в пределах расположения Azure.</span><span class="sxs-lookup"><span data-stu-id="cc211-125">Replace *mypublicdns* with a name that is unique within the Azure location.</span></span>

      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP1 \
      --domain-name-label mypublicdns --allocation-method Static
        
      azure network nic create --resource-group $RgName --location $Location --name myNic1 \
      --private-ip-address 10.0.0.4 --subnet-name mySubnet --subnet-vnet-name myVNet \
      --subnet-name mySubnet --public-ip-name myPublicIP1
      ```

      > [!NOTE]
      > <span data-ttu-id="cc211-126">За общедоступные IP-адреса взимается номинальная плата.</span><span class="sxs-lookup"><span data-stu-id="cc211-126">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="cc211-127">Дополнительные сведения о ценах на IP-адреса см. на странице [Цены на IP-адреса](https://azure.microsoft.com/pricing/details/ip-addresses).</span><span class="sxs-lookup"><span data-stu-id="cc211-127">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="cc211-128">Число общедоступных IP-адресов, которые можно использовать в одной подписке, ограничено.</span><span class="sxs-lookup"><span data-stu-id="cc211-128">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="cc211-129">Сведения об ограничениях см. в статье [Подписка Azure, границы, квоты и ограничения службы](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="cc211-129">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

    <span data-ttu-id="cc211-130">**IPConfig-2**</span><span class="sxs-lookup"><span data-stu-id="cc211-130">**IPConfig-2**</span></span>

     <span data-ttu-id="cc211-131">Выполните следующие команды, чтобы создать ресурс общедоступного IP-адреса и IP-конфигурацию с общедоступным статическим IP-адресом и частным статическим IP-адресом.</span><span class="sxs-lookup"><span data-stu-id="cc211-131">Enter the following commands to create a new public IP address resource and a new IP configuration with a static public IP address and a static private IP address:</span></span>
    
      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP2
      --domain-name-label mypublicdns2 --allocation-method Static

      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --name IPConfig-2
      --private-ip-address 10.0.0.5 --public-ip-name myPublicIP2
      ```

    <span data-ttu-id="cc211-132">**IPConfig-3**</span><span class="sxs-lookup"><span data-stu-id="cc211-132">**IPConfig-3**</span></span>

    <span data-ttu-id="cc211-133">Выполните следующие команды, чтобы создать конфигурацию IP с частным статическим IP-адресом без общедоступного IP-адреса:</span><span class="sxs-lookup"><span data-stu-id="cc211-133">Enter the following commands to create an IP configuration with a static private IP address and no public IP address:</span></span>

      ```azurecli
      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --private-ip-address 10.0.0.6 \
      --name IPConfig-3
      ```

    >[!NOTE] 
    ><span data-ttu-id="cc211-134">Хотя в этом руководстве все IP-конфигурации назначаются одному сетевому адаптеру, вы также можете назначить несколько IP-конфигураций любому сетевому адаптеру, связанному с виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="cc211-134">Though this article assigns all IP configurations to a single NIC, you can also assign multiple IP configurations to any NIC in a VM.</span></span> <span data-ttu-id="cc211-135">Изучите статью о создании виртуальной машины с несколькими сетевыми адаптерами.</span><span class="sxs-lookup"><span data-stu-id="cc211-135">To learn how to create a VM with multiple NICs, read the Create a VM with multiple NICs article.</span></span>

7. <span data-ttu-id="cc211-136">Создание виртуальной машины Linux</span><span class="sxs-lookup"><span data-stu-id="cc211-136">Create a Linux VM</span></span> 

    ```azurecli
    az vm create --resource-group $RgName --name myVM1 --location $Location --nics myNic1 \
    --image UbuntuLTS --ssh-key-value ~/.ssh/id_rsa.pub --admin-username azureuser
    ```

    <span data-ttu-id="cc211-137">Например, чтобы использовать размер виртуальной машины Standard DS2 v2, просто добавьте свойство `--vm-size Standard_DS3_v2` в команду `azure vm create` на шаге 6.</span><span class="sxs-lookup"><span data-stu-id="cc211-137">To change the VM size to Standard DS2 v2, for example, simply add the following property `--vm-size Standard_DS3_v2` to the `azure vm create` command in step 6.</span></span>

8. <span data-ttu-id="cc211-138">Введите следующую команду, чтобы просмотреть свойства сетевого адаптера и связанных с ним IP-конфигураций:</span><span class="sxs-lookup"><span data-stu-id="cc211-138">Enter the following command to view the NIC and the associated IP configurations:</span></span>

    ```azurecli
    azure network nic show --resource-group $RgName --name myNic1
    ```
9. <span data-ttu-id="cc211-139">Добавьте в операционную систему виртуальной машины частные IP-адреса, выполнив действия, соответствующие вашей операционной системе, как описано в разделе [Добавление IP-адресов в операционную систему виртуальной машины](#os-config) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="cc211-139">Add the private IP addresses to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span>

## <span data-ttu-id="cc211-140"><a name="add"></a>Добавление IP-адресов в виртуальную машину</span><span class="sxs-lookup"><span data-stu-id="cc211-140"><a name="add"></a>Add IP addresses to a VM</span></span>

<span data-ttu-id="cc211-141">Выполнив следующие шаги, вы сможете назначить дополнительные частные или общедоступные IP-адреса существующим сетевым адаптерам.</span><span class="sxs-lookup"><span data-stu-id="cc211-141">You can add additional private and public IP addresses to an existing NIC by completing the steps that follow.</span></span> <span data-ttu-id="cc211-142">Примеры созданы на основе [сценария](#Scenario), описанного в этой статье.</span><span class="sxs-lookup"><span data-stu-id="cc211-142">The examples build upon the [scenario](#Scenario) described in this article.</span></span>

1. <span data-ttu-id="cc211-143">Откройте интерфейс командной строки Azure и выполните в рамках одного сеанса командной строки все действия, описанные в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="cc211-143">Open Azure CLI and complete the remaining steps in this section within a single CLI session.</span></span> <span data-ttu-id="cc211-144">Если интерфейс командной строки Azure еще не установлен, выполните инструкции из статьи [Установка Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), а затем войдите в учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="cc211-144">If you don't already have Azure CLI installed and configured, complete the steps in the [Install and Configure the Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article and log into your Azure account.</span></span>

2. <span data-ttu-id="cc211-145">Выполните действия, описанные в одном из следующих разделов, с учетом задач.</span><span class="sxs-lookup"><span data-stu-id="cc211-145">Complete the steps in one of the following sections, based on your requirements:</span></span>

    - <span data-ttu-id="cc211-146">**Добавление частного IP-адреса**</span><span class="sxs-lookup"><span data-stu-id="cc211-146">**Add a private IP address**</span></span>
    
        <span data-ttu-id="cc211-147">Чтобы назначить сетевому адаптеру частный IP-адрес, создайте IP-конфигурацию с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="cc211-147">To add a private IP address to a NIC, you must create an IP configuration using the command below.</span></span> <span data-ttu-id="cc211-148">Статический адрес должен быть свободен в используемой подсети.</span><span class="sxs-lookup"><span data-stu-id="cc211-148">The static address must be an unused address for the subnet.</span></span>

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic1 \
        --private-ip-address 10.0.0.7 --name IPConfig-4
        ```
        <span data-ttu-id="cc211-149">Вы можете создать любое количество конфигураций, указывая для них уникальные имена и уникальные частные IP-адреса (если используются статические IP-адреса).</span><span class="sxs-lookup"><span data-stu-id="cc211-149">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    - <span data-ttu-id="cc211-150">**Добавление общедоступного IP-адреса**</span><span class="sxs-lookup"><span data-stu-id="cc211-150">**Add a public IP address**</span></span>
    
        <span data-ttu-id="cc211-151">Чтобы добавить общедоступный IP-адрес, его нужно связать с новой или имеющейся IP-конфигурацией.</span><span class="sxs-lookup"><span data-stu-id="cc211-151">A public IP address is added by associating it to either a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="cc211-152">Выполните шаги, описанные в одном из следующих разделов, в соответствии с задачами.</span><span class="sxs-lookup"><span data-stu-id="cc211-152">Complete the steps in one of the sections that follow, as you require.</span></span>

        > [!NOTE]
        > <span data-ttu-id="cc211-153">За общедоступные IP-адреса взимается номинальная плата.</span><span class="sxs-lookup"><span data-stu-id="cc211-153">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="cc211-154">Дополнительные сведения о ценах на IP-адреса см. на странице [Цены на IP-адреса](https://azure.microsoft.com/pricing/details/ip-addresses).</span><span class="sxs-lookup"><span data-stu-id="cc211-154">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="cc211-155">Число общедоступных IP-адресов, которые можно использовать в одной подписке, ограничено.</span><span class="sxs-lookup"><span data-stu-id="cc211-155">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="cc211-156">Сведения об ограничениях см. в статье [Подписка Azure, границы, квоты и ограничения службы](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="cc211-156">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
        >

        <span data-ttu-id="cc211-157">**Связывание ресурса с новой IP-конфигурацией**</span><span class="sxs-lookup"><span data-stu-id="cc211-157">**Associate the resource to a new IP configuration**</span></span>
    
        <span data-ttu-id="cc211-158">Чтобы добавить общедоступный IP-адрес в новую IP-конфигурацию, необходимо добавить и частный IP-адрес, так как все IP-конфигурации должны иметь частный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="cc211-158">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="cc211-159">В конфигурацию можно добавить имеющийся ресурс общедоступного IP-адреса или создать новый.</span><span class="sxs-lookup"><span data-stu-id="cc211-159">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="cc211-160">Чтобы создать ресурс, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="cc211-160">To create a new one, enter the following command:</span></span>

        ```azurecli
        azure network public-ip create --resource-group myResourceGroup --location westcentralus --name myPublicIP3 \
        --domain-name-label mypublicdns3
        ```

        <span data-ttu-id="cc211-161">Чтобы создать новую конфигурацию IP с частным статическим IP-адресом и связанным ресурсом общедоступного IP-адреса *myPublicIP3*, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="cc211-161">To create a new IP configuration with a static private IP address and the associated *myPublicIP3* public IP address resource, enter the following command:</span></span>

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic --name IPConfig-4 \
        --private-ip-address 10.0.0.8 --public-ip-name myPublicIP3
        ```

        <span data-ttu-id="cc211-162">**Связывание ресурса с существующей IP-конфигурацией**</span><span class="sxs-lookup"><span data-stu-id="cc211-162">**Associate the resource to an existing IP configuration**</span></span>

        <span data-ttu-id="cc211-163">Ресурс общедоступного IP-адреса может быть связан только с такой IP-конфигурацией, у которой еще нет такого ресурса.</span><span class="sxs-lookup"><span data-stu-id="cc211-163">A public IP address resource can only be associated to an IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="cc211-164">Чтобы определить, связан ли с конкретной IP-конфигурацией какой-либо общедоступный IP-адрес, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="cc211-164">You can determine whether an IP configuration has an associated public IP address by entering the following command:</span></span>

        ```azurecli
        azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
        ```

        <span data-ttu-id="cc211-165">Найдите в возвращаемых данных строку, похожую на приведенную ниже для IPConfig-3.</span><span class="sxs-lookup"><span data-stu-id="cc211-165">Look for a line similar to the one that follows for IPConfig-3 in the returned output:</span></span>

        ```         
        Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
        IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
        IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet
        ```
          
        <span data-ttu-id="cc211-166">Столбец **Общедоступный IP-адрес** для IP-конфигурации *IpConfig-3* пуст. Это означает, что сейчас с этой конфигурацией общедоступные IP-адреса не связаны.</span><span class="sxs-lookup"><span data-stu-id="cc211-166">Since the **Public IP** column for *IpConfig-3* is blank, no public IP address resource is currently associated to it.</span></span> <span data-ttu-id="cc211-167">Вы можете добавить к конфигурации IpConfig-3 имеющийся ресурс общедоступного IP-адреса или создать новый ресурс, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="cc211-167">You can add an existing public IP address resource to IpConfig-3, or enter the following command to create one:</span></span>

        ```azurecli
        azure network public-ip create --resource-group  myResourceGroup --location westcentralus \
        --name myPublicIP3 --domain-name-label mypublicdns3 --allocation-method Static
        ```

        <span data-ttu-id="cc211-168">Чтобы связать ресурс общедоступного IP-адреса с имеющейся IP-конфигурацией с именем *IPConfig-3*, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="cc211-168">Enter the following command to associate the public IP address resource to the existing IP configuration named *IPConfig-3*:</span></span>
        ```azurecli
        azure network nic ip-config set --resource-group myResourceGroup --nic-name myNic1 --name IPConfig-3 \
        --public-ip-name myPublicIP3
        ```

3. <span data-ttu-id="cc211-169">Просмотрите частные IP адреса и ресурсы общедоступных IP-адресов, назначенные сетевому адаптеру. Для этого введите следующую команду.</span><span class="sxs-lookup"><span data-stu-id="cc211-169">View the private IP addresses and the public IP address resources assigned to the NIC by entering the following command:</span></span>

    ```azurecli
    azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
    ```

      <span data-ttu-id="cc211-170">Выходные данные аналогичны приведенным ниже.</span><span class="sxs-lookup"><span data-stu-id="cc211-170">The returned output is similar to the following:</span></span>
      ```
      Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        
      default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
      IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
      IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet  myPublicIP3
      ```
4. <span data-ttu-id="cc211-171">Добавьте в операционную систему виртуальной машины частные IP-адреса, которые вы ранее назначили сетевой карте. Для этого выполните инструкции из раздела [Добавление IP-адресов в операционную систему виртуальной машины](#os-config) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="cc211-171">Add the private IP addresses you added to the NIC to the VM operating system by following the instructions in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="cc211-172">Не добавляйте в операционную систему общедоступные IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="cc211-172">Do not add the public IP addresses to the operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
