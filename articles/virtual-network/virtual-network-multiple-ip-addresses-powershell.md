---
title: "Назначение виртуальным машинам Azure нескольких IP-адресов с помощью PowerShell | Документация Майкрософт"
description: "Сведения о назначении виртуальной машине нескольких IP-адресов с помощью PowerShell при использовании Resource Manager."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c44ea62f-7e54-4e3b-81ef-0b132111f1f8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/24/2017
ms.author: jdial;annahar
ms.openlocfilehash: 29f64aeefc2a7deb1f84d759c2323347536b9c27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="assign-multiple-ip-addresses-to-virtual-machines-using-powershell"></a><span data-ttu-id="f0460-103">Назначение виртуальным машинам нескольких IP-адресов с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="f0460-103">Assign multiple IP addresses to virtual machines using PowerShell</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="f0460-104">В этой статье описывается создание виртуальной машины с помощью модели развертывания Azure Resource Manager с использованием PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f0460-104">This article explains how to create a virtual machine (VM) through the Azure Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="f0460-105">Для ресурсов, созданных с помощью классической модели развертывания, нельзя назначить несколько IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="f0460-105">Multiple IP addresses cannot be assigned to resources created through the classic deployment model.</span></span> <span data-ttu-id="f0460-106">Дополнительные сведения о моделях развертывания Azure см. в статье [Azure Resource Manager vs. classic deployment: Understand deployment models and the state of your resources](../resource-manager-deployment-model.md) (Развертывание с помощью Azure Resource Manager и классическое развертывание. Общие сведения о моделях развертывания и состоянии ресурсов).</span><span class="sxs-lookup"><span data-stu-id="f0460-106">To learn more about Azure deployment models, read the [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="f0460-107"><a name = "create"></a>Создание виртуальной машины с несколькими IP-адресами</span><span class="sxs-lookup"><span data-stu-id="f0460-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="f0460-108">Вы можете создать пример виртуальной машины с несколькими IP-адресами, как описано в нашем сценарии.</span><span class="sxs-lookup"><span data-stu-id="f0460-108">The steps that follow explain how to create an example VM with multiple IP addresses, as described in the scenario.</span></span> <span data-ttu-id="f0460-109">Измените имена переменных в соответствии с требованиями своей реализации.</span><span class="sxs-lookup"><span data-stu-id="f0460-109">Change variable values as required for your implementation.</span></span>

1. <span data-ttu-id="f0460-110">Откройте командную строку PowerShell и выполните остальные действия в этом разделе в пределах одного сеанса PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f0460-110">Open a PowerShell command prompt and complete the remaining steps in this section within a single PowerShell session.</span></span> <span data-ttu-id="f0460-111">Если вы еще не установили и не настроили PowerShell, выполните шаги, описанные в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="f0460-111">If you don't already have PowerShell installed and configured, complete the steps in the [How to install and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="f0460-112">Войдите в свою учетную запись с помощью команды `login-azurermaccount`.</span><span class="sxs-lookup"><span data-stu-id="f0460-112">Login to your account with the `login-azurermaccount` command.</span></span>
3. <span data-ttu-id="f0460-113">Замените *myResourceGroup* и *westus* именем и расположением по своему выбору.</span><span class="sxs-lookup"><span data-stu-id="f0460-113">Replace *myResourceGroup* and *westus* with a name and location of your choosing.</span></span> <span data-ttu-id="f0460-114">Создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f0460-114">Create a resource group.</span></span> <span data-ttu-id="f0460-115">Группа ресурсов — это логический контейнер, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="f0460-115">A resource group is a logical container into which Azure resources are deployed and managed.</span></span>

    ```powershell
    $RgName   = "MyResourceGroup"
    $Location = "westus"

    New-AzureRmResourceGroup `
    -Name $RgName `
    -Location $Location
    ```

