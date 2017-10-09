---
title: "aaaAzure виртуальных сетей и виртуальных машин Windows | Документы Microsoft"
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
ms.openlocfilehash: ed77d9d5873e849fcb2aaf15e41899d7ad8c781a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-windows-virtual-machines-with-azure-powershell"></a><span data-ttu-id="e717e-103">Управление виртуальными сетями Azure и виртуальными машинами Windows с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e717e-103">Manage Azure Virtual Networks and Windows Virtual Machines with Azure PowerShell</span></span>

<span data-ttu-id="e717e-104">Виртуальные машины Azure осуществляют внутреннее и внешнее взаимодействие через сеть Azure.</span><span class="sxs-lookup"><span data-stu-id="e717e-104">Azure virtual machines use Azure networking for internal and external network communication.</span></span> <span data-ttu-id="e717e-105">Это руководство содержит сведения о создании нескольких виртуальных машин (ВМ) в виртуальной сети и настройках сетевого взаимодействия между ними.</span><span class="sxs-lookup"><span data-stu-id="e717e-105">In this tutorial, you create multiple virtual machines (VMs) in a virtual network and configure network connectivity between them.</span></span> <span data-ttu-id="e717e-106">Вы узнаете, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="e717e-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e717e-107">Создать виртуальную сеть</span><span class="sxs-lookup"><span data-stu-id="e717e-107">Create a virtual network</span></span>
> * <span data-ttu-id="e717e-108">Создание подсетей виртуальных сетей</span><span class="sxs-lookup"><span data-stu-id="e717e-108">Create virtual network subnets</span></span>
> * <span data-ttu-id="e717e-109">Управление сетевым трафиком с помощью групп безопасности сети</span><span class="sxs-lookup"><span data-stu-id="e717e-109">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="e717e-110">Просмотр правил трафика в действии</span><span class="sxs-lookup"><span data-stu-id="e717e-110">View traffic rules in action</span></span>

