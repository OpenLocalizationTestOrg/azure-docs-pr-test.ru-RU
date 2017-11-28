---
title: "aaaMultiple IP-адресов для виртуальных машин Azure — PowerShell | Документы Microsoft"
description: "Узнайте, как tooassign несколько IP-адресов tooa виртуальной машины с помощью PowerShell | Диспетчер ресурсов."
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
ms.openlocfilehash: df54c4386ce13521e660a3e7208c8c1ab1459bc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-powershell"></a><span data-ttu-id="eece1-103">Назначение нескольких IP-адресов toovirtual машин с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="eece1-103">Assign multiple IP addresses toovirtual machines using PowerShell</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="eece1-104">В этой статье объясняется, как toocreate виртуальной машины (VM) с помощью развертывания диспетчера ресурсов Azure hello модели с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="eece1-104">This article explains how toocreate a virtual machine (VM) through hello Azure Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="eece1-105">Несколько IP-адресов нельзя назначить tooresources, созданные с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="eece1-105">Multiple IP addresses cannot be assigned tooresources created through hello classic deployment model.</span></span> <span data-ttu-id="eece1-106">Дополнительные сведения о моделях развертывания Azure, чтение hello toolearn [понять модели развертывания](../resource-manager-deployment-model.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="eece1-106">toolearn more about Azure deployment models, read hello [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="eece1-107"><a name = "create"></a>Создание виртуальной машины с несколькими IP-адресами</span><span class="sxs-lookup"><span data-stu-id="eece1-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="eece1-108">Привет, описанных ниже объясняется, как toocreate пример виртуальной Машины с несколькими IP-адресов, как описано в сценарии hello.</span><span class="sxs-lookup"><span data-stu-id="eece1-108">hello steps that follow explain how toocreate an example VM with multiple IP addresses, as described in hello scenario.</span></span> <span data-ttu-id="eece1-109">Измените имена переменных в соответствии с требованиями своей реализации.</span><span class="sxs-lookup"><span data-stu-id="eece1-109">Change variable values as required for your implementation.</span></span>

1. <span data-ttu-id="eece1-110">Откройте окно командной строки PowerShell и завершения hello, оставшиеся шаги в этом разделе в одном сеансе PowerShell.</span><span class="sxs-lookup"><span data-stu-id="eece1-110">Open a PowerShell command prompt and complete hello remaining steps in this section within a single PowerShell session.</span></span> <span data-ttu-id="eece1-111">Если у вас еще нет PowerShell устанавливается и настраивается, hello завершения шагов в hello [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) статьи.</span><span class="sxs-lookup"><span data-stu-id="eece1-111">If you don't already have PowerShell installed and configured, complete hello steps in hello [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="eece1-112">Учетная запись входа tooyour с hello `login-azurermaccount` команды.</span><span class="sxs-lookup"><span data-stu-id="eece1-112">Login tooyour account with hello `login-azurermaccount` command.</span></span>
3. <span data-ttu-id="eece1-113">Замените *myResourceGroup* и *westus* именем и расположением по своему выбору.</span><span class="sxs-lookup"><span data-stu-id="eece1-113">Replace *myResourceGroup* and *westus* with a name and location of your choosing.</span></span> <span data-ttu-id="eece1-114">Создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="eece1-114">Create a resource group.</span></span> <span data-ttu-id="eece1-115">Группа ресурсов — это логический контейнер, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="eece1-115">A resource group is a logical container into which Azure resources are deployed and managed.</span></span>

    ```powershell
    $RgName   = "MyResourceGroup"
    $Location = "westus"

    New-AzureRmResourceGroup `
    -Name $RgName `
    -Location $Location
    ```