4. <span data-ttu-id="f0460-116">Создайте виртуальную сеть и подсеть в расположении, где находится группа ресурсов:</span><span class="sxs-lookup"><span data-stu-id="f0460-116">Create a virtual network (VNet) and subnet in the same location as the resource group:</span></span>

    ```powershell
    
    # Create a subnet configuration
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name MySubnet `
    -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $VNet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $RgName `
    -Location $Location `
    -Name MyVNet `
    -AddressPrefix 10.0.0.0/16 `
    -Subnet $subnetConfig

    # Get the subnet object
    $Subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $SubnetConfig.Name -VirtualNetwork $VNet
    ```

5. <span data-ttu-id="f0460-117">Создайте группу безопасности сети (NSG) и правило.</span><span class="sxs-lookup"><span data-stu-id="f0460-117">Create a network security group (NSG) and a rule.</span></span> <span data-ttu-id="f0460-118">Группа NSG защищает виртуальную машину с помощью правил входящего и исходящего трафика.</span><span class="sxs-lookup"><span data-stu-id="f0460-118">The NSG secures the VM using inbound and outbound rules.</span></span> <span data-ttu-id="f0460-119">В нашем случае создается правило для входящего трафика порта 3389, которое разрешает входящие подключения к удаленному рабочему столу.</span><span class="sxs-lookup"><span data-stu-id="f0460-119">In this case, an inbound rule is created for port 3389, which allows incoming remote desktop connections.</span></span>

    ```powershell
    
    # Create an inbound network security group rule for port 3389

    $NSGRule = New-AzureRmNetworkSecurityRuleConfig `
    -Name MyNsgRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 -Access Allow
    
    # Create a network security group
    $NSG = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $RgName `
    -Location $Location `
    -Name MyNetworkSecurityGroup `
    -SecurityRules $NSGRule
    ```

6. <span data-ttu-id="f0460-120">Определите основную конфигурацию IP для сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="f0460-120">Define the primary IP configuration for the NIC.</span></span> <span data-ttu-id="f0460-121">Замените 10.0.0.4 действительным адресом в созданной подсети, если вы не использовали значение, определенное ранее.</span><span class="sxs-lookup"><span data-stu-id="f0460-121">Change 10.0.0.4 to a valid address in the subnet you created, if you didn't use the value defined previously.</span></span> <span data-ttu-id="f0460-122">Прежде чем назначать статический IP-адрес, рекомендуем сначала убедиться, что он не используется.</span><span class="sxs-lookup"><span data-stu-id="f0460-122">Before assigning a static IP address, it's recommended that you first confirm it's not already in use.</span></span> <span data-ttu-id="f0460-123">Введите команду `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`.</span><span class="sxs-lookup"><span data-stu-id="f0460-123">Enter the command `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`.</span></span> <span data-ttu-id="f0460-124">Если адрес доступен, в выходных данных возвращается значение *True*,</span><span class="sxs-lookup"><span data-stu-id="f0460-124">If the address is available, the output returns *True*.</span></span> <span data-ttu-id="f0460-125">а если нет — значение *False* и список доступных адресов.</span><span class="sxs-lookup"><span data-stu-id="f0460-125">If it's not available, the output returns *False* and a list of addresses that are available.</span></span> 

    <span data-ttu-id="f0460-126">В следующих командах **замените <replace-with-your-unique-name> уникальным DNS-именем.**</span><span class="sxs-lookup"><span data-stu-id="f0460-126">In the following commands, **Replace <replace-with-your-unique-name> with the unique DNS name to use.**</span></span> <span data-ttu-id="f0460-127">Имя должно быть уникальным для всех общедоступных IP-адресов в регионе Azure.</span><span class="sxs-lookup"><span data-stu-id="f0460-127">The name must be unique across all public IP addresses within an Azure region.</span></span> <span data-ttu-id="f0460-128">Данный параметр является необязательным.</span><span class="sxs-lookup"><span data-stu-id="f0460-128">This is an optional parameter.</span></span> <span data-ttu-id="f0460-129">Его можно удалить, если вам нужно подключаться к виртуальной машине, используя только общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="f0460-129">It can be removed if you only want to connect to the VM using the public IP address.</span></span>

    ```powershell
    
    # Create a public IP address
    $PublicIP1 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP1" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -DomainNameLabel <replace-with-your-unique-name> `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign the public IP ddress to it
    $IpConfigName1 = "IPConfig-1"
    $IpConfig1     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName1 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.4 `
    -PublicIpAddress $PublicIP1 `
    -Primary
    ```

    <span data-ttu-id="f0460-130">При назначении нескольких IP-конфигураций сетевому интерфейсу одну конфигурацию необходимо назначить в качестве первичной (*-Primary*).</span><span class="sxs-lookup"><span data-stu-id="f0460-130">When you assign multiple IP configurations to a NIC, one configuration must be assigned as the *-Primary*.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f0460-131">За общедоступные IP-адреса взимается номинальная плата.</span><span class="sxs-lookup"><span data-stu-id="f0460-131">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="f0460-132">Дополнительные сведения о ценах на IP-адреса см. на странице [Цены на IP-адреса](https://azure.microsoft.com/pricing/details/ip-addresses).</span><span class="sxs-lookup"><span data-stu-id="f0460-132">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="f0460-133">Число общедоступных IP-адресов, которые можно использовать в одной подписке, ограничено.</span><span class="sxs-lookup"><span data-stu-id="f0460-133">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="f0460-134">Сведения об ограничениях см. в статье [Подписка Azure, границы, квоты и ограничения службы](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="f0460-134">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

7. <span data-ttu-id="f0460-135">Определите дополнительную конфигурацию IP для сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="f0460-135">Define the secondary IP configurations for the NIC.</span></span> <span data-ttu-id="f0460-136">Конфигурации можно добавлять и удалять по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="f0460-136">You can add or remove configurations as necessary.</span></span> <span data-ttu-id="f0460-137">Каждой конфигурации IP должен быть назначен частный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="f0460-137">Each IP configuration must have a private IP address assigned.</span></span> <span data-ttu-id="f0460-138">Каждой конфигурации может быть назначен один необязательный общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="f0460-138">Each configuration can optionally have one public IP address assigned.</span></span>

    ```powershell
    
    # Create a public IP address
    $PublicIP2 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP2" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign the public IP ddress to it
    $IpConfigName2 = "IPConfig-2"
    $IpConfig2     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName2 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.5 `
    -PublicIpAddress $PublicIP2
        
    $IpConfigName3 = "IpConfig-3"
    $IpConfig3 = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IPConfigName3 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.6
    ```

