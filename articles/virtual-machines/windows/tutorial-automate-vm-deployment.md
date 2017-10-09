---
title: "aaaCustomize виртуальной Машине Windows в Azure | Документы Microsoft"
description: "Узнайте, как toouse hello расширение пользовательского скрипта и хранилище ключей toocustomize виртуальные машины Windows в Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: c03b2bb6d70875134c63ea2fe4c2e2c1777c2188
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="84f58-103">Как toocustomize виртуальной машине в Azure</span><span class="sxs-lookup"><span data-stu-id="84f58-103">How toocustomize a Windows virtual machine in Azure</span></span>
<span data-ttu-id="84f58-104">Обычно требуется tooconfigure виртуальных машин (ВМ) в виде краткое и согласованное, средства автоматизации.</span><span class="sxs-lookup"><span data-stu-id="84f58-104">tooconfigure virtual machines (VMs) in a quick and consistent manner, some form of automation is typically desired.</span></span> <span data-ttu-id="84f58-105">Общие toocustomize подход ВМ Windows — toouse [пользовательский скрипт расширения для Windows](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="84f58-105">A common approach toocustomize a Windows VM is toouse [Custom Script Extension for Windows](extensions-customscript.md).</span></span> <span data-ttu-id="84f58-106">Из этого руководства вы узнаете, как выполнить следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="84f58-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="84f58-107">Использовать настраиваемое расширение скриптов hello tooinstall IIS</span><span class="sxs-lookup"><span data-stu-id="84f58-107">Use hello Custom Script Extension tooinstall IIS</span></span>
> * <span data-ttu-id="84f58-108">Создание виртуальной Машины, которая использует hello настраиваемое расширение скриптов</span><span class="sxs-lookup"><span data-stu-id="84f58-108">Create a VM that uses hello Custom Script Extension</span></span>
> * <span data-ttu-id="84f58-109">Просмотр выполняющегося сайт IIS после применения расширения hello</span><span class="sxs-lookup"><span data-stu-id="84f58-109">View a running IIS site after hello extension is applied</span></span>

<span data-ttu-id="84f58-110">Этот учебник требует hello Azure PowerShell модуль версии 3.6 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="84f58-110">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="84f58-111">Запустите ` Get-Module -ListAvailable AzureRM` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="84f58-111">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="84f58-112">Получить tooupgrade [установите Azure PowerShell модуль](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="84f58-112">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="custom-script-extension-overview"></a><span data-ttu-id="84f58-113">Общие сведения о расширении настраиваемых сценариев</span><span class="sxs-lookup"><span data-stu-id="84f58-113">Custom script extension overview</span></span>
<span data-ttu-id="84f58-114">Hello настраиваемое расширение скриптов загружает и запускает сценарии на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="84f58-114">hello Custom Script Extension downloads and executes scripts on Azure VMs.</span></span> <span data-ttu-id="84f58-115">Это расширение можно использовать для настройки после развертывания, установки программного обеспечения и других задач настройки или управления.</span><span class="sxs-lookup"><span data-stu-id="84f58-115">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="84f58-116">Скрипты можно загружается из хранилища Azure или GitHub, или предоставить toohello портал Azure во время выполнения модуля.</span><span class="sxs-lookup"><span data-stu-id="84f58-116">Scripts can be downloaded from Azure storage or GitHub, or provided toohello Azure portal at extension run time.</span></span>

<span data-ttu-id="84f58-117">Hello расширение пользовательского скрипта интегрируется с шаблоны Azure Resource Manager и также можно выполнить с помощью hello Azure CLI, PowerShell, портал Azure или hello API REST Azure виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="84f58-117">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="84f58-118">Hello настраиваемое расширение скриптов можно использовать с Windows и виртуальных машин Linux.</span><span class="sxs-lookup"><span data-stu-id="84f58-118">You can use hello Custom Script Extension with both Windows and Linux VMs.</span></span>


## <a name="create-virtual-machine"></a><span data-ttu-id="84f58-119">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="84f58-119">Create virtual machine</span></span>
<span data-ttu-id="84f58-120">Прежде чем создать виртуальную машину, выполните команду [az group create](/powershell/module/azurerm.resources/new-azurermresourcegroup) для создания группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="84f58-120">Before you can create a VM, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="84f58-121">Hello следующий пример создает группу ресурсов с именем *myResourceGroupAutomate* в hello *EastUS* расположение:</span><span class="sxs-lookup"><span data-stu-id="84f58-121">hello following example creates a resource group named *myResourceGroupAutomate* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupAutomate -Location EastUS
```

<span data-ttu-id="84f58-122">Набор администратору имя пользователя и пароль для виртуальных машин hello с [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="84f58-122">Set an administrator username and password for hello VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="84f58-123">Теперь можно создавать hello виртуальной Машины с [New AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="84f58-123">Now you can create hello VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="84f58-124">Hello следующий пример создает компоненты hello необходимые виртуальной сети, конфигурации hello ОС и затем создает Виртуальную машину с именем *myVM*:</span><span class="sxs-lookup"><span data-stu-id="84f58-124">hello following example creates hello required virtual network components, hello OS configuration, and then creates a VM named *myVM*:</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleRDP  `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleWWW  `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1001 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80 `
    -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP,$nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2016-Datacenter -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName myResourceGroupAutomate -Location EastUS -VM $vmConfig
```

<span data-ttu-id="84f58-125">Он занимает несколько минут для ресурсов hello и toobe виртуальная машина создана.</span><span class="sxs-lookup"><span data-stu-id="84f58-125">It takes a few minutes for hello resources and VM toobe created.</span></span>


## <a name="automate-iis-install"></a><span data-ttu-id="84f58-126">Автоматизация установки IIS</span><span class="sxs-lookup"><span data-stu-id="84f58-126">Automate IIS install</span></span>
<span data-ttu-id="84f58-127">Используйте [AzureRmVMExtension набор](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello настраиваемого расширения скриптов.</span><span class="sxs-lookup"><span data-stu-id="84f58-127">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello Custom Script Extension.</span></span> <span data-ttu-id="84f58-128">Здравствуйте, выполняется расширение `powershell Add-WindowsFeature Web-Server` tooinstall hello веб-сервере IIS, а затем обновления hello *Default.htm* страницы tooshow hello имя узла виртуальной Машины hello:</span><span class="sxs-lookup"><span data-stu-id="84f58-128">hello extension runs `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS webserver and then updates hello *Default.htm* page tooshow hello hostname of hello VM:</span></span>

```powershell
Set-AzureRmVMExtension -ResourceGroupName myResourceGroupAutomate `
    -ExtensionName IIS `
    -VMName myVM `
    -Publisher Microsoft.Compute `
    -ExtensionType CustomScriptExtension `
    -TypeHandlerVersion 1.4 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
    -Location EastUS
```


## <a name="test-web-site"></a><span data-ttu-id="84f58-129">Проверка веб-сайта</span><span class="sxs-lookup"><span data-stu-id="84f58-129">Test web site</span></span>
<span data-ttu-id="84f58-130">Получить hello общедоступный IP-адрес балансировки нагрузки, с [Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="84f58-130">Obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="84f58-131">Hello следующий пример извлекает hello IP-адрес для *myPublicIP* созданную ранее:</span><span class="sxs-lookup"><span data-stu-id="84f58-131">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Name myPublicIP | select IpAddress
```

<span data-ttu-id="84f58-132">После этого можно вводить hello общедоступный IP-адрес в tooa веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="84f58-132">You can then enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="84f58-133">отображается Hello веб-сайта, включая имя узла виртуальной Машины hello hello балансировки нагрузки, hello распределенных tooas трафика в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="84f58-133">hello website is displayed, including hello hostname of hello VM that hello load balancer distributed traffic tooas in hello following example:</span></span>

![Выполнение веб-сайта IIS](./media/tutorial-automate-vm-deployment/running-iis-website.png)


## <a name="next-steps"></a><span data-ttu-id="84f58-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="84f58-135">Next steps</span></span>

<span data-ttu-id="84f58-136">В этом учебнике автоматической hello, службы IIS устанавливаются на виртуальной Машине.</span><span class="sxs-lookup"><span data-stu-id="84f58-136">In this tutorial, you automated hello IIS install on a VM.</span></span> <span data-ttu-id="84f58-137">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="84f58-137">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="84f58-138">Использовать настраиваемое расширение скриптов hello tooinstall IIS</span><span class="sxs-lookup"><span data-stu-id="84f58-138">Use hello Custom Script Extension tooinstall IIS</span></span>
> * <span data-ttu-id="84f58-139">Создание виртуальной Машины, которая использует hello настраиваемое расширение скриптов</span><span class="sxs-lookup"><span data-stu-id="84f58-139">Create a VM that uses hello Custom Script Extension</span></span>
> * <span data-ttu-id="84f58-140">Просмотр выполняющегося сайт IIS после применения расширения hello</span><span class="sxs-lookup"><span data-stu-id="84f58-140">View a running IIS site after hello extension is applied</span></span>

<span data-ttu-id="84f58-141">Как переместить следующий учебник toolearn toohello toocreate пользовательских образов виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="84f58-141">Advance toohello next tutorial toolearn how toocreate custom VM images.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="84f58-142">Создание образа настраиваемой виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="84f58-142">Create custom VM images</span></span>](./tutorial-custom-images.md)