4. <span data-ttu-id="eece1-116">Создание виртуальной сети (VNet) и подсети в hello местоположения hello группа ресурсов:</span><span class="sxs-lookup"><span data-stu-id="eece1-116">Create a virtual network (VNet) and subnet in hello same location as hello resource group:</span></span>

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

    # Get hello subnet object
    $Subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $SubnetConfig.Name -VirtualNetwork $VNet
    ```

5. <span data-ttu-id="eece1-117">Создайте группу безопасности сети (NSG) и правило.</span><span class="sxs-lookup"><span data-stu-id="eece1-117">Create a network security group (NSG) and a rule.</span></span> <span data-ttu-id="eece1-118">Hello NSG защищает hello виртуальной Машины с помощью правила входящего и исходящего трафика.</span><span class="sxs-lookup"><span data-stu-id="eece1-118">hello NSG secures hello VM using inbound and outbound rules.</span></span> <span data-ttu-id="eece1-119">В нашем случае создается правило для входящего трафика порта 3389, которое разрешает входящие подключения к удаленному рабочему столу.</span><span class="sxs-lookup"><span data-stu-id="eece1-119">In this case, an inbound rule is created for port 3389, which allows incoming remote desktop connections.</span></span>

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

6. <span data-ttu-id="eece1-120">Определение hello основной IP-конфигурации для hello сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="eece1-120">Define hello primary IP configuration for hello NIC.</span></span> <span data-ttu-id="eece1-121">Изменение 10.0.0.4 tooa допустимый адрес в подсети hello, вы создали, если вы не использовали ранее определенное значение hello.</span><span class="sxs-lookup"><span data-stu-id="eece1-121">Change 10.0.0.4 tooa valid address in hello subnet you created, if you didn't use hello value defined previously.</span></span> <span data-ttu-id="eece1-122">Прежде чем назначать статический IP-адрес, рекомендуем сначала убедиться, что он не используется.</span><span class="sxs-lookup"><span data-stu-id="eece1-122">Before assigning a static IP address, it's recommended that you first confirm it's not already in use.</span></span> <span data-ttu-id="eece1-123">Введите команду hello `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`.</span><span class="sxs-lookup"><span data-stu-id="eece1-123">Enter hello command `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`.</span></span> <span data-ttu-id="eece1-124">Если доступен адрес hello, hello выходные возвращает *True*.</span><span class="sxs-lookup"><span data-stu-id="eece1-124">If hello address is available, hello output returns *True*.</span></span> <span data-ttu-id="eece1-125">Если он недоступен, hello выходные возвращает *False* и список доступных адресов.</span><span class="sxs-lookup"><span data-stu-id="eece1-125">If it's not available, hello output returns *False* and a list of addresses that are available.</span></span> 

    <span data-ttu-id="eece1-126">В следующие команды, hello **замените hello уникальное DNS имя toouse < замены с your уникальный name >.**</span><span class="sxs-lookup"><span data-stu-id="eece1-126">In hello following commands, **Replace <replace-with-your-unique-name> with hello unique DNS name toouse.**</span></span> <span data-ttu-id="eece1-127">Hello имя должно быть уникальным для общих IP-адресов внутри области Azure.</span><span class="sxs-lookup"><span data-stu-id="eece1-127">hello name must be unique across all public IP addresses within an Azure region.</span></span> <span data-ttu-id="eece1-128">Данный параметр является необязательным.</span><span class="sxs-lookup"><span data-stu-id="eece1-128">This is an optional parameter.</span></span> <span data-ttu-id="eece1-129">Его можно удалить, если требуется только tooconnect toohello виртуальной Машины с помощью hello общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="eece1-129">It can be removed if you only want tooconnect toohello VM using hello public IP address.</span></span>

    ```powershell
    
    # Create a public IP address
    $PublicIP1 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP1" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -DomainNameLabel <replace-with-your-unique-name> `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign hello public IP ddress tooit
    $IpConfigName1 = "IPConfig-1"
    $IpConfig1     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName1 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.4 `
    -PublicIpAddress $PublicIP1 `
    -Primary
    ```

    <span data-ttu-id="eece1-130">При назначении нескольких tooa конфигурации IP сетевого Адаптера, один конфигурации должны быть назначены как hello *-основной*.</span><span class="sxs-lookup"><span data-stu-id="eece1-130">When you assign multiple IP configurations tooa NIC, one configuration must be assigned as hello *-Primary*.</span></span>

    > [!NOTE]
    > <span data-ttu-id="eece1-131">За общедоступные IP-адреса взимается номинальная плата.</span><span class="sxs-lookup"><span data-stu-id="eece1-131">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="eece1-132">Дополнительные сведения о IP-адресов цен, toolearn чтения hello [цены IP адрес](https://azure.microsoft.com/pricing/details/ip-addresses) страницы.</span><span class="sxs-lookup"><span data-stu-id="eece1-132">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="eece1-133">Нет toohello предельное число общих IP-адресов, которые могут использоваться в подписке.</span><span class="sxs-lookup"><span data-stu-id="eece1-133">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="eece1-134">Дополнительные об ограничениях hello, чтение hello toolearn [Azure ограничивает](../azure-subscription-service-limits.md#networking-limits) статьи.</span><span class="sxs-lookup"><span data-stu-id="eece1-134">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

7. <span data-ttu-id="eece1-135">Определение hello дополнительный IP-конфигурации для hello сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="eece1-135">Define hello secondary IP configurations for hello NIC.</span></span> <span data-ttu-id="eece1-136">Конфигурации можно добавлять и удалять по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="eece1-136">You can add or remove configurations as necessary.</span></span> <span data-ttu-id="eece1-137">Каждой конфигурации IP должен быть назначен частный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="eece1-137">Each IP configuration must have a private IP address assigned.</span></span> <span data-ttu-id="eece1-138">Каждой конфигурации может быть назначен один необязательный общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="eece1-138">Each configuration can optionally have one public IP address assigned.</span></span>

    ```powershell
    
    # Create a public IP address
    $PublicIP2 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP2" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign hello public IP ddress tooit
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