8. <span data-ttu-id="f0460-139">Создайте сетевой адаптер и свяжите с ним три конфигурации IP:</span><span class="sxs-lookup"><span data-stu-id="f0460-139">Create the NIC and associate the three IP configurations to it:</span></span>

    ```powershell
    
    $NIC = New-AzureRmNetworkInterface `
    -Name MyNIC `
    -ResourceGroupName $RgName `
    -Location $Location `
    -NetworkSecurityGroupId $NSG.Id `
    -IpConfiguration $IpConfig1,$IpConfig2,$IpConfig3
    ```

    >[!NOTE]
    ><span data-ttu-id="f0460-140">Хотя в этой статье все конфигурации назначены одному сетевому адаптеру, каждому сетевому адаптеру, подключенному к виртуальной машине, можно назначить несколько конфигураций IP.</span><span class="sxs-lookup"><span data-stu-id="f0460-140">Though all configurations are assigned to one NIC in this article, you can assign multiple IP configurations to every NIC attached to the VM.</span></span> <span data-ttu-id="f0460-141">Дополнительные сведения о создании виртуальной машины с несколькими сетевыми интерфейсами см. в [этой статье](virtual-network-deploy-multinic-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="f0460-141">To learn how to create a VM with multiple NICs, read the [Create a VM with multiple NICs](virtual-network-deploy-multinic-arm-ps.md) article.</span></span>

9. <span data-ttu-id="f0460-142">Создайте виртуальную машину с помощью следующих команд:</span><span class="sxs-lookup"><span data-stu-id="f0460-142">Create the VM by entering the following commands:</span></span>

    ```powershell
    
    # Define a credential object. When you run these commands, you're prompted to enter a sername and password for the VM you're reating.
    $cred = Get-Credential
    
    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
    -VMName MyVM `
    -VMSize Standard_DS1_v2 | `
    Set-AzureRmVMOperatingSystem -Windows `
    -ComputerName MyVM `
    -Credential $cred | `
    Set-AzureRmVMSourceImage `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest | `
    Add-AzureRmVMNetworkInterface `
    -Id $NIC.Id
    
    # Create the VM
    New-AzureRmVM `
    -ResourceGroupName $RgName `
    -Location $Location `
    -VM $VmConfig
    ```