<span data-ttu-id="e717e-111">Этот учебник требует hello Azure PowerShell модуль версии 3.6 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="e717e-111">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="e717e-112">Запустите ` Get-Module -ListAvailable AzureRM` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="e717e-112">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="e717e-113">Получить tooupgrade [установите Azure PowerShell модуль](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="e717e-113">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-vnet"></a><span data-ttu-id="e717e-114">Создание виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="e717e-114">Create VNet</span></span>

<span data-ttu-id="e717e-115">Виртуальная сеть — это представление сети в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="e717e-115">A VNet is a representation of your own network in hello cloud.</span></span> <span data-ttu-id="e717e-116">Виртуальная сеть является логической изоляции hello подписки tooyour выделенное облако Azure.</span><span class="sxs-lookup"><span data-stu-id="e717e-116">A VNet is a logical isolation of hello Azure cloud dedicated tooyour subscription.</span></span> <span data-ttu-id="e717e-117">В виртуальной сети найти подсетей правила подсети toothose подключения и подключения из подсети toohello hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e717e-117">Within a VNet, you find subnets, rules for connectivity toothose subnets, and connections from hello VMs toohello subnets.</span></span>

<span data-ttu-id="e717e-118">Перед созданием другие ресурсы Azure, необходимо toocreate группу ресурсов с [New AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="e717e-118">Before you can create any other Azure resources, you need toocreate a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="e717e-119">Hello следующий пример создает группу ресурсов с именем *myRGNetwork* в hello *EastUS* расположение:</span><span class="sxs-lookup"><span data-stu-id="e717e-119">hello following example creates a resource group named *myRGNetwork* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myRGNetwork -Location EastUS
```

<span data-ttu-id="e717e-120">Подсеть является дочерним ресурсом виртуальной сети, который помогает определить сегменты адресных пространств в пределах блока CIDR на основе префиксов IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="e717e-120">A subnet is a child resource of a VNet, and helps define segments of address spaces within a CIDR block, using IP address prefixes.</span></span> <span data-ttu-id="e717e-121">Сетевые адаптеры могут добавляться toosubnets и подключенных tooVMs, предоставляя возможность подключения к для различных рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="e717e-121">NICs can be added toosubnets, and connected tooVMs, providing connectivity for various workloads.</span></span>

<span data-ttu-id="e717e-122">Создайте подсеть с помощью командлета [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="e717e-122">Create a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
$frontendSubnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name myFrontendSubnet `
  -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="e717e-123">Создайте виртуальную сеть *myVNet*, использующую *myFrontendSubnet*, выполнив командлет [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="e717e-123">Create a VNET named *myVNet* using *myFrontendSubnet* with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myVNet `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $frontendSubnet
```

## <a name="create-front-end-vm"></a><span data-ttu-id="e717e-124">Создание интерфейсной виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="e717e-124">Create front-end VM</span></span>

<span data-ttu-id="e717e-125">Для виртуальной Машины toocommunicate, в виртуальной сети он должен виртуального сетевого интерфейса (NIC).</span><span class="sxs-lookup"><span data-stu-id="e717e-125">For a VM toocommunicate in a VNet, it needs a virtual network interface (NIC).</span></span> <span data-ttu-id="e717e-126">Hello *myFrontendVM* осуществляется из hello Интернета, поэтому он также требуется общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="e717e-126">hello *myFrontendVM* is accessed from hello internet, so it also needs a public IP address.</span></span> 

<span data-ttu-id="e717e-127">Создайте общедоступный IP-адрес с помощью командлета [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span><span class="sxs-lookup"><span data-stu-id="e717e-127">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

<span data-ttu-id="e717e-128">Создайте сетевую карту с помощью командлета [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="e717e-128">Create a NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span></span>


```powershell
$frontendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myFrontendNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

<span data-ttu-id="e717e-129">Укажите имя пользователя hello и пароль для учетной записи администратора hello hello виртуальной Машины с [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="e717e-129">Set hello username and password needed for hello administrator account on hello VM with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="e717e-130">Создание виртуальных машин hello с [New AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [набор AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [AzureRmVMSourceImage набор](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [Добавить AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), и [новый AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="e717e-130">Create hello VMs with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), and [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> 

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

## <a name="install-web-server"></a><span data-ttu-id="e717e-131">Установка веб-сервера</span><span class="sxs-lookup"><span data-stu-id="e717e-131">Install web server</span></span>

<span data-ttu-id="e717e-132">Установить службы IIS на *myFrontendVM* можно с помощью сеанса удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="e717e-132">You can install IIS on *myFrontendVM* by using a remote desktop session.</span></span> <span data-ttu-id="e717e-133">Требуется tooget hello общедоступный IP-адрес виртуальной Машины tooaccess hello его.</span><span class="sxs-lookup"><span data-stu-id="e717e-133">You need tooget hello public IP address of hello VM tooaccess it.</span></span>

<span data-ttu-id="e717e-134">Можно получить hello общедоступный IP-адрес *myFrontendVM* с [Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="e717e-134">You can get hello public IP address of *myFrontendVM* with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="e717e-135">Hello следующий пример извлекает hello IP-адрес для *myPublicIPAddress* созданную ранее:</span><span class="sxs-lookup"><span data-stu-id="e717e-135">hello following example obtains hello IP address for *myPublicIPAddress* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myRGNetwork `
    -Name myPublicIPAddress | select IpAddress
```

<span data-ttu-id="e717e-136">Запишите этот IP-адрес, чтобы использовать его в последующих шагах.</span><span class="sxs-lookup"><span data-stu-id="e717e-136">Take note of this IP Address so you can use it in future steps.</span></span>

<span data-ttu-id="e717e-137">Используйте hello следующая команда toocreate сеанс удаленного рабочего стола с *myFrontendVM*.</span><span class="sxs-lookup"><span data-stu-id="e717e-137">Use hello following command toocreate a remote desktop session with *myFrontendVM*.</span></span> <span data-ttu-id="e717e-138">Замените  *<publicIPAddress>*  с адресом hello, ранее сохраненным.</span><span class="sxs-lookup"><span data-stu-id="e717e-138">Replace *<publicIPAddress>* with hello address that you previously recorded.</span></span> <span data-ttu-id="e717e-139">При появлении запроса введите hello учетные данные, используемые при создании hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="e717e-139">When prompted, enter hello credentials used when you created hello VM.</span></span>

```
mstsc /v:<publicIpAddress>
``` 

<span data-ttu-id="e717e-140">Теперь, когда был выполнен вход слишком*myFrontendVM*, можно использовать одну строку PowerShell tooinstall IIS и включить hello локальном брандмауэре правило tooallow веб-трафика.</span><span class="sxs-lookup"><span data-stu-id="e717e-140">Now that you have logged in too*myFrontendVM*, you can use a single line of PowerShell tooinstall IIS and enable hello local firewall rule tooallow web traffic.</span></span> <span data-ttu-id="e717e-141">Откройте командную строку PowerShell и выполните следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="e717e-141">Open a PowerShell prompt and run hello following command:</span></span>

<span data-ttu-id="e717e-142">Используйте [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) toorun hello настраиваемое расширение сценария, устанавливающий веб-сервер IIS hello:</span><span class="sxs-lookup"><span data-stu-id="e717e-142">Use [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) toorun hello custom script extension that installs hello IIS webserver:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

<span data-ttu-id="e717e-143">Теперь можно использовать hello открытый IP адрес toobrowse toohello ВМ toosee hello узла IIS.</span><span class="sxs-lookup"><span data-stu-id="e717e-143">Now you can use hello public IP address toobrowse toohello VM toosee hello IIS site.</span></span>

![Сайт IIS по умолчанию](./media/tutorial-virtual-network/iis.png)

## <a name="manage-internal-traffic"></a><span data-ttu-id="e717e-145">Управление внутренним трафиком</span><span class="sxs-lookup"><span data-stu-id="e717e-145">Manage internal traffic</span></span>

<span data-ttu-id="e717e-146">Группа безопасности сети (NSG) содержит список правил безопасности, которые разрешают или запрещают tooa tooresources подключен сетевой трафик виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="e717e-146">A network security group (NSG) contains a list of security rules that allow or deny network traffic tooresources connected tooa VNet.</span></span> <span data-ttu-id="e717e-147">Nsg может быть связан toosubnets или tooVMs присоединенного отдельные сетевые адаптеры.</span><span class="sxs-lookup"><span data-stu-id="e717e-147">NSGs can be associated toosubnets or individual NICs attached tooVMs.</span></span> <span data-ttu-id="e717e-148">Выполняется открытие или закрытие tooVMs доступа к портам с помощью правила NSG.</span><span class="sxs-lookup"><span data-stu-id="e717e-148">Opening or closing access tooVMs through ports is done using NSG rules.</span></span> <span data-ttu-id="e717e-149">При создании *myFrontendVM* входящий порт 3389 автоматически был открыт для RDP-подключений.</span><span class="sxs-lookup"><span data-stu-id="e717e-149">When you created *myFrontendVM*, inbound port 3389 was automatically opened for RDP connectivity.</span></span>

<span data-ttu-id="e717e-150">С помощью группы безопасности сети можно настроить взаимодействие внутри виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e717e-150">Internal communication of VMs can be configured using an NSG.</span></span> <span data-ttu-id="e717e-151">В этом разделе вы узнаете, как toocreate дополнительные подсети в hello сети и назначить соединение из NSG tooit tooallow *myFrontendVM* слишком*myBackendVM* через порт 1433.</span><span class="sxs-lookup"><span data-stu-id="e717e-151">In this section, you learn how toocreate an additional subnet in hello network and assign an NSG tooit tooallow a connection from *myFrontendVM* too*myBackendVM* on port 1433.</span></span> <span data-ttu-id="e717e-152">подсети Hello назначается toohello виртуальной Машины при ее создании.</span><span class="sxs-lookup"><span data-stu-id="e717e-152">hello subnet is then assigned toohello VM when it is created.</span></span>

<span data-ttu-id="e717e-153">Можно ограничить внутренний трафик слишком*myBackendVM* только от *myFrontendVM* путем создания NSG для hello внутренней подсети.</span><span class="sxs-lookup"><span data-stu-id="e717e-153">You can limit internal traffic too*myBackendVM* from only *myFrontendVM* by creating an NSG for hello back-end subnet.</span></span> <span data-ttu-id="e717e-154">Hello следующий пример создает NSG правило с именем *myBackendNSGRule* с [New AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):</span><span class="sxs-lookup"><span data-stu-id="e717e-154">hello following example creates an NSG rule named *myBackendNSGRule* with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):</span></span>

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

<span data-ttu-id="e717e-155">Добавьте группу безопасности сети *myBackendNSG* с помощью командлета [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span><span class="sxs-lookup"><span data-stu-id="e717e-155">Add a network security group named *myBackendNSG* with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span></span>

```powershell
$nsgBackend = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNSG `
  -SecurityRules $nsgBackendRule
```
## <a name="add-back-end-subnet"></a><span data-ttu-id="e717e-156">Добавление внутренней подсети</span><span class="sxs-lookup"><span data-stu-id="e717e-156">Add back-end subnet</span></span>

<span data-ttu-id="e717e-157">Добавить *myBackEndSubnet* слишком*myVNet* с [AzureRmVirtualNetworkSubnetConfig добавить](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="e717e-157">Add *myBackEndSubnet* too*myVNet* with [Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):</span></span>

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

## <a name="create-back-end-vm"></a><span data-ttu-id="e717e-158">Создание внутренней виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="e717e-158">Create back-end VM</span></span>

<span data-ttu-id="e717e-159">Hello простым способом toocreate hello внутренней виртуальной Машины можно с помощью образа SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e717e-159">hello easiest way toocreate hello back-end VM is by using a SQL Server image.</span></span> <span data-ttu-id="e717e-160">Этот учебник только создает hello виртуальной Машины с сервером базы данных hello, но не предоставляет сведения о доступе к базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="e717e-160">This tutorial only creates hello VM with hello database server, but doesn't provide information about accessing hello database.</span></span>

<span data-ttu-id="e717e-161">Создайте *myBackendNic*.</span><span class="sxs-lookup"><span data-stu-id="e717e-161">Create *myBackendNic*:</span></span>

```powershell
$backendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNic `
  -SubnetId $vnet.Subnets[1].Id
```

<span data-ttu-id="e717e-162">Задайте hello имя пользователя и пароль для учетной записи администратора hello hello виртуальной Машины с помощью Get-Credential.</span><span class="sxs-lookup"><span data-stu-id="e717e-162">Set hello username and password needed for hello administrator account on hello VM with Get-Credential:</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="e717e-163">Создайте *myBackendVM*.</span><span class="sxs-lookup"><span data-stu-id="e717e-163">Create *myBackendVM*:</span></span>

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

<span data-ttu-id="e717e-164">Hello изображение, используемое установлен SQL Server, но не используется в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="e717e-164">hello image that is used has SQL Server installed, but is not used in this tutorial.</span></span> <span data-ttu-id="e717e-165">Это включается tooshow вы Настройка веб-трафик toohandle ВМ и управление виртуальными Машинами toohandle базы данных.</span><span class="sxs-lookup"><span data-stu-id="e717e-165">It is included tooshow you how you can configure a VM toohandle web traffic and a VM toohandle database management.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e717e-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e717e-166">Next steps</span></span>

<span data-ttu-id="e717e-167">В этом учебнике создается и защищенных сетей Azure как связанные toovirtual машины.</span><span class="sxs-lookup"><span data-stu-id="e717e-167">In this tutorial, you created and secured Azure networks as related toovirtual machines.</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="e717e-168">Создать виртуальную сеть</span><span class="sxs-lookup"><span data-stu-id="e717e-168">Create a virtual network</span></span>
> * <span data-ttu-id="e717e-169">Создание подсетей виртуальных сетей</span><span class="sxs-lookup"><span data-stu-id="e717e-169">Create virtual network subnets</span></span>
> * <span data-ttu-id="e717e-170">Управление сетевым трафиком с помощью групп безопасности сети</span><span class="sxs-lookup"><span data-stu-id="e717e-170">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="e717e-171">Просмотр правил трафика в действии</span><span class="sxs-lookup"><span data-stu-id="e717e-171">View traffic rules in action</span></span>

<span data-ttu-id="e717e-172">Переместить следующий учебник toolearn toohello о наблюдении за обеспечение безопасности данных на виртуальных машинах с помощью резервного копирования Azure.</span><span class="sxs-lookup"><span data-stu-id="e717e-172">Advance toohello next tutorial toolearn about monitoring securing data on virtual machines using Azure backup.</span></span> <span data-ttu-id="e717e-173">.</span><span class="sxs-lookup"><span data-stu-id="e717e-173">.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e717e-174">Архивация виртуальных машин Windows в Azure</span><span class="sxs-lookup"><span data-stu-id="e717e-174">Back up Windows virtual machines in Azure</span></span>](./tutorial-backup-vms.md)
