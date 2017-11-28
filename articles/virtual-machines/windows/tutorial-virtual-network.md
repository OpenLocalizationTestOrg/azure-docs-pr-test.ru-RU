---
title: "Виртуальные сети и виртуальные машины Windows в Azure | Документы Майкрософт"
description: "Руководство по управлению виртуальными сетями Azure и виртуальными машинами Windows с помощью Azure PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: c71c07f8ecd123a7e27848ba5043d46e315fcf03
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="manage-azure-virtual-networks-and-windows-virtual-machines-with-azure-powershell"></a><span data-ttu-id="c63b6-103">Управление виртуальными сетями Azure и виртуальными машинами Windows с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c63b6-103">Manage Azure Virtual Networks and Windows Virtual Machines with Azure PowerShell</span></span>

<span data-ttu-id="c63b6-104">Виртуальные машины Azure осуществляют внутреннее и внешнее взаимодействие через сеть Azure.</span><span class="sxs-lookup"><span data-stu-id="c63b6-104">Azure virtual machines use Azure networking for internal and external network communication.</span></span> <span data-ttu-id="c63b6-105">Это руководство содержит сведения о создании нескольких виртуальных машин (ВМ) в виртуальной сети и настройках сетевого взаимодействия между ними.</span><span class="sxs-lookup"><span data-stu-id="c63b6-105">In this tutorial, you create multiple virtual machines (VMs) in a virtual network and configure network connectivity between them.</span></span> <span data-ttu-id="c63b6-106">Вы узнаете, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="c63b6-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c63b6-107">Создать виртуальную сеть</span><span class="sxs-lookup"><span data-stu-id="c63b6-107">Create a virtual network</span></span>
> * <span data-ttu-id="c63b6-108">Создание подсетей виртуальных сетей</span><span class="sxs-lookup"><span data-stu-id="c63b6-108">Create virtual network subnets</span></span>
> * <span data-ttu-id="c63b6-109">Управление сетевым трафиком с помощью групп безопасности сети</span><span class="sxs-lookup"><span data-stu-id="c63b6-109">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="c63b6-110">Просмотр правил трафика в действии</span><span class="sxs-lookup"><span data-stu-id="c63b6-110">View traffic rules in action</span></span>

