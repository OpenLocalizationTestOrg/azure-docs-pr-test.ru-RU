---
title: "aaaCreate и управление виртуальными машинами Windows с hello модуля Azure PowerShell | Документы Microsoft"
description: "Учебник — Создание и управление виртуальными машинами Windows с hello модуля Azure PowerShell"
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
ms.openlocfilehash: 20adcb673ef4de683e6ad82d048a9625a1dc838c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-with-hello-azure-powershell-module"></a><span data-ttu-id="973fc-103">Создание и управление виртуальными машинами Windows с hello модуля Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="973fc-103">Create and Manage Windows VMs with hello Azure PowerShell module</span></span>

<span data-ttu-id="973fc-104">Виртуальные машины Azure предоставляют полностью настраиваемую и гибкую вычислительную среду.</span><span class="sxs-lookup"><span data-stu-id="973fc-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="973fc-105">В этом руководстве рассматриваются основные элементы развертывания виртуальной машины Azure, например выбор ее размера, образа и ее развертывание.</span><span class="sxs-lookup"><span data-stu-id="973fc-105">This tutorial covers basic Azure virtual machine deployment items such as selecting a VM size, selecting a VM image, and deploying a VM.</span></span> <span data-ttu-id="973fc-106">Вы узнаете, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="973fc-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="973fc-107">Создать и присоединить tooa виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="973fc-107">Create and connect tooa VM</span></span>
> * <span data-ttu-id="973fc-108">Выбор и использование образов виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="973fc-108">Select and use VM images</span></span>
> * <span data-ttu-id="973fc-109">Просмотр и использование определенных размеров виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="973fc-109">View and use specific VM sizes</span></span>
> * <span data-ttu-id="973fc-110">Изменение размера виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="973fc-110">Resize a VM</span></span>
> * <span data-ttu-id="973fc-111">Просмотр виртуальной машины и оценка ее состояния</span><span class="sxs-lookup"><span data-stu-id="973fc-111">View and understand VM state</span></span>