8. <span data-ttu-id="eece1-139">Создайте hello сетевой Адаптер и связать hello три IP конфигурации tooit:</span><span class="sxs-lookup"><span data-stu-id="eece1-139">Create hello NIC and associate hello three IP configurations tooit:</span></span>

    ```powershell
    
    $NIC = New-AzureRmNetworkInterface `
    -Name MyNIC `
    -ResourceGroupName $RgName `
    -Location $Location `
    -NetworkSecurityGroupId $NSG.Id `
    -IpConfiguration $IpConfig1,$IpConfig2,$IpConfig3
    ```

    >[!NOTE]
    ><span data-ttu-id="eece1-140">Хотя все конфигурации будут назначены tooone сетевого Адаптера в этой статье, можно назначить сетевого Адаптера, подключенного tooevery toohello виртуальной Машины для нескольких IP конфигурации.</span><span class="sxs-lookup"><span data-stu-id="eece1-140">Though all configurations are assigned tooone NIC in this article, you can assign multiple IP configurations tooevery NIC attached toohello VM.</span></span> <span data-ttu-id="eece1-141">как считывать toocreate виртуальной Машины с несколькими сетевыми картами toolearn hello [создания виртуальной Машины с несколькими сетевыми адаптерами](virtual-network-deploy-multinic-arm-ps.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="eece1-141">toolearn how toocreate a VM with multiple NICs, read hello [Create a VM with multiple NICs](virtual-network-deploy-multinic-arm-ps.md) article.</span></span>

9. <span data-ttu-id="eece1-142">Создайте hello виртуальной Машины, введя hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="eece1-142">Create hello VM by entering hello following commands:</span></span>

    ```powershell
    
    # Define a credential object. When you run these commands, you're prompted tooenter a sername and password for hello VM you're reating.
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
    
    # Create hello VM
    New-AzureRmVM `
    -ResourceGroupName $RgName `
    -Location $Location `
    -VM $VmConfig
    ```

