---
title: "Создание виртуальных машин Windows и управление ими с помощью модуля Azure PowerShell | Документация Майкрософт"
description: "Руководство по созданию виртуальных машин Windows и управлению ими с помощью модуля Azure PowerShell."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: ec1bb7834beb66dc28dd5b1db764bd358243292c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-windows-vms-with-the-azure-powershell-module"></a><span data-ttu-id="0abf7-103">Создание виртуальных машин Windows и управление ими с помощью модуля Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0abf7-103">Create and Manage Windows VMs with the Azure PowerShell module</span></span>

<span data-ttu-id="0abf7-104">Виртуальные машины Azure предоставляют полностью настраиваемую и гибкую вычислительную среду.</span><span class="sxs-lookup"><span data-stu-id="0abf7-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="0abf7-105">В этом руководстве рассматриваются основные элементы развертывания виртуальной машины Azure, например выбор ее размера, образа и ее развертывание.</span><span class="sxs-lookup"><span data-stu-id="0abf7-105">This tutorial covers basic Azure virtual machine deployment items such as selecting a VM size, selecting a VM image, and deploying a VM.</span></span> <span data-ttu-id="0abf7-106">Вы узнаете, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="0abf7-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0abf7-107">Создание виртуальной машины и подключение к ней</span><span class="sxs-lookup"><span data-stu-id="0abf7-107">Create and connect to a VM</span></span>
> * <span data-ttu-id="0abf7-108">Выбор и использование образов виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="0abf7-108">Select and use VM images</span></span>
> * <span data-ttu-id="0abf7-109">Просмотр и использование определенных размеров виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="0abf7-109">View and use specific VM sizes</span></span>
> * <span data-ttu-id="0abf7-110">Изменение размера виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="0abf7-110">Resize a VM</span></span>
> * <span data-ttu-id="0abf7-111">Просмотр виртуальной машины и оценка ее состояния</span><span class="sxs-lookup"><span data-stu-id="0abf7-111">View and understand VM state</span></span>