<span data-ttu-id="973fc-112">Этот учебник требует hello Azure PowerShell модуль версии 3.6 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="973fc-112">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="973fc-113">Запустите ` Get-Module -ListAvailable AzureRM` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="973fc-113">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="973fc-114">Получить tooupgrade [установите Azure PowerShell модуль](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="973fc-114">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="973fc-115">Создать группу ресурсов</span><span class="sxs-lookup"><span data-stu-id="973fc-115">Create resource group</span></span>

<span data-ttu-id="973fc-116">Создание группы ресурсов с hello [New AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) команды.</span><span class="sxs-lookup"><span data-stu-id="973fc-116">Create a resource group with hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> 

<span data-ttu-id="973fc-117">Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="973fc-117">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="973fc-118">Группу ресурсов следует создавать до виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="973fc-118">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="973fc-119">В этом примере имя группы ресурсов *myResourceGroupVM* создается в hello *EastUS* области.</span><span class="sxs-lookup"><span data-stu-id="973fc-119">In this example, a resource group named *myResourceGroupVM* is created in hello *EastUS* region.</span></span> 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupVM -Location EastUS
```

<span data-ttu-id="973fc-120">Группа ресурсов Hello указывается при создании или изменении виртуальных Машин, который можно увидеть на протяжении этого учебника.</span><span class="sxs-lookup"><span data-stu-id="973fc-120">hello resource group is specified when creating or modifying a VM, which can be seen throughout this tutorial.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="973fc-121">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="973fc-121">Create virtual machine</span></span>

<span data-ttu-id="973fc-122">Виртуальная машина должна быть tooa подключенной виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="973fc-122">A virtual machine must be connected tooa virtual network.</span></span> <span data-ttu-id="973fc-123">Взаимодействовать с виртуальной машиной hello, используя общедоступный IP-адрес через сетевой адаптер.</span><span class="sxs-lookup"><span data-stu-id="973fc-123">You communicate with hello virtual machine using a public IP address through a network interface card.</span></span>

### <a name="create-virtual-network"></a><span data-ttu-id="973fc-124">Создание виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="973fc-124">Create virtual network</span></span>

<span data-ttu-id="973fc-125">Создайте подсеть с помощью командлета [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="973fc-125">Create a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="973fc-126">Создайте виртуальную сеть с помощью командлета [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="973fc-126">Create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 ` 
  -Subnet $subnetConfig
```
### <a name="create-public-ip-address"></a><span data-ttu-id="973fc-127">Создание общедоступного IP-адреса</span><span class="sxs-lookup"><span data-stu-id="973fc-127">Create public IP address</span></span>

<span data-ttu-id="973fc-128">Создайте общедоступный IP-адрес с помощью командлета [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span><span class="sxs-lookup"><span data-stu-id="973fc-128">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress ` 
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS ` 
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

### <a name="create-network-interface-card"></a><span data-ttu-id="973fc-129">Создание сетевого адаптера</span><span class="sxs-lookup"><span data-stu-id="973fc-129">Create network interface card</span></span>

<span data-ttu-id="973fc-130">Создайте сетевой адаптер с помощью командлета [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="973fc-130">Create a network interface card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span></span>

```powershell
$nic = New-AzureRmNetworkInterface `
  -ResourceGroupName myResourceGroupVM  `
  -Location EastUS `
  -Name myNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

### <a name="create-network-security-group"></a><span data-ttu-id="973fc-131">Создание группы безопасности сети</span><span class="sxs-lookup"><span data-stu-id="973fc-131">Create network security group</span></span>

<span data-ttu-id="973fc-132">[Группа безопасности сети](../../virtual-network/virtual-networks-nsg.md) Azure управляет входящим и исходящим трафиком одной или нескольких виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="973fc-132">An Azure [network security group](../../virtual-network/virtual-networks-nsg.md) (NSG) controls inbound and outbound traffic for one or many virtual machines.</span></span> <span data-ttu-id="973fc-133">Правила группы безопасности сети разрешают или запрещают передачу сетевого трафика на определенный порт или диапазон портов.</span><span class="sxs-lookup"><span data-stu-id="973fc-133">Network security group rules allow or deny network traffic on a specific port or port range.</span></span> <span data-ttu-id="973fc-134">Эти правила также могут включать префикс адреса источника, чтобы на виртуальную машину передавался только трафик от определенного источника.</span><span class="sxs-lookup"><span data-stu-id="973fc-134">These rules can also include a source address prefix so that only traffic originating at a predefined source can communicate with a virtual machine.</span></span> <span data-ttu-id="973fc-135">tooaccess hello IIS веб-сервер, установке, необходимо добавить правило для входящего трафика NSG.</span><span class="sxs-lookup"><span data-stu-id="973fc-135">tooaccess hello IIS webserver that you are installing, you must add an inbound NSG rule.</span></span>

<span data-ttu-id="973fc-136">использовать toocreate входящее правило NSG [AzureRmNetworkSecurityRuleConfig добавить](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="973fc-136">toocreate an inbound NSG rule, use [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="973fc-137">Hello следующий пример создает NSG правило с именем *myNSGRule* , открывает порт *3389* для hello виртуальной машины:</span><span class="sxs-lookup"><span data-stu-id="973fc-137">hello following example creates an NSG rule named *myNSGRule* that opens port *3389* for hello virtual machine:</span></span>

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

<span data-ttu-id="973fc-138">Создание с помощью NSG hello *myNSGRule* с [New AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span><span class="sxs-lookup"><span data-stu-id="973fc-138">Create hello NSG using *myNSGRule* with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupVM `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRule
```

<span data-ttu-id="973fc-139">Добавить подсеть toohello NSG hello в hello виртуальной сети с [AzureRmVirtualNetworkSubnetConfig набор](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="973fc-139">Add hello NSG toohello subnet in hello virtual network with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Set-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -VirtualNetwork $vnet `
    -NetworkSecurityGroup $nsg `
    -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="973fc-140">Обновление hello виртуальную сеть с [AzureRmVirtualNetwork набор](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="973fc-140">Update hello virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-machine"></a><span data-ttu-id="973fc-141">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="973fc-141">Create virtual machine</span></span>

<span data-ttu-id="973fc-142">При создании виртуальной машины доступно несколько вариантов, таких как образ операционной системы, определение размера диска и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="973fc-142">When creating a virtual machine, several options are available such as operating system image, disk sizing, and administrative credentials.</span></span> <span data-ttu-id="973fc-143">В этом примере создается виртуальная машина с именем *myVM* выполнение hello последнюю версию Windows Server 2016 Datacenter.</span><span class="sxs-lookup"><span data-stu-id="973fc-143">In this example, a virtual machine is created with a name of *myVM* running hello latest version of Windows Server 2016 Datacenter.</span></span>

<span data-ttu-id="973fc-144">Укажите имя пользователя hello и пароль для учетной записи администратора hello на виртуальной машине hello [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="973fc-144">Set hello username and password needed for hello administrator account on hello virtual machine with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="973fc-145">Создание начальной настройки hello для hello виртуальной машины с [New AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig):</span><span class="sxs-lookup"><span data-stu-id="973fc-145">Create hello initial configuration for hello virtual machine with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig):</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1
```

<span data-ttu-id="973fc-146">Добавить конфигурацию виртуальной машины toohello сведения операционной системы hello с [AzureRmVMOperatingSystem набор](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):</span><span class="sxs-lookup"><span data-stu-id="973fc-146">Add hello operating system information toohello virtual machine configuration with [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):</span></span>

```powershell
$vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM `
    -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

<span data-ttu-id="973fc-147">Добавить конфигурацию виртуальной машины toohello сведения изображения hello с [AzureRmVMSourceImage набор](/powershell/module/azurerm.compute/set-azurermvmsourceimage):</span><span class="sxs-lookup"><span data-stu-id="973fc-147">Add hello image information toohello virtual machine configuration with [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage):</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
```

<span data-ttu-id="973fc-148">Добавить hello операционной системы диска параметры toohello конфигурация виртуальной машины с [AzureRmVMOSDisk набор](/powershell/module/azurerm.compute/set-azurermvmosdisk):</span><span class="sxs-lookup"><span data-stu-id="973fc-148">Add hello operating system disk settings toohello virtual machine configuration with [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk):</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
```

<span data-ttu-id="973fc-149">Добавить hello сетевого интерфейса, созданный ранее toohello конфигурация виртуальной машины с [AzureRmVMNetworkInterface добавить](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="973fc-149">Add hello network interface card that you previously created toohello virtual machine configuration with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

<span data-ttu-id="973fc-150">Создание виртуальной машины hello с [New AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="973fc-150">Create hello virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroupVM -Location EastUS -VM $vm
```

## <a name="connect-toovm"></a><span data-ttu-id="973fc-151">Подключение tooVM</span><span class="sxs-lookup"><span data-stu-id="973fc-151">Connect tooVM</span></span>

<span data-ttu-id="973fc-152">После завершения развертывания hello создания удаленного рабочего стола с виртуальной машиной hello.</span><span class="sxs-lookup"><span data-stu-id="973fc-152">After hello deployment has completed, create a remote desktop connection with hello virtual machine.</span></span>

<span data-ttu-id="973fc-153">Выполните следующие команды tooreturn hello общедоступный IP-адрес виртуальной машины hello hello.</span><span class="sxs-lookup"><span data-stu-id="973fc-153">Run hello following commands tooreturn hello public IP address of hello virtual machine.</span></span> <span data-ttu-id="973fc-154">Запишите этот IP-адрес для подключения tooit с вашего браузера tootest соединения через сеть на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="973fc-154">Take note of this IP Address so you can connect tooit with your browser tootest web connectivity in a future step.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroupVM  | Select IpAddress
```

<span data-ttu-id="973fc-155">Используйте hello следующая команда toocreate сеанс удаленного рабочего стола с виртуальной машиной hello.</span><span class="sxs-lookup"><span data-stu-id="973fc-155">Use hello following command toocreate a remote desktop session with hello virtual machine.</span></span> <span data-ttu-id="973fc-156">Замените hello hello IP-адрес *publicIPAddress* вашей виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="973fc-156">Replace hello IP address with hello *publicIPAddress* of your virtual machine.</span></span> <span data-ttu-id="973fc-157">При появлении запроса введите hello учетные данные, используемые при создании виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="973fc-157">When prompted, enter hello credentials used when creating hello virtual machine.</span></span>

```powershell
mstsc /v:<publicIpAddress>
```

## <a name="understand-vm-images"></a><span data-ttu-id="973fc-158">Описание образов виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="973fc-158">Understand VM images</span></span>

<span data-ttu-id="973fc-159">Hello Azure marketplace включает много образы виртуальных машин, которые можно использовать toocreate новой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="973fc-159">hello Azure marketplace includes many virtual machine images that can be used toocreate a new virtual machine.</span></span> <span data-ttu-id="973fc-160">В предыдущих шагах hello виртуальная машина создана с помощью образа Windows Server 2016 — Datacenter hello.</span><span class="sxs-lookup"><span data-stu-id="973fc-160">In hello previous steps, a virtual machine was created using hello Windows Server 2016-Datacenter image.</span></span> <span data-ttu-id="973fc-161">На этом этапе модуль PowerShell hello — магазин hello toosearch используется для других образов Windows, которые можно также в качестве базы для новых виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="973fc-161">In this step, hello PowerShell module is used toosearch hello marketplace for other Windows images, which can also as a base for new VMs.</span></span> <span data-ttu-id="973fc-162">Этот процесс состоит из поиск hello издателя, предложения и имя образа hello (конфигурация).</span><span class="sxs-lookup"><span data-stu-id="973fc-162">This process consists of finding hello publisher, offer, and hello image name (Sku).</span></span> 

<span data-ttu-id="973fc-163">Используйте hello [Get AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) tooreturn команда список издателей изображения.</span><span class="sxs-lookup"><span data-stu-id="973fc-163">Use hello [Get-AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) command tooreturn a list of image publishers.</span></span>  

```powersehll
Get-AzureRmVMImagePublisher -Location "EastUS"
```

<span data-ttu-id="973fc-164">Используйте hello [Get AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) tooreturn список предложений изображения.</span><span class="sxs-lookup"><span data-stu-id="973fc-164">Use hello [Get-AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) tooreturn a list of image offers.</span></span> <span data-ttu-id="973fc-165">С помощью этой команды hello вернуть список будет отфильтрован по указанным издателем hello.</span><span class="sxs-lookup"><span data-stu-id="973fc-165">With this command, hello returned list is filtered on hello specified publisher.</span></span> 

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

<span data-ttu-id="973fc-166">Hello [Get AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) команды используется затем для фильтрации tooreturn имя издателя и предложение hello списка имен образов.</span><span class="sxs-lookup"><span data-stu-id="973fc-166">hello [Get-AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) command will then filter on hello publisher and offer name tooreturn a list of image names.</span></span>

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

<span data-ttu-id="973fc-167">Эти сведения можно использовать toodeploy виртуальной Машины с помощью специального образа.</span><span class="sxs-lookup"><span data-stu-id="973fc-167">This information can be used toodeploy a VM with a specific image.</span></span> <span data-ttu-id="973fc-168">В этом примере задает имя образа hello hello объекта виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="973fc-168">This example sets hello image name on hello VM object.</span></span> <span data-ttu-id="973fc-169">См. в этом учебнике шаги завершения развертывания toohello предыдущих примерах.</span><span class="sxs-lookup"><span data-stu-id="973fc-169">Refer toohello previous examples in this tutorial for complete deployment steps.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter-with-Containers `
    -Version latest
```

## <a name="understand-vm-sizes"></a><span data-ttu-id="973fc-170">Описание размеров виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="973fc-170">Understand VM sizes</span></span>

<span data-ttu-id="973fc-171">Размер виртуальной машины определяет hello объем вычислительных ресурсов, таких как ЦП, графического Процессора и памяти, сделанные доступными toohello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="973fc-171">A virtual machine size determines hello amount of compute resources such as CPU, GPU, and memory that are made available toohello virtual machine.</span></span> <span data-ttu-id="973fc-172">Виртуальные машины должны toobe создана с размером соответствующего для hello ожидать рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="973fc-172">Virtual machines need toobe created with a size appropriate for hello expect work load.</span></span> <span data-ttu-id="973fc-173">При увеличении рабочей нагрузки размер существующей виртуальной машины может быть изменен.</span><span class="sxs-lookup"><span data-stu-id="973fc-173">If workload increases, an existing virtual machine can be resized.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="973fc-174">Размеры виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="973fc-174">VM Sizes</span></span>

<span data-ttu-id="973fc-175">в следующей таблице Hello относит размеры вариантов использования.</span><span class="sxs-lookup"><span data-stu-id="973fc-175">hello following table categorizes sizes into use cases.</span></span>  

| <span data-ttu-id="973fc-176">Тип</span><span class="sxs-lookup"><span data-stu-id="973fc-176">Type</span></span>                     | <span data-ttu-id="973fc-177">Размеры</span><span class="sxs-lookup"><span data-stu-id="973fc-177">Sizes</span></span>           |    <span data-ttu-id="973fc-178">Описание</span><span class="sxs-lookup"><span data-stu-id="973fc-178">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="973fc-179">Универсальные</span><span class="sxs-lookup"><span data-stu-id="973fc-179">General purpose</span></span>         |<span data-ttu-id="973fc-180">DSv2, Dv2, DS, D, Av2, A0–A7</span><span class="sxs-lookup"><span data-stu-id="973fc-180">DSv2, Dv2, DS, D, Av2, A0-7</span></span>| <span data-ttu-id="973fc-181">Сбалансированное соотношение ресурсов ЦП и памяти.</span><span class="sxs-lookup"><span data-stu-id="973fc-181">Balanced CPU-to-memory.</span></span> <span data-ttu-id="973fc-182">Идеально подходит для разработки и тестирования и малого toomedium приложениям и данным решения.</span><span class="sxs-lookup"><span data-stu-id="973fc-182">Ideal for dev / test and small toomedium applications and data solutions.</span></span>  |
| <span data-ttu-id="973fc-183">Оптимизированные для вычислений</span><span class="sxs-lookup"><span data-stu-id="973fc-183">Compute optimized</span></span>      | <span data-ttu-id="973fc-184">Fs, F</span><span class="sxs-lookup"><span data-stu-id="973fc-184">Fs, F</span></span>             | <span data-ttu-id="973fc-185">Высокое соотношение ресурсов ЦП и памяти.</span><span class="sxs-lookup"><span data-stu-id="973fc-185">High CPU-to-memory.</span></span> <span data-ttu-id="973fc-186">Подходят для приложений со средним объемом трафика, сетевых устройств и пакетных процессов.</span><span class="sxs-lookup"><span data-stu-id="973fc-186">Good for medium traffic applications, network appliances, and batch processes.</span></span>        |
| <span data-ttu-id="973fc-187">Оптимизированные для памяти</span><span class="sxs-lookup"><span data-stu-id="973fc-187">Memory optimized</span></span>       | <span data-ttu-id="973fc-188">GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="973fc-188">GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="973fc-189">Высокое соотношение ресурсов памяти и числа ядер.</span><span class="sxs-lookup"><span data-stu-id="973fc-189">High memory-to-core.</span></span> <span data-ttu-id="973fc-190">Идеально подходит для реляционных баз данных, кэши средний toolarge и аналитики в памяти.</span><span class="sxs-lookup"><span data-stu-id="973fc-190">Great for relational databases, medium toolarge caches, and in-memory analytics.</span></span>                 |
| <span data-ttu-id="973fc-191">Оптимизированные для хранилища</span><span class="sxs-lookup"><span data-stu-id="973fc-191">Storage optimized</span></span>       | <span data-ttu-id="973fc-192">Ls</span><span class="sxs-lookup"><span data-stu-id="973fc-192">Ls</span></span>                | <span data-ttu-id="973fc-193">Высокая пропускная способность дисков и количество операций ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="973fc-193">High disk throughput and IO.</span></span> <span data-ttu-id="973fc-194">Идеальный вариант для работы с большими данными, а также с базами данных SQL и NoSQL.</span><span class="sxs-lookup"><span data-stu-id="973fc-194">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| <span data-ttu-id="973fc-195">Графический процессор</span><span class="sxs-lookup"><span data-stu-id="973fc-195">GPU</span></span>           | <span data-ttu-id="973fc-196">NV, NC</span><span class="sxs-lookup"><span data-stu-id="973fc-196">NV, NC</span></span>            | <span data-ttu-id="973fc-197">Специализированные виртуальные машины, предназначенные для ресурсоемкой отрисовки изображений и редактирования видео.</span><span class="sxs-lookup"><span data-stu-id="973fc-197">Specialized VMs targeted for heavy graphic rendering and video editing.</span></span>       |
| <span data-ttu-id="973fc-198">Высокопроизводительные</span><span class="sxs-lookup"><span data-stu-id="973fc-198">High performance</span></span> | <span data-ttu-id="973fc-199">H, A8–A11</span><span class="sxs-lookup"><span data-stu-id="973fc-199">H, A8-11</span></span>          | <span data-ttu-id="973fc-200">Виртуальные машины с самыми мощными ЦП, для которых можно настроить сетевые интерфейсы с высокой пропускной способностью (RDMA).</span><span class="sxs-lookup"><span data-stu-id="973fc-200">Our most powerful CPU VMs with optional high-throughput network interfaces (RDMA).</span></span> 


### <a name="find-available-vm-sizes"></a><span data-ttu-id="973fc-201">Поиск всех доступных размеров виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="973fc-201">Find available VM sizes</span></span>

<span data-ttu-id="973fc-202">toosee список виртуальных Машин размеров, доступных в определенном регионе, используйте hello [Get AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) команды.</span><span class="sxs-lookup"><span data-stu-id="973fc-202">toosee a list of VM sizes available in a particular region, use hello [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) command.</span></span>

```powershell
Get-AzureRmVMSize -Location EastUS
```

## <a name="resize-a-vm"></a><span data-ttu-id="973fc-203">Изменение размера виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="973fc-203">Resize a VM</span></span>

<span data-ttu-id="973fc-204">После развертывания виртуальной Машины, ее можно изменять размер tooincrease или уменьшить выделения ресурсов.</span><span class="sxs-lookup"><span data-stu-id="973fc-204">After a VM has been deployed, it can be resized tooincrease or decrease resource allocation.</span></span>

<span data-ttu-id="973fc-205">Перед изменением размера виртуальной Машины, проверьте hello желаемый размер доступен на hello текущего кластера виртуальных Машин.</span><span class="sxs-lookup"><span data-stu-id="973fc-205">Before resizing a VM, check if hello desired size is available on hello current VM cluster.</span></span> <span data-ttu-id="973fc-206">Hello [Get AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) команда возвращает список размеров.</span><span class="sxs-lookup"><span data-stu-id="973fc-206">hello [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) command returns a list of sizes.</span></span> 

```powershell
Get-AzureRmVMSize -ResourceGroupName myResourceGroupVM -VMName myVM 
```

<span data-ttu-id="973fc-207">При желании hello, что он доступен hello виртуальной Машины могут быть изменены из состояния включении, однако он не будет перезагружен во время операции hello.</span><span class="sxs-lookup"><span data-stu-id="973fc-207">If hello desired size is available, hello VM can be resized from a powered-on state, however it is rebooted during hello operation.</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM 
$vm.HardwareProfile.VmSize = "Standard_D4"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
```

<span data-ttu-id="973fc-208">Если hello желаемый размер находится не на hello текущего кластера, hello ВМ потребностей, может произойти toobe освобождена до hello операцию изменения размера.</span><span class="sxs-lookup"><span data-stu-id="973fc-208">If hello desired size is not on hello current cluster, hello VM needs toobe deallocated before hello resize operation can occur.</span></span> <span data-ttu-id="973fc-209">Обратите внимание, что при hello виртуальная машина не будет включено обратно, удаляются все данные на диске временный hello и изменяйте hello общедоступный IP-адрес, если используется статический IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="973fc-209">Note, when hello VM is powered back on, any data on hello temp disk are removed, and hello public IP address change unless a static IP address is being used.</span></span> 

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM
$vm.HardwareProfile.VmSize = "Standard_F4s"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
Start-AzureRmVM -ResourceGroupName myResourceGroupVM  -Name $vm.name
```

## <a name="vm-power-states"></a><span data-ttu-id="973fc-210">Состояния включенной виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="973fc-210">VM power states</span></span>

<span data-ttu-id="973fc-211">Включенная виртуальная машина Azure может находиться в одном из многих состояний.</span><span class="sxs-lookup"><span data-stu-id="973fc-211">An Azure VM can have one of many power states.</span></span> <span data-ttu-id="973fc-212">Это состояние представляет текущее состояние hello hello виртуальной Машины с точки зрения hello hello низкоуровневой оболочки.</span><span class="sxs-lookup"><span data-stu-id="973fc-212">This state represents hello current state of hello VM from hello standpoint of hello hypervisor.</span></span> 

### <a name="power-states"></a><span data-ttu-id="973fc-213">Состояния включения</span><span class="sxs-lookup"><span data-stu-id="973fc-213">Power states</span></span>

| <span data-ttu-id="973fc-214">Состояние включения</span><span class="sxs-lookup"><span data-stu-id="973fc-214">Power State</span></span> | <span data-ttu-id="973fc-215">Описание</span><span class="sxs-lookup"><span data-stu-id="973fc-215">Description</span></span>
|----|----|
| <span data-ttu-id="973fc-216">Starting</span><span class="sxs-lookup"><span data-stu-id="973fc-216">Starting</span></span> | <span data-ttu-id="973fc-217">Указывает, что hello виртуальная машина запускается.</span><span class="sxs-lookup"><span data-stu-id="973fc-217">Indicates hello virtual machine is being started.</span></span> |
| <span data-ttu-id="973fc-218">Выполнение</span><span class="sxs-lookup"><span data-stu-id="973fc-218">Running</span></span> | <span data-ttu-id="973fc-219">Указывает, что выполняется hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="973fc-219">Indicates that hello virtual machine is running.</span></span> |
| <span data-ttu-id="973fc-220">Остановка</span><span class="sxs-lookup"><span data-stu-id="973fc-220">Stopping</span></span> | <span data-ttu-id="973fc-221">Указывает, что выполняется остановка виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="973fc-221">Indicates that hello virtual machine is being stopped.</span></span> | 
| <span data-ttu-id="973fc-222">Остановлено</span><span class="sxs-lookup"><span data-stu-id="973fc-222">Stopped</span></span> | <span data-ttu-id="973fc-223">Указывает, что этот hello виртуальная машина остановлена.</span><span class="sxs-lookup"><span data-stu-id="973fc-223">Indicates that hello virtual machine is stopped.</span></span> <span data-ttu-id="973fc-224">Обратите внимание, что виртуальные машины в состоянии остановки hello взиматься плата за вычислительные операции.</span><span class="sxs-lookup"><span data-stu-id="973fc-224">Note that virtual machines in hello stopped state still incur compute charges.</span></span>  |
| <span data-ttu-id="973fc-225">Отмена выделения</span><span class="sxs-lookup"><span data-stu-id="973fc-225">Deallocating</span></span> | <span data-ttu-id="973fc-226">Указывает, что выполняется освобождение hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="973fc-226">Indicates that hello virtual machine is being deallocated.</span></span> |
| <span data-ttu-id="973fc-227">Освобождено</span><span class="sxs-lookup"><span data-stu-id="973fc-227">Deallocated</span></span> | <span data-ttu-id="973fc-228">Указывает, что для этой виртуальной машине hello полностью удалены из hello низкоуровневой оболочки, но по-прежнему доступны в плоскости управления hello.</span><span class="sxs-lookup"><span data-stu-id="973fc-228">Indicates that hello virtual machine is completely removed from hello hypervisor but still available in hello control plane.</span></span> <span data-ttu-id="973fc-229">Виртуальные машины в состоянии освобождена hello не взимается вычислений.</span><span class="sxs-lookup"><span data-stu-id="973fc-229">Virtual machines in hello Deallocated state do not incur compute charges.</span></span> |
| - | <span data-ttu-id="973fc-230">Указывает на неизвестное состояние электропитания hello hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="973fc-230">Indicates that hello power state of hello virtual machine is unknown.</span></span> |

### <a name="find-power-state"></a><span data-ttu-id="973fc-231">Поиск состояние включения</span><span class="sxs-lookup"><span data-stu-id="973fc-231">Find power state</span></span>

<span data-ttu-id="973fc-232">состояние конкретной виртуальной Машины, используйте hello hello tooretrieve [Get AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) команды.</span><span class="sxs-lookup"><span data-stu-id="973fc-232">tooretrieve hello state of a particular VM, use hello [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) command.</span></span> <span data-ttu-id="973fc-233">Быть toospecify убедиться, что допустимое имя для виртуальной машины и группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="973fc-233">Be sure toospecify a valid name for a virtual machine and resource group.</span></span> 

```powershell
Get-AzureRmVM `
    -ResourceGroupName myResourceGroup `
    -Name myVM `
    -Status | Select @{n="Status"; e={$_.Statuses[1].Code}}
```

<span data-ttu-id="973fc-234">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="973fc-234">Output:</span></span>

```powershell
Status
------
PowerState/running
```

## <a name="management-tasks"></a><span data-ttu-id="973fc-235">Задачи управления</span><span class="sxs-lookup"><span data-stu-id="973fc-235">Management tasks</span></span>

<span data-ttu-id="973fc-236">Во время жизненного цикла hello виртуальной машины может понадобиться toorun задачи управления, такие как запуск, остановка или удаление виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="973fc-236">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="973fc-237">Кроме того вы можете toocreate сценариев tooautomate повторяющихся или сложных задач.</span><span class="sxs-lookup"><span data-stu-id="973fc-237">Additionally, you may want toocreate scripts tooautomate repetitive or complex tasks.</span></span> <span data-ttu-id="973fc-238">С помощью Azure PowerShell, многие часто встречающиеся задачи управления можно запускать из командной строки hello, или в скриптах.</span><span class="sxs-lookup"><span data-stu-id="973fc-238">Using Azure PowerShell, many common management tasks can be run from hello command line or in scripts.</span></span>

### <a name="stop-virtual-machine"></a><span data-ttu-id="973fc-239">Прекращение работы виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="973fc-239">Stop virtual machine</span></span>

<span data-ttu-id="973fc-240">Остановите и освободите виртуальную машину с помощью командлета [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="973fc-240">Stop and deallocate a virtual machine with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm):</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
```

<span data-ttu-id="973fc-241">Tookeep hello виртуальной машины в подготовленное состояние, используйте параметр - StayProvisioned hello.</span><span class="sxs-lookup"><span data-stu-id="973fc-241">If you want tookeep hello virtual machine in a provisioned state, use hello -StayProvisioned parameter.</span></span>

### <a name="start-virtual-machine"></a><span data-ttu-id="973fc-242">Запуск виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="973fc-242">Start virtual machine</span></span>

```powershell
Start-AzureRmVM -ResourceGroupName myResourceGroupVM -Name myVM
```

### <a name="delete-resource-group"></a><span data-ttu-id="973fc-243">Удалить группу ресурсов</span><span class="sxs-lookup"><span data-stu-id="973fc-243">Delete resource group</span></span>

<span data-ttu-id="973fc-244">При удалении группы ресурсов будут также удалены все ресурсы, содержащиеся в ней.</span><span class="sxs-lookup"><span data-stu-id="973fc-244">Deleting a resource group also deletes all resources contained within.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroupVM -Force
```

## <a name="next-steps"></a><span data-ttu-id="973fc-245">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="973fc-245">Next steps</span></span>

<span data-ttu-id="973fc-246">В рамках этого руководства вы изучили основы создания виртуальной машины и управления ею. Вы узнали, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="973fc-246">In this tutorial, you learned about basic VM creation and management such as how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="973fc-247">Создать и присоединить tooa виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="973fc-247">Create and connect tooa VM</span></span>
> * <span data-ttu-id="973fc-248">Выбор и использование образов виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="973fc-248">Select and use VM images</span></span>
> * <span data-ttu-id="973fc-249">Просмотр и использование определенных размеров виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="973fc-249">View and use specific VM sizes</span></span>
> * <span data-ttu-id="973fc-250">Изменение размера виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="973fc-250">Resize a VM</span></span>
> * <span data-ttu-id="973fc-251">Просмотр виртуальной машины и оценка ее состояния</span><span class="sxs-lookup"><span data-stu-id="973fc-251">View and understand VM state</span></span>

<span data-ttu-id="973fc-252">Переместить следующий учебник toolearn toohello о дисках виртуальных Машин.</span><span class="sxs-lookup"><span data-stu-id="973fc-252">Advance toohello next tutorial toolearn about VM disks.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="973fc-253">Управление дисками Azure с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="973fc-253">Create and Manage VM disks</span></span>](./tutorial-manage-data-disk.md)
