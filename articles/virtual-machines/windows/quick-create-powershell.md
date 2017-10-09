---
title: "Быстрый запуск - aaaAzure создания виртуальной Машины Windows PowerShell | Документы Microsoft"
description: "Быстро Узнайте toocreate виртуальных машинах с помощью PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5e92435bf7ee443a01c158fed91c356363e2f425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell"></a><span data-ttu-id="febed-103">Создание виртуальной машины Windows с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="febed-103">Create a Windows virtual machine with PowerShell</span></span>

<span data-ttu-id="febed-104">используется toocreate и управления ресурсами Azure из командной строки PowerShell hello, или в сценариях Hello модуля Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="febed-104">hello Azure PowerShell module is used toocreate and manage Azure resources from hello PowerShell command line or in scripts.</span></span> <span data-ttu-id="febed-105">В этом руководстве рассматривается использование PowerShell toocreate и виртуальная машина Azure под управлением Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="febed-105">This guide details using PowerShell toocreate and Azure virtual machine running Windows Server 2016.</span></span> <span data-ttu-id="febed-106">После завершения развертывания мы подключения toohello сервера и установить службы IIS.</span><span class="sxs-lookup"><span data-stu-id="febed-106">Once deployment is complete, we connect toohello server and install IIS.</span></span>  

<span data-ttu-id="febed-107">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="febed-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="febed-108">В этом кратком руководстве требует hello Azure PowerShell модуль версии 3.6 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="febed-108">This quick start requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="febed-109">Запустите ` Get-Module -ListAvailable AzureRM` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="febed-109">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="febed-110">Если требуется tooinstall или обновления, см. раздел [установите Azure PowerShell модуль](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="febed-110">If you need tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="febed-111">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="febed-111">Log in tooAzure</span></span>

<span data-ttu-id="febed-112">Войдите в подписку Azure совместно с hello tooyour `Login-AzureRmAccount` команды и выполните hello на экране инструкциям.</span><span class="sxs-lookup"><span data-stu-id="febed-112">Log in tooyour Azure subscription with hello `Login-AzureRmAccount` command and follow hello on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="febed-113">Создать группу ресурсов</span><span class="sxs-lookup"><span data-stu-id="febed-113">Create resource group</span></span>