<span data-ttu-id="0abf7-112">Для работы с этим руководством требуется модуль Azure PowerShell версии не ниже 3.6.</span><span class="sxs-lookup"><span data-stu-id="0abf7-112">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="0abf7-113">Чтобы узнать версию, выполните команду ` Get-Module -ListAvailable AzureRM`.</span><span class="sxs-lookup"><span data-stu-id="0abf7-113">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="0abf7-114">Если вам необходимо выполнить обновление, ознакомьтесь со статьей, посвященной [установке модуля Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="0abf7-114">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="0abf7-115">Создать группу ресурсов</span><span class="sxs-lookup"><span data-stu-id="0abf7-115">Create resource group</span></span>

<span data-ttu-id="0abf7-116">Создайте группу ресурсов с помощью команды [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="0abf7-116">Create a resource group with the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> 

<span data-ttu-id="0abf7-117">Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="0abf7-117">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="0abf7-118">Группу ресурсов следует создавать до виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0abf7-118">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="0abf7-119">В этом примере создается группа ресурсов с именем *myResourceGroupVM* в регионе *EastUS*.</span><span class="sxs-lookup"><span data-stu-id="0abf7-119">In this example, a resource group named *myResourceGroupVM* is created in the *EastUS* region.</span></span> 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupVM -Location EastUS
```

<span data-ttu-id="0abf7-120">Группа ресурсов указывается при создании или изменении виртуальной машины, что показывается в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="0abf7-120">The resource group is specified when creating or modifying a VM, which can be seen throughout this tutorial.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="0abf7-121">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="0abf7-121">Create virtual machine</span></span>

<span data-ttu-id="0abf7-122">Виртуальная машина должна быть подключена к виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="0abf7-122">A virtual machine must be connected to a virtual network.</span></span> <span data-ttu-id="0abf7-123">Взаимодействие с виртуальной машиной осуществляется через сетевой адаптер, к которому привязан общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="0abf7-123">You communicate with the virtual machine using a public IP address through a network interface card.</span></span>

### <a name="create-virtual-network"></a><span data-ttu-id="0abf7-124">Создание виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="0abf7-124">Create virtual network</span></span>

<span data-ttu-id="0abf7-125">Создайте подсеть с помощью командлета [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="0abf7-125">Create a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="0abf7-126">Создайте виртуальную сеть с помощью командлета [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="0abf7-126">Create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 ` 
  -Subnet $subnetConfig
```
### <a name="create-public-ip-address"></a><span data-ttu-id="0abf7-127">Создание общедоступного IP-адреса</span><span class="sxs-lookup"><span data-stu-id="0abf7-127">Create public IP address</span></span>

<span data-ttu-id="0abf7-128">Создайте общедоступный IP-адрес с помощью командлета [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span><span class="sxs-lookup"><span data-stu-id="0abf7-128">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress ` 
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS ` 
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

### <a name="create-network-interface-card"></a><span data-ttu-id="0abf7-129">Создание сетевого адаптера</span><span class="sxs-lookup"><span data-stu-id="0abf7-129">Create network interface card</span></span>

<span data-ttu-id="0abf7-130">Создайте сетевой адаптер с помощью командлета [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="0abf7-130">Create a network interface card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span></span>

```powershell
$nic = New-AzureRmNetworkInterface `
  -ResourceGroupName myResourceGroupVM  `
  -Location EastUS `
  -Name myNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

### <a name="create-network-security-group"></a><span data-ttu-id="0abf7-131">Создание группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="0abf7-131">Create network security group</span></span>

<span data-ttu-id="0abf7-132">[Группа безопасности сети](../../virtual-network/virtual-networks-nsg.md) Azure управляет входящим и исходящим трафиком одной или нескольких виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="0abf7-132">An Azure [network security group](../../virtual-network/virtual-networks-nsg.md) (NSG) controls inbound and outbound traffic for one or many virtual machines.</span></span> <span data-ttu-id="0abf7-133">Правила группы безопасности сети разрешают или запрещают передачу сетевого трафика на определенный порт или диапазон портов.</span><span class="sxs-lookup"><span data-stu-id="0abf7-133">Network security group rules allow or deny network traffic on a specific port or port range.</span></span> <span data-ttu-id="0abf7-134">Эти правила также могут включать префикс адреса источника, чтобы на виртуальную машину передавался только трафик от определенного источника.</span><span class="sxs-lookup"><span data-stu-id="0abf7-134">These rules can also include a source address prefix so that only traffic originating at a predefined source can communicate with a virtual machine.</span></span> <span data-ttu-id="0abf7-135">Для доступа к веб-серверу IIS, который вы устанавливаете, необходимо добавить правило группы безопасности сети для входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="0abf7-135">To access the IIS webserver that you are installing, you must add an inbound NSG rule.</span></span>

<span data-ttu-id="0abf7-136">Чтобы создать его, используйте командлет [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="0abf7-136">To create an inbound NSG rule, use [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="0abf7-137">Следующий пример создает правило NSG *myNSGRule*, которое открывает порт *3389* для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0abf7-137">The following example creates an NSG rule named *myNSGRule* that opens port *3389* for the virtual machine:</span></span>

```powershell
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1000 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 3389 `
  -Access Allow
```

<span data-ttu-id="0abf7-138">Создайте группу безопасности сети *myNSGRule* с помощью командлета [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span><span class="sxs-lookup"><span data-stu-id="0abf7-138">Create the NSG using *myNSGRule* with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupVM `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRule
```

<span data-ttu-id="0abf7-139">Добавьте группу безопасности сети в подсеть виртуальной сети с помощью командлета [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="0abf7-139">Add the NSG to the subnet in the virtual network with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Set-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -VirtualNetwork $vnet `
    -NetworkSecurityGroup $nsg `
    -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="0abf7-140">Обновите виртуальную сеть, используя командлет [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="0abf7-140">Update the virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-machine"></a><span data-ttu-id="0abf7-141">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="0abf7-141">Create virtual machine</span></span>

<span data-ttu-id="0abf7-142">При создании виртуальной машины доступно несколько вариантов, таких как образ операционной системы, определение размера диска и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="0abf7-142">When creating a virtual machine, several options are available such as operating system image, disk sizing, and administrative credentials.</span></span> <span data-ttu-id="0abf7-143">В этом примере создается виртуальная машина *myVM*, на которой выполняется последняя версия Windows Server 2016 Datacenter.</span><span class="sxs-lookup"><span data-stu-id="0abf7-143">In this example, a virtual machine is created with a name of *myVM* running the latest version of Windows Server 2016 Datacenter.</span></span>

<span data-ttu-id="0abf7-144">Настройте на виртуальной машине имя пользователя и пароль для учетной записи администратора с помощью командлета [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="0abf7-144">Set the username and password needed for the administrator account on the virtual machine with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="0abf7-145">Создайте начальную конфигурацию виртуальной машины с помощью командлета [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig):</span><span class="sxs-lookup"><span data-stu-id="0abf7-145">Create the initial configuration for the virtual machine with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig):</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1
```

<span data-ttu-id="0abf7-146">Добавьте сведения об операционной системе в конфигурацию виртуальной машины с помощью командлета [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):</span><span class="sxs-lookup"><span data-stu-id="0abf7-146">Add the operating system information to the virtual machine configuration with [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):</span></span>

```powershell
$vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM `
    -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

<span data-ttu-id="0abf7-147">Добавьте сведения об образе в конфигурацию виртуальной машины с помощью командлета [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage):</span><span class="sxs-lookup"><span data-stu-id="0abf7-147">Add the image information to the virtual machine configuration with [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage):</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
```

<span data-ttu-id="0abf7-148">Добавьте сведения о настройках диска операционной системы в конфигурацию виртуальной машины с помощью командлета [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk):</span><span class="sxs-lookup"><span data-stu-id="0abf7-148">Add the operating system disk settings to the virtual machine configuration with [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk):</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
```

<span data-ttu-id="0abf7-149">Добавьте ранее созданный сетевой адаптер в конфигурацию виртуальной машины с помощью командлета [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="0abf7-149">Add the network interface card that you previously created to the virtual machine configuration with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

<span data-ttu-id="0abf7-150">Создайте виртуальную машину с помощью командлета [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="0abf7-150">Create the virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroupVM -Location EastUS -VM $vm
```

## <a name="connect-to-vm"></a><span data-ttu-id="0abf7-151">Подключение к виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="0abf7-151">Connect to VM</span></span>

<span data-ttu-id="0abf7-152">После завершения развертывания создайте подключение к удаленному рабочему столу виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0abf7-152">After the deployment has completed, create a remote desktop connection with the virtual machine.</span></span>

<span data-ttu-id="0abf7-153">Выполните приведенные ниже команды, чтобы получить общедоступный IP-адрес виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0abf7-153">Run the following commands to return the public IP address of the virtual machine.</span></span> <span data-ttu-id="0abf7-154">Запишите этот IP-адрес. Он потребуется, чтобы подключиться к виртуальной машине в браузере и проверить возможность подключения к Интернету на следующем этапе.</span><span class="sxs-lookup"><span data-stu-id="0abf7-154">Take note of this IP Address so you can connect to it with your browser to test web connectivity in a future step.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroupVM  | Select IpAddress
```

<span data-ttu-id="0abf7-155">Используйте следующую команду для создания сеанса удаленного рабочего стола с виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="0abf7-155">Use the following command to create a remote desktop session with the virtual machine.</span></span> <span data-ttu-id="0abf7-156">Замените IP-адрес значением *publicIPAddress* виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0abf7-156">Replace the IP address with the *publicIPAddress* of your virtual machine.</span></span> <span data-ttu-id="0abf7-157">При появлении запроса введите учетные данные, использованные при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0abf7-157">When prompted, enter the credentials used when creating the virtual machine.</span></span>

```powershell
mstsc /v:<publicIpAddress>
```

## <a name="understand-vm-images"></a><span data-ttu-id="0abf7-158">Описание образов виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="0abf7-158">Understand VM images</span></span>

<span data-ttu-id="0abf7-159">Azure Marketplace содержит множество образов виртуальных машин, которые можно использовать для создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0abf7-159">The Azure marketplace includes many virtual machine images that can be used to create a new virtual machine.</span></span> <span data-ttu-id="0abf7-160">На предыдущих шагах виртуальная машина создавалась с помощью образа Windows Server 2016-Datacenter.</span><span class="sxs-lookup"><span data-stu-id="0abf7-160">In the previous steps, a virtual machine was created using the Windows Server 2016-Datacenter image.</span></span> <span data-ttu-id="0abf7-161">На этом шаге модуль PowerShell используется для поиска других образов Windows на сайте Marketplace, которые можно также использовать для создания виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="0abf7-161">In this step, the PowerShell module is used to search the marketplace for other Windows images, which can also as a base for new VMs.</span></span> <span data-ttu-id="0abf7-162">Этот процесс состоит из поиска издателя, предложения и имени образа (SKU).</span><span class="sxs-lookup"><span data-stu-id="0abf7-162">This process consists of finding the publisher, offer, and the image name (Sku).</span></span> 

<span data-ttu-id="0abf7-163">Используйте команду [Get-AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), чтобы получить список издателей образов.</span><span class="sxs-lookup"><span data-stu-id="0abf7-163">Use the [Get-AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) command to return a list of image publishers.</span></span>  

```powersehll
Get-AzureRmVMImagePublisher -Location "EastUS"
```

<span data-ttu-id="0abf7-164">Используйте команду [Get-AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), чтобы получить список предложений образов.</span><span class="sxs-lookup"><span data-stu-id="0abf7-164">Use the [Get-AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) to return a list of image offers.</span></span> <span data-ttu-id="0abf7-165">С помощью этой команды возвращается список, отфильтрованный по указанному издателю.</span><span class="sxs-lookup"><span data-stu-id="0abf7-165">With this command, the returned list is filtered on the specified publisher.</span></span> 

```powershell
Get-AzureRmVMImageOffer -Location "EastUS" -PublisherName "MicrosoftWindowsServer"
```

```powershell
Offer             PublisherName          Location
-----             -------------          -------- 
Windows-HUB       MicrosoftWindowsServer EastUS 
WindowsServer     MicrosoftWindowsServer EastUS   
WindowsServer-HUB MicrosoftWindowsServer EastUS   
```

<span data-ttu-id="0abf7-166">Команда [Get-AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) отфильтрует список по имени издателя и названию предложения, отобразив список имен образов.</span><span class="sxs-lookup"><span data-stu-id="0abf7-166">The [Get-AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) command will then filter on the publisher and offer name to return a list of image names.</span></span>

```powershell
Get-AzureRmVMImageSku -Location "EastUS" -PublisherName "MicrosoftWindowsServer" -Offer "WindowsServer"
```

```powershell
Skus                            Offer         PublisherName          Location
----                            -----         -------------          --------
2008-R2-SP1                     WindowsServer MicrosoftWindowsServer EastUS  
2008-R2-SP1-BYOL                WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter-BYOL            WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter              WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter-BYOL         WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-Server-Core     WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-with-Containers WindowsServer MicrosoftWindowsServer EastUS  
2016-Nano-Server                WindowsServer MicrosoftWindowsServer EastUS
```

<span data-ttu-id="0abf7-167">Эти сведения можно использовать для развертывания виртуальной машины на основе конкретного образа.</span><span class="sxs-lookup"><span data-stu-id="0abf7-167">This information can be used to deploy a VM with a specific image.</span></span> <span data-ttu-id="0abf7-168">В этом примере задается имя образа для объекта виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0abf7-168">This example sets the image name on the VM object.</span></span> <span data-ttu-id="0abf7-169">Полные инструкции по развертыванию приведены в предыдущих примерах в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="0abf7-169">Refer to the previous examples in this tutorial for complete deployment steps.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter-with-Containers `
    -Version latest
```

## <a name="understand-vm-sizes"></a><span data-ttu-id="0abf7-170">Описание размеров виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="0abf7-170">Understand VM sizes</span></span>

<span data-ttu-id="0abf7-171">Размер виртуальной машины определяет количество выделяемых ей вычислительных ресурсов, таких как ЦП, GPU и память.</span><span class="sxs-lookup"><span data-stu-id="0abf7-171">A virtual machine size determines the amount of compute resources such as CPU, GPU, and memory that are made available to the virtual machine.</span></span> <span data-ttu-id="0abf7-172">Виртуальные машины нужно создавать с размером, подходящим для ожидаемой рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="0abf7-172">Virtual machines need to be created with a size appropriate for the expect work load.</span></span> <span data-ttu-id="0abf7-173">При увеличении рабочей нагрузки размер существующей виртуальной машины может быть изменен.</span><span class="sxs-lookup"><span data-stu-id="0abf7-173">If workload increases, an existing virtual machine can be resized.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="0abf7-174">Размеры виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="0abf7-174">VM Sizes</span></span>

<span data-ttu-id="0abf7-175">В приведенной ниже таблицы указаны категории размеров и примеры использования.</span><span class="sxs-lookup"><span data-stu-id="0abf7-175">The following table categorizes sizes into use cases.</span></span>  

| <span data-ttu-id="0abf7-176">Тип</span><span class="sxs-lookup"><span data-stu-id="0abf7-176">Type</span></span>                     | <span data-ttu-id="0abf7-177">Размеры</span><span class="sxs-lookup"><span data-stu-id="0abf7-177">Sizes</span></span>           |    <span data-ttu-id="0abf7-178">Описание</span><span class="sxs-lookup"><span data-stu-id="0abf7-178">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0abf7-179">Универсальные</span><span class="sxs-lookup"><span data-stu-id="0abf7-179">General purpose</span></span>         |<span data-ttu-id="0abf7-180">DSv2, Dv2, DS, D, Av2, A0–A7</span><span class="sxs-lookup"><span data-stu-id="0abf7-180">DSv2, Dv2, DS, D, Av2, A0-7</span></span>| <span data-ttu-id="0abf7-181">Сбалансированное соотношение ресурсов ЦП и памяти.</span><span class="sxs-lookup"><span data-stu-id="0abf7-181">Balanced CPU-to-memory.</span></span> <span data-ttu-id="0abf7-182">Идеально подходят для разработки и тестирования малых и средних приложений и решений для обработки данных.</span><span class="sxs-lookup"><span data-stu-id="0abf7-182">Ideal for dev / test and small to medium applications and data solutions.</span></span>  |
| <span data-ttu-id="0abf7-183">Оптимизированные для вычислений</span><span class="sxs-lookup"><span data-stu-id="0abf7-183">Compute optimized</span></span>      | <span data-ttu-id="0abf7-184">Fs, F</span><span class="sxs-lookup"><span data-stu-id="0abf7-184">Fs, F</span></span>             | <span data-ttu-id="0abf7-185">Высокое соотношение ресурсов ЦП и памяти.</span><span class="sxs-lookup"><span data-stu-id="0abf7-185">High CPU-to-memory.</span></span> <span data-ttu-id="0abf7-186">Подходят для приложений со средним объемом трафика, сетевых устройств и пакетных процессов.</span><span class="sxs-lookup"><span data-stu-id="0abf7-186">Good for medium traffic applications, network appliances, and batch processes.</span></span>        |
| <span data-ttu-id="0abf7-187">Оптимизированные для памяти</span><span class="sxs-lookup"><span data-stu-id="0abf7-187">Memory optimized</span></span>       | <span data-ttu-id="0abf7-188">GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="0abf7-188">GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="0abf7-189">Высокое соотношение ресурсов памяти и числа ядер.</span><span class="sxs-lookup"><span data-stu-id="0abf7-189">High memory-to-core.</span></span> <span data-ttu-id="0abf7-190">Отлично подходят для реляционных баз данных, кэша среднего и большого объема, а также выполняющейся в памяти аналитики.</span><span class="sxs-lookup"><span data-stu-id="0abf7-190">Great for relational databases, medium to large caches, and in-memory analytics.</span></span>                 |
| <span data-ttu-id="0abf7-191">Оптимизированные для хранилища</span><span class="sxs-lookup"><span data-stu-id="0abf7-191">Storage optimized</span></span>       | <span data-ttu-id="0abf7-192">Ls</span><span class="sxs-lookup"><span data-stu-id="0abf7-192">Ls</span></span>                | <span data-ttu-id="0abf7-193">Высокая пропускная способность дисков и количество операций ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="0abf7-193">High disk throughput and IO.</span></span> <span data-ttu-id="0abf7-194">Идеальный вариант для работы с большими данными, а также с базами данных SQL и NoSQL.</span><span class="sxs-lookup"><span data-stu-id="0abf7-194">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| <span data-ttu-id="0abf7-195">Графический процессор</span><span class="sxs-lookup"><span data-stu-id="0abf7-195">GPU</span></span>           | <span data-ttu-id="0abf7-196">NV, NC</span><span class="sxs-lookup"><span data-stu-id="0abf7-196">NV, NC</span></span>            | <span data-ttu-id="0abf7-197">Специализированные виртуальные машины, предназначенные для ресурсоемкой отрисовки изображений и редактирования видео.</span><span class="sxs-lookup"><span data-stu-id="0abf7-197">Specialized VMs targeted for heavy graphic rendering and video editing.</span></span>       |
| <span data-ttu-id="0abf7-198">Высокопроизводительные</span><span class="sxs-lookup"><span data-stu-id="0abf7-198">High performance</span></span> | <span data-ttu-id="0abf7-199">H, A8–A11</span><span class="sxs-lookup"><span data-stu-id="0abf7-199">H, A8-11</span></span>          | <span data-ttu-id="0abf7-200">Виртуальные машины с самыми мощными ЦП, для которых можно настроить сетевые интерфейсы с высокой пропускной способностью (RDMA).</span><span class="sxs-lookup"><span data-stu-id="0abf7-200">Our most powerful CPU VMs with optional high-throughput network interfaces (RDMA).</span></span> 


### <a name="find-available-vm-sizes"></a><span data-ttu-id="0abf7-201">Поиск всех доступных размеров виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="0abf7-201">Find available VM sizes</span></span>

<span data-ttu-id="0abf7-202">Чтобы просмотреть список доступных размеров виртуальных машин в определенном регионе, используйте команду [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize).</span><span class="sxs-lookup"><span data-stu-id="0abf7-202">To see a list of VM sizes available in a particular region, use the [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) command.</span></span>

```powershell
Get-AzureRmVMSize -Location EastUS
```

## <a name="resize-a-vm"></a><span data-ttu-id="0abf7-203">Изменение размера виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="0abf7-203">Resize a VM</span></span>

<span data-ttu-id="0abf7-204">После развертывания виртуальной машины ее размер можно изменить, чтобы увеличить или уменьшить выделенные ей ресурсы.</span><span class="sxs-lookup"><span data-stu-id="0abf7-204">After a VM has been deployed, it can be resized to increase or decrease resource allocation.</span></span>

<span data-ttu-id="0abf7-205">Перед изменением размера виртуальной машины проверьте, доступен ли желаемый размер в текущем кластере виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="0abf7-205">Before resizing a VM, check if the desired size is available on the current VM cluster.</span></span> <span data-ttu-id="0abf7-206">Команда [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) возвращает список размеров.</span><span class="sxs-lookup"><span data-stu-id="0abf7-206">The [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) command returns a list of sizes.</span></span> 

```powershell
Get-AzureRmVMSize -ResourceGroupName myResourceGroupVM -VMName myVM 
```

<span data-ttu-id="0abf7-207">Если желаемый размер доступен, то размер виртуальной машины можно изменить во включенном состоянии, однако виртуальную машину нужно будет перезагрузить.</span><span class="sxs-lookup"><span data-stu-id="0abf7-207">If the desired size is available, the VM can be resized from a powered-on state, however it is rebooted during the operation.</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM 
$vm.HardwareProfile.VmSize = "Standard_D4"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
```

<span data-ttu-id="0abf7-208">Если желаемый размер в текущем кластере недоступен, то перед изменением размера виртуальную машину нужно освободить.</span><span class="sxs-lookup"><span data-stu-id="0abf7-208">If the desired size is not on the current cluster, the VM needs to be deallocated before the resize operation can occur.</span></span> <span data-ttu-id="0abf7-209">Обратите внимание на то, что после повторного включения виртуальной машины все данные на временном диске будут удалены, а общедоступный IP-адрес изменится, если только не используется статический IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="0abf7-209">Note, when the VM is powered back on, any data on the temp disk are removed, and the public IP address change unless a static IP address is being used.</span></span> 

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM
$vm.HardwareProfile.VmSize = "Standard_F4s"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
Start-AzureRmVM -ResourceGroupName myResourceGroupVM  -Name $vm.name
```

## <a name="vm-power-states"></a><span data-ttu-id="0abf7-210">Состояния включенной виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="0abf7-210">VM power states</span></span>

<span data-ttu-id="0abf7-211">Включенная виртуальная машина Azure может находиться в одном из многих состояний.</span><span class="sxs-lookup"><span data-stu-id="0abf7-211">An Azure VM can have one of many power states.</span></span> <span data-ttu-id="0abf7-212">Это состояние отражает текущее состояние виртуальной машины с точки зрения гипервизора.</span><span class="sxs-lookup"><span data-stu-id="0abf7-212">This state represents the current state of the VM from the standpoint of the hypervisor.</span></span> 

### <a name="power-states"></a><span data-ttu-id="0abf7-213">Состояния включения</span><span class="sxs-lookup"><span data-stu-id="0abf7-213">Power states</span></span>

| <span data-ttu-id="0abf7-214">Состояние включения</span><span class="sxs-lookup"><span data-stu-id="0abf7-214">Power State</span></span> | <span data-ttu-id="0abf7-215">Описание</span><span class="sxs-lookup"><span data-stu-id="0abf7-215">Description</span></span>
|----|----|
| <span data-ttu-id="0abf7-216">Starting</span><span class="sxs-lookup"><span data-stu-id="0abf7-216">Starting</span></span> | <span data-ttu-id="0abf7-217">Указывает, что виртуальная машина запущена.</span><span class="sxs-lookup"><span data-stu-id="0abf7-217">Indicates the virtual machine is being started.</span></span> |
| <span data-ttu-id="0abf7-218">Выполнение</span><span class="sxs-lookup"><span data-stu-id="0abf7-218">Running</span></span> | <span data-ttu-id="0abf7-219">Указывает, что виртуальная машина работает.</span><span class="sxs-lookup"><span data-stu-id="0abf7-219">Indicates that the virtual machine is running.</span></span> |
| <span data-ttu-id="0abf7-220">Остановка</span><span class="sxs-lookup"><span data-stu-id="0abf7-220">Stopping</span></span> | <span data-ttu-id="0abf7-221">Указывает, что виртуальная машина останавливается.</span><span class="sxs-lookup"><span data-stu-id="0abf7-221">Indicates that the virtual machine is being stopped.</span></span> | 
| <span data-ttu-id="0abf7-222">Остановлено</span><span class="sxs-lookup"><span data-stu-id="0abf7-222">Stopped</span></span> | <span data-ttu-id="0abf7-223">Указывает, что виртуальная машина остановлена.</span><span class="sxs-lookup"><span data-stu-id="0abf7-223">Indicates that the virtual machine is stopped.</span></span> <span data-ttu-id="0abf7-224">Обратите внимание, что за виртуальные машины в остановленном состоянии по-прежнему взимается плата за вычислительные операции.</span><span class="sxs-lookup"><span data-stu-id="0abf7-224">Note that virtual machines in the stopped state still incur compute charges.</span></span>  |
| <span data-ttu-id="0abf7-225">Отмена выделения</span><span class="sxs-lookup"><span data-stu-id="0abf7-225">Deallocating</span></span> | <span data-ttu-id="0abf7-226">Указывает, что виртуальная машина освобождается.</span><span class="sxs-lookup"><span data-stu-id="0abf7-226">Indicates that the virtual machine is being deallocated.</span></span> |
| <span data-ttu-id="0abf7-227">Освобождено</span><span class="sxs-lookup"><span data-stu-id="0abf7-227">Deallocated</span></span> | <span data-ttu-id="0abf7-228">Указывает, что виртуальная машина полностью удалена из гипервизора, но по-прежнему доступна в плоскости управления.</span><span class="sxs-lookup"><span data-stu-id="0abf7-228">Indicates that the virtual machine is completely removed from the hypervisor but still available in the control plane.</span></span> <span data-ttu-id="0abf7-229">За виртуальные машины в освобожденном состоянии не взимается плата за вычислительные операции.</span><span class="sxs-lookup"><span data-stu-id="0abf7-229">Virtual machines in the Deallocated state do not incur compute charges.</span></span> |
| - | <span data-ttu-id="0abf7-230">Указывает, что состояние включенной виртуальной машины неизвестно.</span><span class="sxs-lookup"><span data-stu-id="0abf7-230">Indicates that the power state of the virtual machine is unknown.</span></span> |

### <a name="find-power-state"></a><span data-ttu-id="0abf7-231">Поиск состояние включения</span><span class="sxs-lookup"><span data-stu-id="0abf7-231">Find power state</span></span>

<span data-ttu-id="0abf7-232">Чтобы получить состояние конкретной виртуальной машины, используйте команду [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="0abf7-232">To retrieve the state of a particular VM, use the [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) command.</span></span> <span data-ttu-id="0abf7-233">Необходимо указать допустимое имя виртуальной машины и группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0abf7-233">Be sure to specify a valid name for a virtual machine and resource group.</span></span> 

```powershell
Get-AzureRmVM `
    -ResourceGroupName myResourceGroup `
    -Name myVM `
    -Status | Select @{n="Status"; e={$_.Statuses[1].Code}}
```

<span data-ttu-id="0abf7-234">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="0abf7-234">Output:</span></span>

```powershell
Status
------
PowerState/running
```

## <a name="management-tasks"></a><span data-ttu-id="0abf7-235">Задачи управления</span><span class="sxs-lookup"><span data-stu-id="0abf7-235">Management tasks</span></span>

<span data-ttu-id="0abf7-236">В течение жизненного цикла виртуальной машины можно выполнять задачи управления, такие как запуск, остановка или удаление виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0abf7-236">During the lifecycle of a virtual machine, you may want to run management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="0abf7-237">Кроме того, можно создавать скрипты для автоматизации повторяющихся или сложных задач.</span><span class="sxs-lookup"><span data-stu-id="0abf7-237">Additionally, you may want to create scripts to automate repetitive or complex tasks.</span></span> <span data-ttu-id="0abf7-238">С помощью Azure PowerShell можно выполнять множество распространенных задач управления в командной строке или в скриптах.</span><span class="sxs-lookup"><span data-stu-id="0abf7-238">Using Azure PowerShell, many common management tasks can be run from the command line or in scripts.</span></span>

### <a name="stop-virtual-machine"></a><span data-ttu-id="0abf7-239">Прекращение работы виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="0abf7-239">Stop virtual machine</span></span>

<span data-ttu-id="0abf7-240">Остановите и освободите виртуальную машину с помощью командлета [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="0abf7-240">Stop and deallocate a virtual machine with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm):</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
```

<span data-ttu-id="0abf7-241">Если вы хотите сохранить виртуальную машину в подготовленном состоянии, задайте параметр -StayProvisioned.</span><span class="sxs-lookup"><span data-stu-id="0abf7-241">If you want to keep the virtual machine in a provisioned state, use the -StayProvisioned parameter.</span></span>

### <a name="start-virtual-machine"></a><span data-ttu-id="0abf7-242">Запуск виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="0abf7-242">Start virtual machine</span></span>

```powershell
Start-AzureRmVM -ResourceGroupName myResourceGroupVM -Name myVM
```

### <a name="delete-resource-group"></a><span data-ttu-id="0abf7-243">Удалить группу ресурсов</span><span class="sxs-lookup"><span data-stu-id="0abf7-243">Delete resource group</span></span>

<span data-ttu-id="0abf7-244">При удалении группы ресурсов будут также удалены все ресурсы, содержащиеся в ней.</span><span class="sxs-lookup"><span data-stu-id="0abf7-244">Deleting a resource group also deletes all resources contained within.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroupVM -Force
```

## <a name="next-steps"></a><span data-ttu-id="0abf7-245">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0abf7-245">Next steps</span></span>

<span data-ttu-id="0abf7-246">В рамках этого руководства вы изучили основы создания виртуальной машины и управления ею. Вы узнали, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="0abf7-246">In this tutorial, you learned about basic VM creation and management such as how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0abf7-247">Создание виртуальной машины и подключение к ней</span><span class="sxs-lookup"><span data-stu-id="0abf7-247">Create and connect to a VM</span></span>
> * <span data-ttu-id="0abf7-248">Выбор и использование образов виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="0abf7-248">Select and use VM images</span></span>
> * <span data-ttu-id="0abf7-249">Просмотр и использование определенных размеров виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="0abf7-249">View and use specific VM sizes</span></span>
> * <span data-ttu-id="0abf7-250">Изменение размера виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="0abf7-250">Resize a VM</span></span>
> * <span data-ttu-id="0abf7-251">Просмотр виртуальной машины и оценка ее состояния</span><span class="sxs-lookup"><span data-stu-id="0abf7-251">View and understand VM state</span></span>

<span data-ttu-id="0abf7-252">Перейдите к следующему руководству, чтобы узнать о дисках виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="0abf7-252">Advance to the next tutorial to learn about VM disks.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="0abf7-253">Управление дисками Azure с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0abf7-253">Create and Manage VM disks</span></span>](./tutorial-manage-data-disk.md)