10. <span data-ttu-id="eece1-143">Добавить hello частного IP адресов toohello ВМ операционной системы, выполнив шаги hello для вашей операционной системы в hello [добавить IP-адресов операционной системы виртуальной Машины tooa](#os-config) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="eece1-143">Add hello private IP addresses toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="eece1-144">Не добавляйте hello открытый IP адресов toohello операционной системы.</span><span class="sxs-lookup"><span data-stu-id="eece1-144">Do not add hello public IP addresses toohello operating system.</span></span>

## <span data-ttu-id="eece1-145"><a name="add"></a>Добавьте IP адресов tooa виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="eece1-145"><a name="add"></a>Add IP addresses tooa VM</span></span>

<span data-ttu-id="eece1-146">Можно добавить открытые и закрытые tooa адресов IP сетевого Адаптера, выполнив hello, описанных ниже.</span><span class="sxs-lookup"><span data-stu-id="eece1-146">You can add private and public IP addresses tooa NIC by completing hello steps that follow.</span></span> <span data-ttu-id="eece1-147">Hello примеры в следующих разделах hello предполагается, что вы уже виртуальной Машины с hello трех IP-конфигурации, описанной в hello [сценарий](#Scenario) в этой статье, но он не обязательно должен выполнить.</span><span class="sxs-lookup"><span data-stu-id="eece1-147">hello examples in hello following sections assume that you already have a VM with hello three IP configurations described in hello [scenario](#Scenario) in this article, but it's not required that you do.</span></span>

1. <span data-ttu-id="eece1-148">Откройте окно командной строки PowerShell и завершения hello, оставшиеся шаги в этом разделе в одном сеансе PowerShell.</span><span class="sxs-lookup"><span data-stu-id="eece1-148">Open a PowerShell command prompt and complete hello remaining steps in this section within a single PowerShell session.</span></span> <span data-ttu-id="eece1-149">Если у вас еще нет PowerShell устанавливается и настраивается, hello завершения шагов в hello [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) статьи.</span><span class="sxs-lookup"><span data-stu-id="eece1-149">If you don't already have PowerShell installed and configured, complete hello steps in hello [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="eece1-150">Изменить hello «значения» hello, следуя имя toohello $Variables hello сетевого Адаптера необходимо tooadd IP адрес tooand hello ресурсов группы и размещения hello сетевой Адаптер существует в:</span><span class="sxs-lookup"><span data-stu-id="eece1-150">Change hello "values" of hello following $Variables toohello name of hello NIC you want tooadd IP address tooand hello resource group and location hello NIC exists in:</span></span>

    ```powershell
    $NicName  = "MyNIC"
    $RgName   = "MyResourceGroup"
    $Location = "westus"
    ```

    <span data-ttu-id="eece1-151">Если вы не знаете имя hello hello требуется toochange сетевого Адаптера, введите следующие команды hello, а затем измените значения hello hello предыдущие переменные:</span><span class="sxs-lookup"><span data-stu-id="eece1-151">If you don't know hello name of hello NIC you want toochange, enter hello following commands, then change hello values of hello previous variables:</span></span>

    ```powershell
    Get-AzureRmNetworkInterface | Format-Table Name, ResourceGroupName, Location
    ```
3. <span data-ttu-id="eece1-152">Создайте переменную и присвойте ему toohello существующего сетевого Адаптера, введя следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="eece1-152">Create a variable and set it toohello existing NIC by typing hello following command:</span></span>

    ```powershell
    $MyNIC = Get-AzureRmNetworkInterface -Name $NicName -ResourceGroupName $RgName
    ```
4. <span data-ttu-id="eece1-153">В hello, следующие команды, измените *MyVNet* и *MySubnet* toohello имена hello виртуальной сети и подсети hello, подключен сетевой Адаптер.</span><span class="sxs-lookup"><span data-stu-id="eece1-153">In hello following commands, change *MyVNet* and *MySubnet* toohello names of hello VNet and subnet hello NIC is connected to.</span></span> <span data-ttu-id="eece1-154">Введите hello команды tooretrieve hello виртуальной сети и подсети объектов hello подключения сетевого Адаптера:</span><span class="sxs-lookup"><span data-stu-id="eece1-154">Enter hello commands tooretrieve hello VNet and subnet objects hello NIC is connected to:</span></span>

    ```powershell
    $MyVNet = Get-AzureRMVirtualnetwork -Name MyVNet -ResourceGroupName $RgName
    $Subnet = $MyVnet.Subnets | Where-Object { $_.Name -eq "MySubnet" }
    ```
    <span data-ttu-id="eece1-155">Если вы не знаете hello виртуальную сеть или подсеть имя приветствия подключен сетевой Адаптер, введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="eece1-155">If you don't know hello VNet or subnet name hello NIC is connected to, enter hello following command:</span></span>
    ```powershell
    $MyNIC.IpConfigurations
    ```
    <span data-ttu-id="eece1-156">В выходных данных hello найдите toohello аналогичный текст, следующий пример выходных данных:</span><span class="sxs-lookup"><span data-stu-id="eece1-156">In hello output, look for text similar toohello following example output:</span></span>
    
    ```
    "Id": "/subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/MyVNet/subnets/MySubnet"
    ```
    <span data-ttu-id="eece1-157">В данном выходе *MyVnet* — hello виртуальной сети и *MySubnet* — сетевой Адаптер подключен к hello подсети hello.</span><span class="sxs-lookup"><span data-stu-id="eece1-157">In this output, *MyVnet* is hello VNet and *MySubnet* is hello subnet hello NIC is connected to.</span></span>

5. <span data-ttu-id="eece1-158">Выполните действия hello в одном из следующих разделах, в зависимости от требований hello.</span><span class="sxs-lookup"><span data-stu-id="eece1-158">Complete hello steps in one of hello following sections, based on your requirements:</span></span>

    <span data-ttu-id="eece1-159">**Добавление частного IP-адреса**</span><span class="sxs-lookup"><span data-stu-id="eece1-159">**Add a private IP address**</span></span>

    <span data-ttu-id="eece1-160">tooadd закрытый tooa адрес IP сетевого Адаптера, необходимо создать IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="eece1-160">tooadd a private IP address tooa NIC, you must create an IP configuration.</span></span> <span data-ttu-id="eece1-161">Hello следующая команда создает конфигурации со статическим IP-адресом 10.0.0.7.</span><span class="sxs-lookup"><span data-stu-id="eece1-161">hello following command creates a configuration with a static IP address of 10.0.0.7.</span></span> <span data-ttu-id="eece1-162">При задании статического IP-адреса, он должен быть неиспользуемый адрес для подсети hello.</span><span class="sxs-lookup"><span data-stu-id="eece1-162">When specifying a static IP address, it must be an unused address for hello subnet.</span></span> <span data-ttu-id="eece1-163">Рекомендуется сначала протестировать tooensure адрес hello, она доступна, введя hello `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet` команды.</span><span class="sxs-lookup"><span data-stu-id="eece1-163">It's recommended that you first test hello address tooensure it's available by entering hello `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet` command.</span></span> <span data-ttu-id="eece1-164">Если IP-адрес hello, hello output возвращает *True*.</span><span class="sxs-lookup"><span data-stu-id="eece1-164">If hello IP address is available, hello output returns *True*.</span></span> <span data-ttu-id="eece1-165">Если он недоступен, hello выходные возвращает *False*и список доступных адресов.</span><span class="sxs-lookup"><span data-stu-id="eece1-165">If it's not available, hello output returns *False*, and a list of addresses that are available.</span></span>

    ```powershell
    Add-AzureRmNetworkInterfaceIpConfig -Name IPConfig-4 -NetworkInterface `
    $MyNIC -Subnet $Subnet -PrivateIpAddress 10.0.0.7
    ```
    <span data-ttu-id="eece1-166">Вы можете создать любое количество конфигураций, указывая для них уникальные имена и уникальные частные IP-адреса (если используются статические IP-адреса).</span><span class="sxs-lookup"><span data-stu-id="eece1-166">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    <span data-ttu-id="eece1-167">Добавьте hello частного IP адрес toohello операционной системы ВМ, выполнив действия hello для вашей операционной системы в hello [добавить IP-адресов операционной системы виртуальной Машины tooa](#os-config) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="eece1-167">Add hello private IP address toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span>

    <span data-ttu-id="eece1-168">**Добавление общедоступного IP-адреса**</span><span class="sxs-lookup"><span data-stu-id="eece1-168">**Add a public IP address**</span></span>

    <span data-ttu-id="eece1-169">Общедоступный IP-адрес будет добавлен, связав общих ресурсов tooeither IP-адрес новой конфигурации IP или существующей конфигурации IP.</span><span class="sxs-lookup"><span data-stu-id="eece1-169">A public IP address is added by associating a public IP address resource tooeither a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="eece1-170">Этапы hello в одном hello следующих разделах, сколько требуется.</span><span class="sxs-lookup"><span data-stu-id="eece1-170">Complete hello steps in one of hello sections that follow, as you require.</span></span>

    > [!NOTE]
    > <span data-ttu-id="eece1-171">За общедоступные IP-адреса взимается номинальная плата.</span><span class="sxs-lookup"><span data-stu-id="eece1-171">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="eece1-172">Дополнительные сведения о IP-адресов цен, toolearn чтения hello [цены IP адрес](https://azure.microsoft.com/pricing/details/ip-addresses) страницы.</span><span class="sxs-lookup"><span data-stu-id="eece1-172">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="eece1-173">Нет toohello предельное число общих IP-адресов, которые могут использоваться в подписке.</span><span class="sxs-lookup"><span data-stu-id="eece1-173">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="eece1-174">Дополнительные об ограничениях hello, чтение hello toolearn [Azure ограничивает](../azure-subscription-service-limits.md#networking-limits) статьи.</span><span class="sxs-lookup"><span data-stu-id="eece1-174">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
    >

    - <span data-ttu-id="eece1-175">**Связать hello открытый конфигурацию IP-адреса ресурса tooa новый IP**</span><span class="sxs-lookup"><span data-stu-id="eece1-175">**Associate hello public IP address resource tooa new IP configuration**</span></span>
    
        <span data-ttu-id="eece1-176">Чтобы добавить общедоступный IP-адрес в новую IP-конфигурацию, необходимо добавить и частный IP-адрес, так как все IP-конфигурации должны иметь частный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="eece1-176">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="eece1-177">В конфигурацию можно добавить имеющийся ресурс общедоступного IP-адреса или создать новый.</span><span class="sxs-lookup"><span data-stu-id="eece1-177">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="eece1-178">toocreate новый, введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="eece1-178">toocreate a new one, enter hello following command:</span></span>
    
        ```powershell
        $myPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "myPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location `
        -AllocationMethod Static
        ```

        <span data-ttu-id="eece1-179">toocreate новой конфигурации IP с статический частный IP-адрес и связанные hello *myPublicIp3* общедоступный IP-адрес адрес ресурса, введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="eece1-179">toocreate a new IP configuration with a static private IP address and hello associated *myPublicIp3* public IP address resource, enter hello following command:</span></span>

        ```powershell
        Add-AzureRmNetworkInterfaceIpConfig `
        -Name IPConfig-4 `
        -NetworkInterface $myNIC `
        -Subnet $Subnet `
        -PrivateIpAddress 10.0.0.7 `
        -PublicIpAddress $myPublicIp3
        ```

    - <span data-ttu-id="eece1-180">**Связать hello открытый конфигурацию IP-адреса ресурса tooan существующие IP**</span><span class="sxs-lookup"><span data-stu-id="eece1-180">**Associate hello public IP address resource tooan existing IP configuration**</span></span>

        <span data-ttu-id="eece1-181">Открытый ресурс IP-адреса можно только связанные tooan IP-конфигурации, уже не связан.</span><span class="sxs-lookup"><span data-stu-id="eece1-181">A public IP address resource can only be associated tooan IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="eece1-182">Можно определить, имеет ли связанный общий IP-адрес IP-адрес, введя следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="eece1-182">You can determine whether an IP configuration has an associated public IP address by entering hello following command:</span></span>

        ```powershell
        $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
        ```

        <span data-ttu-id="eece1-183">Вы видите аналогичные toohello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="eece1-183">You see output similar toohello following:</span></span>

        ```     
        Name       PrivateIpAddress PublicIpAddress                                           Primary
        
        IPConfig-1 10.0.0.4         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress    True
        IPConfig-2 10.0.0.5         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress   False
        IpConfig-3 10.0.0.6                                                                     False
        ```

        <span data-ttu-id="eece1-184">С момента hello **PublicIpAddress** столбца для *IpConfig 3* является пустым, не открытого ресурса IP-адреса является в настоящее время связаны tooit.</span><span class="sxs-lookup"><span data-stu-id="eece1-184">Since hello **PublicIpAddress** column for *IpConfig-3* is blank, no public IP address resource is currently associated tooit.</span></span> <span data-ttu-id="eece1-185">Можно добавить существующие открытый IP адрес ресурса tooIpConfig-3, или введите hello, следующая команда toocreate один:</span><span class="sxs-lookup"><span data-stu-id="eece1-185">You can add an existing public IP address resource tooIpConfig-3, or enter hello following command toocreate one:</span></span>

        ```powershell
        $MyPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "MyPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location -AllocationMethod Static
        ```

        <span data-ttu-id="eece1-186">Введите следующую команду, общедоступный IP-адрес tooassociate hello адресов toohello существующие IP конфигурации ресурса с именем hello *IpConfig 3*:</span><span class="sxs-lookup"><span data-stu-id="eece1-186">Enter hello following command tooassociate hello public IP address resource toohello existing IP configuration named *IpConfig-3*:</span></span>
    
        ```powershell
        Set-AzureRmNetworkInterfaceIpConfig `
        -Name IpConfig-3 `
        -NetworkInterface $mynic `
        -Subnet $Subnet `
        -PublicIpAddress $myPublicIp3
        ```

6. <span data-ttu-id="eece1-187">Задайте hello Сетевых hello новой конфигурации IP, указав hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="eece1-187">Set hello NIC with hello new IP configuration by entering hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $MyNIC
    ```

7. <span data-ttu-id="eece1-188">Просмотр hello частных IP-адресов и hello открытый IP адрес ресурсы назначенного toohello hello сетевого Адаптера, введя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="eece1-188">View hello private IP addresses and hello public IP address resources assigned toohello NIC by entering hello following command:</span></span>

    ```powershell   
    $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
    ```
8. <span data-ttu-id="eece1-189">Добавьте hello частного IP адрес toohello операционной системы ВМ, выполнив действия hello для вашей операционной системы в hello [добавить IP-адресов операционной системы виртуальной Машины tooa](#os-config) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="eece1-189">Add hello private IP address toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="eece1-190">Не добавляйте hello открытый IP адрес toohello операционной системы.</span><span class="sxs-lookup"><span data-stu-id="eece1-190">Do not add hello public IP address toohello operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