10. <span data-ttu-id="f0460-143">Добавьте в операционную систему виртуальной машины частные IP-адреса, выполнив действия, соответствующие вашей операционной системе, как описано в разделе [Добавление IP-адресов в операционную систему виртуальной машины](#os-config) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="f0460-143">Add the private IP addresses to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="f0460-144">Не добавляйте в операционную систему общедоступные IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="f0460-144">Do not add the public IP addresses to the operating system.</span></span>

## <span data-ttu-id="f0460-145"><a name="add"></a>Добавление IP-адресов в виртуальную машину</span><span class="sxs-lookup"><span data-stu-id="f0460-145"><a name="add"></a>Add IP addresses to a VM</span></span>

<span data-ttu-id="f0460-146">Выполнив следующие шаги, вы сможете добавить к сетевой карте частные и общедоступные IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="f0460-146">You can add private and public IP addresses to a NIC by completing the steps that follow.</span></span> <span data-ttu-id="f0460-147">В примерах, приводимых в следующих разделах, предполагается, что у вас уже есть виртуальная машина с тремя IP-конфигурациями, описанными в [сценарии](#Scenario) в этой статье, но это не является обязательным требованием.</span><span class="sxs-lookup"><span data-stu-id="f0460-147">The examples in the following sections assume that you already have a VM with the three IP configurations described in the [scenario](#Scenario) in this article, but it's not required that you do.</span></span>

1. <span data-ttu-id="f0460-148">Откройте командную строку PowerShell и выполните остальные действия в этом разделе в пределах одного сеанса PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f0460-148">Open a PowerShell command prompt and complete the remaining steps in this section within a single PowerShell session.</span></span> <span data-ttu-id="f0460-149">Если вы еще не установили и не настроили PowerShell, выполните шаги, описанные в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="f0460-149">If you don't already have PowerShell installed and configured, complete the steps in the [How to install and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="f0460-150">Измените значения переменных со знаком "$" на имя сетевого интерфейса, к которому необходимо добавить IP-адрес, а также имя группы ресурсов и расположения, где находится сетевой интерфейс.</span><span class="sxs-lookup"><span data-stu-id="f0460-150">Change the "values" of the following $Variables to the name of the NIC you want to add IP address to and the resource group and location the NIC exists in:</span></span>

    ```powershell
    $NicName  = "MyNIC"
    $RgName   = "MyResourceGroup"
    $Location = "westus"
    ```

    <span data-ttu-id="f0460-151">Если имя сетевого интерфейса, который необходимо изменить, неизвестно, введите следующие команды, а затем измените значения предыдущих переменных.</span><span class="sxs-lookup"><span data-stu-id="f0460-151">If you don't know the name of the NIC you want to change, enter the following commands, then change the values of the previous variables:</span></span>

    ```powershell
    Get-AzureRmNetworkInterface | Format-Table Name, ResourceGroupName, Location
    ```
3. <span data-ttu-id="f0460-152">Создайте переменную и назначьте ее существующему сетевому интерфейсу, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f0460-152">Create a variable and set it to the existing NIC by typing the following command:</span></span>

    ```powershell
    $MyNIC = Get-AzureRmNetworkInterface -Name $NicName -ResourceGroupName $RgName
    ```
4. <span data-ttu-id="f0460-153">В следующих командах замените параметры *MyVNet* и *MySubnet* именами виртуальной сети и подсети, к которым подключен сетевой адаптер.</span><span class="sxs-lookup"><span data-stu-id="f0460-153">In the following commands, change *MyVNet* and *MySubnet* to the names of the VNet and subnet the NIC is connected to.</span></span> <span data-ttu-id="f0460-154">Чтобы получить объекты виртуальной сети и подсети, к которым подключен сетевой интерфейс, выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="f0460-154">Enter the commands to retrieve the VNet and subnet objects the NIC is connected to:</span></span>

    ```powershell
    $MyVNet = Get-AzureRMVirtualnetwork -Name MyVNet -ResourceGroupName $RgName
    $Subnet = $MyVnet.Subnets | Where-Object { $_.Name -eq "MySubnet" }
    ```
    <span data-ttu-id="f0460-155">Если вы не знаете имя виртуальной сети или подсети, к которым подключен сетевой интерфейс, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f0460-155">If you don't know the VNet or subnet name the NIC is connected to, enter the following command:</span></span>
    ```powershell
    $MyNIC.IpConfigurations
    ```
    <span data-ttu-id="f0460-156">В выходных данных найдите текст, похожий на следующий пример:</span><span class="sxs-lookup"><span data-stu-id="f0460-156">In the output, look for text similar to the following example output:</span></span>
    
    ```
    "Id": "/subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/MyVNet/subnets/MySubnet"
    ```
    <span data-ttu-id="f0460-157">В этих выходных данных *MyVnet* — это имя виртуальной сети, а *MySubnet* —имя подсети, к которой подключен сетевой адаптер.</span><span class="sxs-lookup"><span data-stu-id="f0460-157">In this output, *MyVnet* is the VNet and *MySubnet* is the subnet the NIC is connected to.</span></span>

5. <span data-ttu-id="f0460-158">Выполните действия, описанные в одном из следующих разделов, с учетом задач.</span><span class="sxs-lookup"><span data-stu-id="f0460-158">Complete the steps in one of the following sections, based on your requirements:</span></span>

    <span data-ttu-id="f0460-159">**Добавление частного IP-адреса**</span><span class="sxs-lookup"><span data-stu-id="f0460-159">**Add a private IP address**</span></span>

    <span data-ttu-id="f0460-160">Чтобы добавить к сетевому интерфейсу частный IP-адрес, нужно создать IP-конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="f0460-160">To add a private IP address to a NIC, you must create an IP configuration.</span></span> <span data-ttu-id="f0460-161">Следующая команда создает конфигурацию со статическим IP-адресом 10.0.0.7.</span><span class="sxs-lookup"><span data-stu-id="f0460-161">The following command creates a configuration with a static IP address of 10.0.0.7.</span></span> <span data-ttu-id="f0460-162">Указываемый статический IP-адрес должен быть свободен в используемой подсети.</span><span class="sxs-lookup"><span data-stu-id="f0460-162">When specifying a static IP address, it must be an unused address for the subnet.</span></span> <span data-ttu-id="f0460-163">Мы советуем сначала проверить доступность адреса. Для этого выполните команду `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet`.</span><span class="sxs-lookup"><span data-stu-id="f0460-163">It's recommended that you first test the address to ensure it's available by entering the `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet` command.</span></span> <span data-ttu-id="f0460-164">Если IP-адрес доступен, в выходных данных возвращается значение *True*,</span><span class="sxs-lookup"><span data-stu-id="f0460-164">If the IP address is available, the output returns *True*.</span></span> <span data-ttu-id="f0460-165">а если нет — значение *False* и список доступных адресов.</span><span class="sxs-lookup"><span data-stu-id="f0460-165">If it's not available, the output returns *False*, and a list of addresses that are available.</span></span>

    ```powershell
    Add-AzureRmNetworkInterfaceIpConfig -Name IPConfig-4 -NetworkInterface `
    $MyNIC -Subnet $Subnet -PrivateIpAddress 10.0.0.7
    ```
    <span data-ttu-id="f0460-166">Вы можете создать любое количество конфигураций, указывая для них уникальные имена и уникальные частные IP-адреса (если используются статические IP-адреса).</span><span class="sxs-lookup"><span data-stu-id="f0460-166">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    <span data-ttu-id="f0460-167">Добавьте в операционную систему виртуальной машины частный IP-адрес, выполнив действия, соответствующие вашей операционной системе, как описано в разделе [Добавление IP-адресов в операционную систему виртуальной машины](#os-config) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="f0460-167">Add the private IP address to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span>

    <span data-ttu-id="f0460-168">**Добавление общедоступного IP-адреса**</span><span class="sxs-lookup"><span data-stu-id="f0460-168">**Add a public IP address**</span></span>

    <span data-ttu-id="f0460-169">Чтобы добавить общедоступный IP-адрес, его ресурс необходимо связать с новой или существующей IP-конфигурацией.</span><span class="sxs-lookup"><span data-stu-id="f0460-169">A public IP address is added by associating a public IP address resource to either a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="f0460-170">Выполните шаги, описанные в одном из следующих разделов, в соответствии с задачами.</span><span class="sxs-lookup"><span data-stu-id="f0460-170">Complete the steps in one of the sections that follow, as you require.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f0460-171">За общедоступные IP-адреса взимается номинальная плата.</span><span class="sxs-lookup"><span data-stu-id="f0460-171">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="f0460-172">Дополнительные сведения о ценах на IP-адреса см. на странице [Цены на IP-адреса](https://azure.microsoft.com/pricing/details/ip-addresses).</span><span class="sxs-lookup"><span data-stu-id="f0460-172">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="f0460-173">Число общедоступных IP-адресов, которые можно использовать в одной подписке, ограничено.</span><span class="sxs-lookup"><span data-stu-id="f0460-173">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="f0460-174">Сведения об ограничениях см. в статье [Подписка Azure, границы, квоты и ограничения службы](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="f0460-174">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
    >

    - <span data-ttu-id="f0460-175">**Связывание ресурса общедоступного IP-адреса с новой IP-конфигурацией**</span><span class="sxs-lookup"><span data-stu-id="f0460-175">**Associate the public IP address resource to a new IP configuration**</span></span>
    
        <span data-ttu-id="f0460-176">Чтобы добавить общедоступный IP-адрес в новую IP-конфигурацию, необходимо добавить и частный IP-адрес, так как все IP-конфигурации должны иметь частный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="f0460-176">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="f0460-177">В конфигурацию можно добавить имеющийся ресурс общедоступного IP-адреса или создать новый.</span><span class="sxs-lookup"><span data-stu-id="f0460-177">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="f0460-178">Чтобы создать ресурс, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f0460-178">To create a new one, enter the following command:</span></span>
    
        ```powershell
        $myPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "myPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location `
        -AllocationMethod Static
        ```

        <span data-ttu-id="f0460-179">Чтобы создать новую IP-конфигурацию с частным статическим IP-адресом и связанным ресурсом общедоступного IP-адреса *myPublicIp3*, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f0460-179">To create a new IP configuration with a static private IP address and the associated *myPublicIp3* public IP address resource, enter the following command:</span></span>

        ```powershell
        Add-AzureRmNetworkInterfaceIpConfig `
        -Name IPConfig-4 `
        -NetworkInterface $myNIC `
        -Subnet $Subnet `
        -PrivateIpAddress 10.0.0.7 `
        -PublicIpAddress $myPublicIp3
        ```

    - <span data-ttu-id="f0460-180">**Связывание ресурса общедоступного IP-адреса с существующей IP-конфигурацией**</span><span class="sxs-lookup"><span data-stu-id="f0460-180">**Associate the public IP address resource to an existing IP configuration**</span></span>

        <span data-ttu-id="f0460-181">Ресурс общедоступного IP-адреса может быть связан только с такой IP-конфигурацией, у которой еще нет такого ресурса.</span><span class="sxs-lookup"><span data-stu-id="f0460-181">A public IP address resource can only be associated to an IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="f0460-182">Чтобы определить, связан ли с конкретной IP-конфигурацией какой-либо общедоступный IP-адрес, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f0460-182">You can determine whether an IP configuration has an associated public IP address by entering the following command:</span></span>

        ```powershell
        $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
        ```

        <span data-ttu-id="f0460-183">Должен появиться результат, аналогичный приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="f0460-183">You see output similar to the following:</span></span>

        ```     
        Name       PrivateIpAddress PublicIpAddress                                           Primary
        
        IPConfig-1 10.0.0.4         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress    True
        IPConfig-2 10.0.0.5         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress   False
        IpConfig-3 10.0.0.6                                                                     False
        ```

        <span data-ttu-id="f0460-184">Столбец **PublicIpAddress** для IP-конфигурации *IpConfig-3* пуст. Это означает, что в настоящее время с этой конфигурацией не связан никакой общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="f0460-184">Since the **PublicIpAddress** column for *IpConfig-3* is blank, no public IP address resource is currently associated to it.</span></span> <span data-ttu-id="f0460-185">Вы можете добавить к конфигурации IpConfig-3 имеющийся ресурс общедоступного IP-адреса или создать новый ресурс, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f0460-185">You can add an existing public IP address resource to IpConfig-3, or enter the following command to create one:</span></span>

        ```powershell
        $MyPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "MyPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location -AllocationMethod Static
        ```

        <span data-ttu-id="f0460-186">Чтобы связать ресурс общедоступного IP-адреса с имеющейся IP-конфигурацией с именем *IPConfig-3*, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f0460-186">Enter the following command to associate the public IP address resource to the existing IP configuration named *IpConfig-3*:</span></span>
    
        ```powershell
        Set-AzureRmNetworkInterfaceIpConfig `
        -Name IpConfig-3 `
        -NetworkInterface $mynic `
        -Subnet $Subnet `
        -PublicIpAddress $myPublicIp3
        ```

6. <span data-ttu-id="f0460-187">Настройте для сетевого интерфейса IP-конфигурацию, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f0460-187">Set the NIC with the new IP configuration by entering the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $MyNIC
    ```

7. <span data-ttu-id="f0460-188">Просмотрите частные IP адреса и ресурсы общедоступных IP-адресов, назначенные сетевому адаптеру. Для этого введите следующую команду.</span><span class="sxs-lookup"><span data-stu-id="f0460-188">View the private IP addresses and the public IP address resources assigned to the NIC by entering the following command:</span></span>

    ```powershell   
    $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
    ```
8. <span data-ttu-id="f0460-189">Добавьте в операционную систему виртуальной машины частный IP-адрес, выполнив действия, соответствующие вашей операционной системе, как описано в разделе [Добавление IP-адресов в операционную систему виртуальной машины](#os-config) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="f0460-189">Add the private IP address to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="f0460-190">Не добавляйте в операционную систему общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="f0460-190">Do not add the public IP address to the operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