<span data-ttu-id="c63b6-111">Для работы с этим руководством требуется модуль Azure PowerShell версии не ниже 3.6.</span><span class="sxs-lookup"><span data-stu-id="c63b6-111">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="c63b6-112">Чтобы узнать версию, выполните команду ` Get-Module -ListAvailable AzureRM`.</span><span class="sxs-lookup"><span data-stu-id="c63b6-112">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="c63b6-113">Если вам необходимо выполнить обновление, ознакомьтесь со статьей, посвященной [установке модуля Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="c63b6-113">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-vnet"></a><span data-ttu-id="c63b6-114">Создание виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="c63b6-114">Create VNet</span></span>

<span data-ttu-id="c63b6-115">Виртуальная сеть — это представление вашей собственной сети в облаке.</span><span class="sxs-lookup"><span data-stu-id="c63b6-115">A VNet is a representation of your own network in the cloud.</span></span> <span data-ttu-id="c63b6-116">Это логическая изоляция облака Azure, выделенного для вашей подписки.</span><span class="sxs-lookup"><span data-stu-id="c63b6-116">A VNet is a logical isolation of the Azure cloud dedicated to your subscription.</span></span> <span data-ttu-id="c63b6-117">В виртуальной сети находятся подсети, правила для их взаимодействия и подключения от виртуальных машин к подсетям.</span><span class="sxs-lookup"><span data-stu-id="c63b6-117">Within a VNet, you find subnets, rules for connectivity to those subnets, and connections from the VMs to the subnets.</span></span>

<span data-ttu-id="c63b6-118">Прежде чем создавать другие ресурсы Azure, нужно создать группу ресурсов с помощью командлета [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="c63b6-118">Before you can create any other Azure resources, you need to create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="c63b6-119">Следующий пример позволяет создать группу ресурсов *myRGNetwork* в расположении *EastUS*.</span><span class="sxs-lookup"><span data-stu-id="c63b6-119">The following example creates a resource group named *myRGNetwork* in the *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myRGNetwork -Location EastUS
```

<span data-ttu-id="c63b6-120">Подсеть является дочерним ресурсом виртуальной сети, который помогает определить сегменты адресных пространств в пределах блока CIDR на основе префиксов IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="c63b6-120">A subnet is a child resource of a VNet, and helps define segments of address spaces within a CIDR block, using IP address prefixes.</span></span> <span data-ttu-id="c63b6-121">Сетевые карты можно добавлять в подсети и подключать к виртуальным машинам, обеспечивая сетевые подключения для различных рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="c63b6-121">NICs can be added to subnets, and connected to VMs, providing connectivity for various workloads.</span></span>

<span data-ttu-id="c63b6-122">Создайте подсеть с помощью командлета [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="c63b6-122">Create a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
$frontendSubnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name myFrontendSubnet `
  -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="c63b6-123">Создайте виртуальную сеть *myVNet*, использующую *myFrontendSubnet*, выполнив командлет [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="c63b6-123">Create a VNET named *myVNet* using *myFrontendSubnet* with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myVNet `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $frontendSubnet
```

## <a name="create-front-end-vm"></a><span data-ttu-id="c63b6-124">Создание интерфейсной виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c63b6-124">Create front-end VM</span></span>

<span data-ttu-id="c63b6-125">Для взаимодействия в виртуальной сети виртуальной машине требуется виртуальная сетевая карта.</span><span class="sxs-lookup"><span data-stu-id="c63b6-125">For a VM to communicate in a VNet, it needs a virtual network interface (NIC).</span></span> <span data-ttu-id="c63b6-126">Доступ к *myFrontendVM* осуществляется через Интернет, поэтому также необходим общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="c63b6-126">The *myFrontendVM* is accessed from the internet, so it also needs a public IP address.</span></span> 

<span data-ttu-id="c63b6-127">Создайте общедоступный IP-адрес с помощью командлета [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span><span class="sxs-lookup"><span data-stu-id="c63b6-127">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

<span data-ttu-id="c63b6-128">Создайте сетевую карту с помощью командлета [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="c63b6-128">Create a NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span></span>


```powershell
$frontendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myFrontendNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

<span data-ttu-id="c63b6-129">Настройте на виртуальной машине имя пользователя и пароль для учетной записи администратора с помощью командлета [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="c63b6-129">Set the username and password needed for the administrator account on the VM with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="c63b6-130">Создайте виртуальные машины с помощью командлетов [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) и [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="c63b6-130">Create the VMs with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), and [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> 

```powershell
$frontendVM = New-AzureRmVMConfig `
    -VMName myFrontendVM `
    -VMSize Standard_D1
$frontendVM = Set-AzureRmVMOperatingSystem `
    -VM $frontendVM `
    -Windows `
    -ComputerName myFrontendVM `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
$frontendVM = Set-AzureRmVMSourceImage `
    -VM $frontendVM `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
$frontendVM = Set-AzureRmVMOSDisk `
    -VM $frontendVM `
    -Name myFrontendOSDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
$frontendVM = Add-AzureRmVMNetworkInterface `
    -VM $frontendVM `
    -Id $frontendNic.Id
New-AzureRmVM `
    -ResourceGroupName myRGNetwork `
    -Location EastUS `
    -VM $frontendVM
```

## <a name="install-web-server"></a><span data-ttu-id="c63b6-131">Установка веб-сервера</span><span class="sxs-lookup"><span data-stu-id="c63b6-131">Install web server</span></span>

<span data-ttu-id="c63b6-132">Установить службы IIS на *myFrontendVM* можно с помощью сеанса удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="c63b6-132">You can install IIS on *myFrontendVM* by using a remote desktop session.</span></span> <span data-ttu-id="c63b6-133">Вам нужно получить общедоступный IP-адрес виртуальной машины для доступа к ней.</span><span class="sxs-lookup"><span data-stu-id="c63b6-133">You need to get the public IP address of the VM to access it.</span></span>

<span data-ttu-id="c63b6-134">Получить общедоступный IP-адрес *myFrontendVM* можно с помощью командлета [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="c63b6-134">You can get the public IP address of *myFrontendVM* with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="c63b6-135">Следующий пример позволяет получить IP-адрес для созданного ранее *myPublicIPAddress*.</span><span class="sxs-lookup"><span data-stu-id="c63b6-135">The following example obtains the IP address for *myPublicIPAddress* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myRGNetwork `
    -Name myPublicIPAddress | select IpAddress
```

<span data-ttu-id="c63b6-136">Запишите этот IP-адрес, чтобы использовать его в последующих шагах.</span><span class="sxs-lookup"><span data-stu-id="c63b6-136">Take note of this IP Address so you can use it in future steps.</span></span>

<span data-ttu-id="c63b6-137">Используйте приведенную ниже команду для создания сеанса удаленного рабочего стола с *myFrontendVM*.</span><span class="sxs-lookup"><span data-stu-id="c63b6-137">Use the following command to create a remote desktop session with *myFrontendVM*.</span></span> <span data-ttu-id="c63b6-138">Замените *<publicIPAddress>* записанным ранее адресом.</span><span class="sxs-lookup"><span data-stu-id="c63b6-138">Replace *<publicIPAddress>* with the address that you previously recorded.</span></span> <span data-ttu-id="c63b6-139">При появлении запроса введите учетные данные, использованные при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c63b6-139">When prompted, enter the credentials used when you created the VM.</span></span>

```
mstsc /v:<publicIpAddress>
``` 

<span data-ttu-id="c63b6-140">После входа на *myFrontendVM* вы можете установить IIS и включить локальное правило брандмауэра, разрешающее веб-трафик, с помощью одной строки кода PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c63b6-140">Now that you have logged in to *myFrontendVM*, you can use a single line of PowerShell to install IIS and enable the local firewall rule to allow web traffic.</span></span> <span data-ttu-id="c63b6-141">Откройте командную строку PowerShell и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c63b6-141">Open a PowerShell prompt and run the following command:</span></span>

<span data-ttu-id="c63b6-142">Используйте командлет [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) для запуска расширения настраиваемых сценариев, которое устанавливает веб-сервер IIS:</span><span class="sxs-lookup"><span data-stu-id="c63b6-142">Use [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) to run the custom script extension that installs the IIS webserver:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

<span data-ttu-id="c63b6-143">Теперь вы можете использовать общедоступный IP-адрес для перехода к виртуальной машине и просмотра сайта IIS.</span><span class="sxs-lookup"><span data-stu-id="c63b6-143">Now you can use the public IP address to browse to the VM to see the IIS site.</span></span>

![Сайт IIS по умолчанию](./media/tutorial-virtual-network/iis.png)

## <a name="manage-internal-traffic"></a><span data-ttu-id="c63b6-145">Управление внутренним трафиком</span><span class="sxs-lookup"><span data-stu-id="c63b6-145">Manage internal traffic</span></span>

<span data-ttu-id="c63b6-146">Группа безопасности сети (NSG) содержит перечень правил безопасности, которые разрешают или запрещают передачу сетевого трафика к ресурсам, подключенным к виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c63b6-146">A network security group (NSG) contains a list of security rules that allow or deny network traffic to resources connected to a VNet.</span></span> <span data-ttu-id="c63b6-147">Группы безопасности сети можно сопоставить с подсетями или отдельными сетевыми картами, подключенными к виртуальным машинам.</span><span class="sxs-lookup"><span data-stu-id="c63b6-147">NSGs can be associated to subnets or individual NICs attached to VMs.</span></span> <span data-ttu-id="c63b6-148">Открытие или закрытие доступа к виртуальным машинам осуществляется с помощью правил NSG.</span><span class="sxs-lookup"><span data-stu-id="c63b6-148">Opening or closing access to VMs through ports is done using NSG rules.</span></span> <span data-ttu-id="c63b6-149">При создании *myFrontendVM* входящий порт 3389 автоматически был открыт для RDP-подключений.</span><span class="sxs-lookup"><span data-stu-id="c63b6-149">When you created *myFrontendVM*, inbound port 3389 was automatically opened for RDP connectivity.</span></span>

<span data-ttu-id="c63b6-150">С помощью группы безопасности сети можно настроить взаимодействие внутри виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="c63b6-150">Internal communication of VMs can be configured using an NSG.</span></span> <span data-ttu-id="c63b6-151">В этом разделе вы узнаете, как создать в сети дополнительную подсеть и назначить ей группу безопасности сети, чтобы разрешить подключение из *myFrontendVM* к *myBackendVM* через порт 1433.</span><span class="sxs-lookup"><span data-stu-id="c63b6-151">In this section, you learn how to create an additional subnet in the network and assign an NSG to it to allow a connection from *myFrontendVM* to *myBackendVM* on port 1433.</span></span> <span data-ttu-id="c63b6-152">После этого подсеть назначается виртуальной машине при ее создании.</span><span class="sxs-lookup"><span data-stu-id="c63b6-152">The subnet is then assigned to the VM when it is created.</span></span>

<span data-ttu-id="c63b6-153">Можно ограничить внутренний трафик для *myBackendVM* и разрешить только трафик из *myFrontendVM*, создав NSG для внутренней подсети.</span><span class="sxs-lookup"><span data-stu-id="c63b6-153">You can limit internal traffic to *myBackendVM* from only *myFrontendVM* by creating an NSG for the back-end subnet.</span></span> <span data-ttu-id="c63b6-154">Следующий пример создает правило NSG *myBackendNSGRule* с помощью командлета [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="c63b6-154">The following example creates an NSG rule named *myBackendNSGRule* with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):</span></span>

```powershell
$nsgBackendRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myBackendNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 100 `
  -SourceAddressPrefix 10.0.0.0/24 `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 1433 `
  -Access Allow
```

<span data-ttu-id="c63b6-155">Добавьте группу безопасности сети *myBackendNSG* с помощью командлета [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span><span class="sxs-lookup"><span data-stu-id="c63b6-155">Add a network security group named *myBackendNSG* with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span></span>

```powershell
$nsgBackend = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNSG `
  -SecurityRules $nsgBackendRule
```
## <a name="add-back-end-subnet"></a><span data-ttu-id="c63b6-156">Добавление внутренней подсети</span><span class="sxs-lookup"><span data-stu-id="c63b6-156">Add back-end subnet</span></span>

<span data-ttu-id="c63b6-157">Добавьте *myBackEndSubnet* в *myVNet* с помощью командлета [Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="c63b6-157">Add *myBackEndSubnet* to *myVNet* with [Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Add-AzureRmVirtualNetworkSubnetConfig `
  -Name myBackendSubnet `
  -VirtualNetwork $vnet `
  -AddressPrefix 10.0.1.0/24 `
  -NetworkSecurityGroup $nsgBackend
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
$vnet = Get-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Name myVNet
```

## <a name="create-back-end-vm"></a><span data-ttu-id="c63b6-158">Создание внутренней виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c63b6-158">Create back-end VM</span></span>

<span data-ttu-id="c63b6-159">Внутреннюю виртуальную машину проще всего создать с помощью образа SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c63b6-159">The easiest way to create the back-end VM is by using a SQL Server image.</span></span> <span data-ttu-id="c63b6-160">В этом учебнике лишь создается виртуальная машина с сервером базы данных, и не приводятся сведения о доступе к базе данных.</span><span class="sxs-lookup"><span data-stu-id="c63b6-160">This tutorial only creates the VM with the database server, but doesn't provide information about accessing the database.</span></span>

<span data-ttu-id="c63b6-161">Создайте *myBackendNic*.</span><span class="sxs-lookup"><span data-stu-id="c63b6-161">Create *myBackendNic*:</span></span>

```powershell
$backendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNic `
  -SubnetId $vnet.Subnets[1].Id
```

<span data-ttu-id="c63b6-162">Настройте на виртуальной машине имя пользователя и пароль для учетной записи администратора с помощью командлета Get-Credential:</span><span class="sxs-lookup"><span data-stu-id="c63b6-162">Set the username and password needed for the administrator account on the VM with Get-Credential:</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="c63b6-163">Создайте *myBackendVM*.</span><span class="sxs-lookup"><span data-stu-id="c63b6-163">Create *myBackendVM*:</span></span>

```powershell
$backendVM = New-AzureRmVMConfig `
  -VMName myBackendVM `
  -VMSize Standard_D1
$backendVM = Set-AzureRmVMOperatingSystem `
  -VM $backendVM `
  -Windows `
  -ComputerName myBackendVM `
  -Credential $cred `
  -ProvisionVMAgent `
  -EnableAutoUpdate
$backendVM = Set-AzureRmVMSourceImage `
  -VM $backendVM `
  -PublisherName MicrosoftSQLServer `
  -Offer SQL2016SP1-WS2016 `
  -Skus Enterprise `
  -Version latest
$backendVM = Set-AzureRmVMOSDisk `
  -VM $backendVM `
  -Name myBackendOSDisk `
  -DiskSizeInGB 128 `
  -CreateOption FromImage `
  -Caching ReadWrite
$backendVM = Add-AzureRmVMNetworkInterface `
  -VM $backendVM `
  -Id $backendNic.Id
New-AzureRmVM `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -VM $backendVM
```

<span data-ttu-id="c63b6-164">В рассматриваемом образе система SQL Server установлена, однако в данном руководстве она не используется.</span><span class="sxs-lookup"><span data-stu-id="c63b6-164">The image that is used has SQL Server installed, but is not used in this tutorial.</span></span> <span data-ttu-id="c63b6-165">Она показывает, как можно настроить виртуальную машину для обработки веб-трафика, а также для обработки операций управления базой данных.</span><span class="sxs-lookup"><span data-stu-id="c63b6-165">It is included to show you how you can configure a VM to handle web traffic and a VM to handle database management.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c63b6-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c63b6-166">Next steps</span></span>

<span data-ttu-id="c63b6-167">В этом руководстве вы создали и защитили сети Azure с точки зрения виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="c63b6-167">In this tutorial, you created and secured Azure networks as related to virtual machines.</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="c63b6-168">Создать виртуальную сеть</span><span class="sxs-lookup"><span data-stu-id="c63b6-168">Create a virtual network</span></span>
> * <span data-ttu-id="c63b6-169">Создание подсетей виртуальных сетей</span><span class="sxs-lookup"><span data-stu-id="c63b6-169">Create virtual network subnets</span></span>
> * <span data-ttu-id="c63b6-170">Управление сетевым трафиком с помощью групп безопасности сети</span><span class="sxs-lookup"><span data-stu-id="c63b6-170">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="c63b6-171">Просмотр правил трафика в действии</span><span class="sxs-lookup"><span data-stu-id="c63b6-171">View traffic rules in action</span></span>

<span data-ttu-id="c63b6-172">Перейдите к следующему руководству, чтобы узнать о мониторинге защиты данных на виртуальных машинах с помощью службы архивации Azure.</span><span class="sxs-lookup"><span data-stu-id="c63b6-172">Advance to the next tutorial to learn about monitoring securing data on virtual machines using Azure backup.</span></span> <span data-ttu-id="c63b6-173">.</span><span class="sxs-lookup"><span data-stu-id="c63b6-173">.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c63b6-174">Архивация виртуальных машин Windows в Azure</span><span class="sxs-lookup"><span data-stu-id="c63b6-174">Back up Windows virtual machines in Azure</span></span>](./tutorial-backup-vms.md)