<span data-ttu-id="febed-114">Создайте группу ресурсов Azure с помощью командлета [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="febed-114">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="febed-115">Группа ресурсов — это логический контейнер, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="febed-115">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location EastUS
```

## <a name="create-networking-resources"></a><span data-ttu-id="febed-116">Создание сетевых ресурсов</span><span class="sxs-lookup"><span data-stu-id="febed-116">Create networking resources</span></span>

### <a name="create-a-virtual-network-subnet-and-a-public-ip-address"></a><span data-ttu-id="febed-117">Создайте виртуальную сеть, подсеть и общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="febed-117">Create a virtual network, subnet, and a public IP address.</span></span> 
<span data-ttu-id="febed-118">Эти ресурсы, используемые tooprovide сетевого подключения toohello виртуальной машины и подключите его toohello Интернета.</span><span class="sxs-lookup"><span data-stu-id="febed-118">These resources are used tooprovide network connectivity toohello virtual machine and connect it toohello internet.</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork -ResourceGroupName myResourceGroup -Location EastUS `
    -Name MYvNET -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup -Location EastUS `
    -AllocationMethod Static -IdleTimeoutInMinutes 4 -Name "mypublicdns$(Get-Random)"
```

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a><span data-ttu-id="febed-119">Создайте группу безопасности сети и правило группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="febed-119">Create a network security group and a network security group rule.</span></span> 
<span data-ttu-id="febed-120">группы безопасности сети Hello защищает hello виртуальной машины, с помощью правила входящего и исходящего трафика.</span><span class="sxs-lookup"><span data-stu-id="febed-120">hello network security group secures hello virtual machine using inbound and outbound rules.</span></span> <span data-ttu-id="febed-121">В нашем случае создается правило для входящего трафика порта 3389, которое разрешает входящие подключения к удаленному рабочему столу.</span><span class="sxs-lookup"><span data-stu-id="febed-121">In this case, an inbound rule is created for port 3389, which allows incoming remote desktop connections.</span></span> <span data-ttu-id="febed-122">Также мы хотим toocreate входящее правило для порта 80, который позволяет входящего веб-трафика.</span><span class="sxs-lookup"><span data-stu-id="febed-122">We also want toocreate an inbound rule for port 80, which allows incoming web traffic.</span></span>

```powershell
# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP  -Protocol Tcp `
    -Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 3389 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleWWW  -Protocol Tcp `
    -Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName myResourceGroup -Location EastUS `
    -Name myNetworkSecurityGroup -SecurityRules $nsgRuleRDP,$nsgRuleWeb
```

### <a name="create-a-network-card-for-hello-virtual-machine"></a><span data-ttu-id="febed-123">Создайте сетевой карты для hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="febed-123">Create a network card for hello virtual machine.</span></span> 
<span data-ttu-id="febed-124">Создание сетевого адаптера с [New AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) для hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="febed-124">Create a network card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) for hello virtual machine.</span></span> <span data-ttu-id="febed-125">Hello сетевой адаптер подключается подсети tooa hello виртуальных машин, группы безопасности сети и общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="febed-125">hello network card connects hello virtual machine tooa subnet, network security group, and public IP address.</span></span>

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a><span data-ttu-id="febed-126">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="febed-126">Create virtual machine</span></span>

<span data-ttu-id="febed-127">Создайте конфигурацию виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="febed-127">Create a virtual machine configuration.</span></span> <span data-ttu-id="febed-128">Такая настройка включает hello параметров, используемых при развертывании виртуальной машины hello, такие как изображения, размер и проверку подлинности конфигурации виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="febed-128">This configuration includes hello settings that are used when deploying hello virtual machine such as a virtual machine image, size, and authentication configuration.</span></span> <span data-ttu-id="febed-129">При выполнении этого шага будут запрошены учетные данные.</span><span class="sxs-lookup"><span data-stu-id="febed-129">When running this step, you are prompted for credentials.</span></span> <span data-ttu-id="febed-130">вводимые значения Hello настраиваются как hello имя пользователя и пароль для виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="febed-130">hello values that you enter are configured as hello user name and password for hello virtual machine.</span></span>

```powershell
# Define a credential object
$cred = Get-Credential

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
    Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
    Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer -Offer WindowsServer `
    -Skus 2016-Datacenter -Version latest | Add-AzureRmVMNetworkInterface -Id $nic.Id
```

<span data-ttu-id="febed-131">Создание виртуальной машины hello с [New AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="febed-131">Create hello virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location EastUS -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a><span data-ttu-id="febed-132">Подключиться к компьютеру toovirtual</span><span class="sxs-lookup"><span data-stu-id="febed-132">Connect toovirtual machine</span></span>

<span data-ttu-id="febed-133">После завершения развертывания hello создания удаленного рабочего стола с виртуальной машиной hello.</span><span class="sxs-lookup"><span data-stu-id="febed-133">After hello deployment has completed, create a remote desktop connection with hello virtual machine.</span></span>

<span data-ttu-id="febed-134">Используйте hello [Get AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) команды tooreturn hello общедоступный IP-адрес виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="febed-134">Use hello [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) command tooreturn hello public IP address of hello virtual machine.</span></span> <span data-ttu-id="febed-135">Запишите этот IP-адрес для подключения tooit с вашего браузера tootest соединения через сеть на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="febed-135">Take note of this IP Address so you can connect tooit with your browser tootest web connectivity in a future step.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

<span data-ttu-id="febed-136">Используйте hello следующая команда toocreate сеанс удаленного рабочего стола с виртуальной машиной hello.</span><span class="sxs-lookup"><span data-stu-id="febed-136">Use hello following command toocreate a remote desktop session with hello virtual machine.</span></span> <span data-ttu-id="febed-137">Замените hello hello IP-адрес *publicIPAddress* вашей виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="febed-137">Replace hello IP address with hello *publicIPAddress* of your virtual machine.</span></span> <span data-ttu-id="febed-138">При появлении запроса введите hello учетные данные, используемые при создании виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="febed-138">When prompted, enter hello credentials used when creating hello virtual machine.</span></span>

```bash 
mstsc /v:<publicIpAddress>
```

## <a name="install-iis-via-powershell"></a><span data-ttu-id="febed-139">Установка IIS с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="febed-139">Install IIS via PowerShell</span></span>

<span data-ttu-id="febed-140">Теперь, когда вы вошли в toohello виртуальной Машине Azure, можно использовать одну строку PowerShell tooinstall IIS и включить hello локальном брандмауэре правило tooallow веб-трафика.</span><span class="sxs-lookup"><span data-stu-id="febed-140">Now that you have logged in toohello Azure VM, you can use a single line of PowerShell tooinstall IIS and enable hello local firewall rule tooallow web traffic.</span></span> <span data-ttu-id="febed-141">Откройте командную строку PowerShell и выполните следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="febed-141">Open a PowerShell prompt and run hello following command:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-hello-iis-welcome-page"></a><span data-ttu-id="febed-142">Представление hello страницу приветствия IIS</span><span class="sxs-lookup"><span data-stu-id="febed-142">View hello IIS welcome page</span></span>

<span data-ttu-id="febed-143">С установленными службами IIS и порт 80, теперь открыт на ВМ из hello Интернета можно использовать веб-браузере choice tooview hello по умолчанию службы IIS страницу приветствия.</span><span class="sxs-lookup"><span data-stu-id="febed-143">With IIS installed and port 80 now open on your VM from hello Internet, you can use a web browser of your choice tooview hello default IIS welcome page.</span></span> <span data-ttu-id="febed-144">Быть убедиться, что hello toouse *publicIpAddress* приведенной выше toovisit страница по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="febed-144">Be sure toouse hello *publicIpAddress* you documented above toovisit hello default page.</span></span> 

![Сайт IIS по умолчанию](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="febed-146">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="febed-146">Clean up resources</span></span>

<span data-ttu-id="febed-147">Если больше не нужны, можно использовать hello [AzureRmResourceGroup удаление](/powershell/module/azurerm.resources/remove-azurermresourcegroup) команд группы ресурсов tooremove hello, виртуальных Машин и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="febed-147">When no longer needed, you can use hello [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="febed-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="febed-148">Next steps</span></span>

<span data-ttu-id="febed-149">Из этого краткого руководства вы узнали о том, как развернуть простую виртуальную машину, о правилах группы безопасности сети и об установке веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="febed-149">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="febed-150">toolearn Дополнительные сведения о виртуальных машинах Azure, продолжить toohello учебника для виртуальных машин Windows.</span><span class="sxs-lookup"><span data-stu-id="febed-150">toolearn more about Azure virtual machines, continue toohello tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="febed-151">Создание виртуальных машин Windows и управление ими с помощью модуля Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="febed-151">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
