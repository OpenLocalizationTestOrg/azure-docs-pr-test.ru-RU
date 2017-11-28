---
title: "aaaTutorial - построения приложение с высокой доступностью на виртуальных машинах Azure | Документы Microsoft"
description: "Узнайте, как toocreate приложении высокой доступности и безопасности через три виртуальные машины Windows с подсистемой балансировки нагрузки в Azure"
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
ms.date: 03/30/2017
ms.author: davidmu
ms.openlocfilehash: f9eff96be4f3999651c4108f0334e4eaa1a39c0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-load-balanced-highly-available-application-on-windows-virtual-machines-in-azure"></a><span data-ttu-id="16942-103">Создание в Azure высокодоступного приложения с балансировкой нагрузки, выполняемого на виртуальных машинах Windows</span><span class="sxs-lookup"><span data-stu-id="16942-103">Build a load balanced, highly available application on Windows virtual machines in Azure</span></span>

<span data-ttu-id="16942-104">В этом учебнике создается приложение с высокой доступностью, устойчивыми toomaintenance события.</span><span class="sxs-lookup"><span data-stu-id="16942-104">In this tutorial, you create a highly available application that is resilient toomaintenance events.</span></span> <span data-ttu-id="16942-105">приложение Hello использует подсистему балансировки нагрузки, доступности и три виртуальных машинах (ВМ).</span><span class="sxs-lookup"><span data-stu-id="16942-105">hello app uses a load balancer, an availability set, and three Windows virtual machines (VMs).</span></span> <span data-ttu-id="16942-106">Этот учебник Установка служб IIS, на то, что можно использовать этот учебник toodeploy framework другого приложения с помощью hello же компонентов высокого уровня доступности и рекомендации.</span><span class="sxs-lookup"><span data-stu-id="16942-106">This tutorial installs IIS, though you can use this tutorial toodeploy a different application framework using hello same high availability components and guidelines.</span></span> 

## <a name="step-1---azure-prerequisites"></a><span data-ttu-id="16942-107">Шаг 1. Предварительные требования Azure</span><span class="sxs-lookup"><span data-stu-id="16942-107">Step 1 - Azure prerequisites</span></span>

<span data-ttu-id="16942-108">toocomplete этого учебника, убедитесь, что hello установлена последняя версия [Azure PowerShell](/powershell/azure/overview) модуля.</span><span class="sxs-lookup"><span data-stu-id="16942-108">toocomplete this tutorial, make sure that you have installed hello latest [Azure PowerShell](/powershell/azure/overview) module.</span></span>

<span data-ttu-id="16942-109">Во-первых войдите в tooyour подписки Azure с hello команда AzureRmAccount входа в систему и выполните hello на экране инструкциям.</span><span class="sxs-lookup"><span data-stu-id="16942-109">First, log in tooyour Azure subscription with hello Login-AzureRmAccount command and follow hello on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="16942-110">Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="16942-110">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="16942-111">Перед созданием другие ресурсы Azure, необходимо toocreate группу ресурсов с [New AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="16942-111">Before you can create any other Azure resources, you need toocreate a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="16942-112">Hello следующий пример создает группу ресурсов с именем `myResourceGroup` в hello `westeurope` области:</span><span class="sxs-lookup"><span data-stu-id="16942-112">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` region:</span></span> 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroup -Location westeurope
```

## <a name="step-2---create-availability-set"></a><span data-ttu-id="16942-113">Шаг 2. Создание группы доступности</span><span class="sxs-lookup"><span data-stu-id="16942-113">Step 2 - Create availability set</span></span>

<span data-ttu-id="16942-114">Виртуальные машины можно создать в логических доменах сбоя и обновления.</span><span class="sxs-lookup"><span data-stu-id="16942-114">Virtual machines can be created across logical fault and update domains.</span></span> <span data-ttu-id="16942-115">Каждый логический домен представляет часть оборудования в hello основной центр обработки данных Azure.</span><span class="sxs-lookup"><span data-stu-id="16942-115">Each logical domain represents a portion of hardware in hello underlying Azure datacenter.</span></span> <span data-ttu-id="16942-116">При создании двух и более виртуальных машин вычислительные ресурсы и ресурсы хранения распределяются по этим доменам.</span><span class="sxs-lookup"><span data-stu-id="16942-116">When you create two or more VMs, your compute and storage resources are distributed across these domains.</span></span> <span data-ttu-id="16942-117">Это распределение позволяет сохранить доступность hello приложения, если это аппаратный компонент должен обслуживания.</span><span class="sxs-lookup"><span data-stu-id="16942-117">This distribution maintains hello availability of your app if a hardware component needs maintenance.</span></span> <span data-ttu-id="16942-118">Группы доступности позволяют определить эти логические домены сбоя и обновления.</span><span class="sxs-lookup"><span data-stu-id="16942-118">Availability sets let you define these logical fault and update domains.</span></span>

<span data-ttu-id="16942-119">Создайте группу доступности с помощью командлета [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="16942-119">Create an availability set with [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="16942-120">Hello следующий пример создает именованный набор доступности `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="16942-120">hello following example creates an availability set named `myAvailabilitySet`:</span></span>

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroup `
  -Name myAvailabilitySet `
  -Location westeurope `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

## <a name="step-3---create-load-balancer"></a><span data-ttu-id="16942-121">Шаг 3. Создание балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="16942-121">Step 3 - Create load balancer</span></span>

<span data-ttu-id="16942-122">Приложение Azure Load Balancer распределяет трафик между набором определенных виртуальных машин с помощью правил балансировщика нагрузки.</span><span class="sxs-lookup"><span data-stu-id="16942-122">An Azure load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="16942-123">Зонда работоспособности наблюдает за данный порт на каждой виртуальной Машине и только распределяет трафик tooan оперативной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="16942-123">A health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span>

### <a name="create-public-ip-address"></a><span data-ttu-id="16942-124">Создание общедоступного IP-адреса</span><span class="sxs-lookup"><span data-stu-id="16942-124">Create public IP address</span></span>

<span data-ttu-id="16942-125">tooaccess приложения в Интернет, hello назначить балансировщик нагрузки toohello открытый IP адрес.</span><span class="sxs-lookup"><span data-stu-id="16942-125">tooaccess your app on hello Internet, assign a public IP address toohello load balancer.</span></span> <span data-ttu-id="16942-126">Создайте общедоступный IP-адрес с помощью командлета [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="16942-126">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="16942-127">Hello следующий пример создает общедоступный IP-адрес с именем `myPublicIP`:</span><span class="sxs-lookup"><span data-stu-id="16942-127">hello following example creates a public IP address named `myPublicIP`:</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-load-balancer"></a><span data-ttu-id="16942-128">Создание подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="16942-128">Create load balancer</span></span>

<span data-ttu-id="16942-129">Создайте интерфейсный IP-адрес с помощью командлета [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="16942-129">Create a frontend IP address with [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span></span> <span data-ttu-id="16942-130">Hello следующий пример создает интерфейсный IP-адрес с именем `myFrontEndPool`:</span><span class="sxs-lookup"><span data-stu-id="16942-130">hello following example creates a frontend IP address named `myFrontEndPool`:</span></span> 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name myFrontEndPool -PublicIpAddress $pip
```

<span data-ttu-id="16942-131">Создайте внутренний пул адресов с помощью командлета [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span><span class="sxs-lookup"><span data-stu-id="16942-131">Create a backend address pool with [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span></span> <span data-ttu-id="16942-132">Hello следующий пример создает пул адресов серверной части с именем `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="16942-132">hello following example creates a backend address pool named `myBackEndPool`:</span></span>

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

<span data-ttu-id="16942-133">Теперь создадим hello подсистемы балансировки нагрузки с [New AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span><span class="sxs-lookup"><span data-stu-id="16942-133">Now, create hello load balancer with [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span></span> <span data-ttu-id="16942-134">Hello следующий пример создает подсистемы балансировки нагрузки с именем `myLoadBalancer` с помощью hello `myPublicIP` адрес:</span><span class="sxs-lookup"><span data-stu-id="16942-134">hello following example creates a load balancer named `myLoadBalancer` using hello `myPublicIP` address:</span></span>

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroup `
  -Name myLoadBalancer `
  -Location westeurope `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-health-probe"></a><span data-ttu-id="16942-135">Создание пробы работоспособности</span><span class="sxs-lookup"><span data-stu-id="16942-135">Create health probe</span></span>

<span data-ttu-id="16942-136">tooallow hello балансировки toomonitor hello состояние загрузки приложения, используйте проверки работоспособности.</span><span class="sxs-lookup"><span data-stu-id="16942-136">tooallow hello load balancer toomonitor hello status of your app, you use a health probe.</span></span> <span data-ttu-id="16942-137">Проверка работоспособности Hello динамически добавляет или удаляет виртуальные машины из ротации подсистемы балансировки нагрузки hello, в зависимости от их проверки toohealth ответа.</span><span class="sxs-lookup"><span data-stu-id="16942-137">hello health probe dynamically adds or removes VMs from hello load balancer rotation based on their response toohealth checks.</span></span> <span data-ttu-id="16942-138">По умолчанию виртуальная машина удаляется из распределения подсистемы балансировки нагрузки hello после двух последовательных сбоев каждые 15 секунд.</span><span class="sxs-lookup"><span data-stu-id="16942-138">By default, a VM is removed from hello load balancer distribution after two consecutive failures at 15-second intervals.</span></span>

<span data-ttu-id="16942-139">Создайте пробу работоспособности с помощью командлета [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span><span class="sxs-lookup"><span data-stu-id="16942-139">Create a health probe with [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span></span> <span data-ttu-id="16942-140">Hello следующий пример создает зонда работоспособности с именем `myHealthProbe` , отслеживает каждой виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="16942-140">hello following example creates a health probe named `myHealthProbe` that monitors each VM:</span></span>

```powershell
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

### <a name="create-load-balancer-rule"></a><span data-ttu-id="16942-141">Создание правила подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="16942-141">Create load balancer rule</span></span>

<span data-ttu-id="16942-142">Правило подсистемы балансировки нагрузки — toodefine используется как трафика является распределенной toohello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="16942-142">A load balancer rule is used toodefine how traffic is distributed toohello VMs.</span></span>

<span data-ttu-id="16942-143">Создайте правило балансировщика нагрузки с помощью командлета [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span><span class="sxs-lookup"><span data-stu-id="16942-143">Create a load balancer rule with [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span></span> <span data-ttu-id="16942-144">Hello следующий пример создает правила подсистемы балансировки нагрузки с именем `myLoadBalancerRule` и распределяет трафик через порт `80`:</span><span class="sxs-lookup"><span data-stu-id="16942-144">hello following example creates a load balancer rule named `myLoadBalancerRule` and balances traffic on port `80`:</span></span>

```powershell
Add-AzureRmLoadBalancerRuleConfig -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80
```

<span data-ttu-id="16942-145">Обновление подсистемы балансировки нагрузки hello с [AzureRmLoadBalancer набор](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="16942-145">Update hello load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="step-4---configure-networking"></a><span data-ttu-id="16942-146">Шаг 4. Настройка сети</span><span class="sxs-lookup"><span data-stu-id="16942-146">Step 4 - Configure networking</span></span>

<span data-ttu-id="16942-147">Каждая Виртуальная машина имеет один или несколько виртуальных сетевых плат (NIC), подключить виртуальную сеть tooa.</span><span class="sxs-lookup"><span data-stu-id="16942-147">Each VM has one or more virtual network interface cards (NICs) that connect tooa virtual network.</span></span> <span data-ttu-id="16942-148">Эта виртуальная сеть обеспечивается toofilter трафика в зависимости от определенных правил доступа.</span><span class="sxs-lookup"><span data-stu-id="16942-148">This virtual network is secured toofilter traffic based on defined access rules.</span></span>

### <a name="create-virtual-network"></a><span data-ttu-id="16942-149">Создание виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="16942-149">Create virtual network</span></span>

<span data-ttu-id="16942-150">Сначала настройте подсеть с помощью командлета [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="16942-150">First, configure a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="16942-151">Hello следующий пример создает подсеть с именем `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="16942-151">hello following example creates a subnet named `mySubnet`:</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="16942-152">tooyour подключения tooprovide сети виртуальных машин, создайте виртуальную сеть с [New AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="16942-152">tooprovide network connectivity tooyour VMs, create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="16942-153">Hello следующий пример создает виртуальную сеть с именем `myVnet` с `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="16942-153">hello following example creates a virtual network named `myVnet` with `mySubnet`:</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

### <a name="configure-network-security"></a><span data-ttu-id="16942-154">Настройка безопасности сети</span><span class="sxs-lookup"><span data-stu-id="16942-154">Configure network security</span></span>

<span data-ttu-id="16942-155">[Группа безопасности сети](../../virtual-network/virtual-networks-nsg.md) Azure управляет входящим и исходящим трафиком одной или нескольких виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="16942-155">An Azure [network security group](../../virtual-network/virtual-networks-nsg.md) (NSG) controls inbound and outbound traffic for one or many virtual machines.</span></span> <span data-ttu-id="16942-156">Правила группы безопасности сети разрешают или запрещают передачу сетевого трафика на определенный порт или диапазон портов.</span><span class="sxs-lookup"><span data-stu-id="16942-156">Network security group rules allow or deny network traffic on a specific port or port range.</span></span> <span data-ttu-id="16942-157">Эти правила также могут включать префикс адреса источника, чтобы на виртуальную машину передавался только трафик от определенного источника.</span><span class="sxs-lookup"><span data-stu-id="16942-157">These rules can also include a source address prefix so that only traffic originating at a predefined source can communicate with a virtual machine.</span></span>

<span data-ttu-id="16942-158">tooallow веб-трафика tooreach приложения, создайте правило группы безопасности сети с [New AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="16942-158">tooallow web traffic tooreach your app, create a network security group rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="16942-159">Hello следующий пример создает правило группы сетевой безопасности с именем `myNetworkSecurityGroupRule`:</span><span class="sxs-lookup"><span data-stu-id="16942-159">hello following example creates a network security group rule named `myNetworkSecurityGroupRule`:</span></span>

```powershell
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNetworkSecurityGroupRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1001 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 80 `
  -Access Allow
```

<span data-ttu-id="16942-160">Создайте группу безопасности сети с помощью командлета [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span><span class="sxs-lookup"><span data-stu-id="16942-160">Create a network security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span></span> <span data-ttu-id="16942-161">Hello следующий пример создает NSG с именем `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="16942-161">hello following example creates an NSG named `myNetworkSecurityGroup`:</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule
```

<span data-ttu-id="16942-162">Добавить подсеть toohello группы безопасности сети hello с [AzureRmVirtualNetworkSubnetConfig набор](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="16942-162">Add hello network security group toohello subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="16942-163">Обновление hello виртуальную сеть с [AzureRmVirtualNetwork набор](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="16942-163">Update hello virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-network-interface-cards"></a><span data-ttu-id="16942-164">Создание виртуальных сетевых адаптеров</span><span class="sxs-lookup"><span data-stu-id="16942-164">Create virtual network interface cards</span></span>

<span data-ttu-id="16942-165">Загрузить функцию балансировки нагрузки с hello виртуальных Сетевых ресурсов, а не hello фактических виртуальных Машин.</span><span class="sxs-lookup"><span data-stu-id="16942-165">Load balancers function with hello virtual NIC resource rather than hello actual VM.</span></span> <span data-ttu-id="16942-166">Hello виртуальный сетевой Адаптер подключенных toohello Подсистема балансировки нагрузки и затем прикрепляется tooa виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="16942-166">hello virtual NIC is connected toohello load balancer, and then attached tooa VM.</span></span>

<span data-ttu-id="16942-167">Создайте виртуальную сетевую карту с помощью командлета [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="16942-167">Create a virtual NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="16942-168">Hello следующий пример создает три виртуальных сетевых адаптеров.</span><span class="sxs-lookup"><span data-stu-id="16942-168">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="16942-169">(Один виртуальный сетевой Адаптер для каждой виртуальной Машины, создать приложение hello следующих шагов):</span><span class="sxs-lookup"><span data-stu-id="16942-169">(One virtual NIC for each VM you create for your app in hello following steps):</span></span>


```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface -ResourceGroupName myResourceGroup `
     -Name myNic$i `
     -Location westeurope `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}

```

## <a name="step-5---create-virtual-machines"></a><span data-ttu-id="16942-170">Шаг 5. Создание виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="16942-170">Step 5 - Create virtual machines</span></span>

<span data-ttu-id="16942-171">С базовым компоненты на месте всех hello теперь можно создать высокодоступные виртуальные машины toorun приложения.</span><span class="sxs-lookup"><span data-stu-id="16942-171">With all hello underlying components in place, you can now create highly available VMs toorun your app.</span></span> 

<span data-ttu-id="16942-172">Получить hello имя пользователя и пароль для учетной записи администратора hello на виртуальной машине hello [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="16942-172">Get hello username and password needed for hello administrator account on hello virtual machine with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="16942-173">Создание виртуальных машин hello с [New AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [набор AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [AzureRmVMSourceImage набор](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [Добавить AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface), и [новый AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="16942-173">Create hello VMs with [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface), and [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="16942-174">Следующий пример Hello создает три виртуальные машины:</span><span class="sxs-lookup"><span data-stu-id="16942-174">hello following example creates three VMs:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   $vm = New-AzureRmVMConfig -VMName myVM$i -VMSize Standard_D1 -AvailabilitySetId $availabilitySet.Id
   $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName myVM$i -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
   $vm = Set-AzureRmVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2016-Datacenter -Version latest
   $vm = Set-AzureRmVMOSDisk -VM $vm -Name myOsDisk$i -StorageAccountType StandardLRS -DiskSizeInGB 128 -CreateOption FromImage -Caching ReadWrite
   $nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic$i
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM -ResourceGroupName myResourceGroup -Location westeurope -VM $vm
}

```

<span data-ttu-id="16942-175">Он занимает несколько минут toocreate и настроить все три виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="16942-175">It takes several minutes toocreate and configure all three VMs.</span></span> <span data-ttu-id="16942-176">Hello зонда работоспособности подсистемы балансировки нагрузки автоматически определяет, когда приложение hello выполняется на каждой виртуальной Машине.</span><span class="sxs-lookup"><span data-stu-id="16942-176">hello load balancer health probe automatically detects when hello app is running on each VM.</span></span> <span data-ttu-id="16942-177">После запуска приложение hello правило подсистемы балансировки нагрузки hello запускает toodistribute трафика.</span><span class="sxs-lookup"><span data-stu-id="16942-177">Once hello app is running, hello load balancer rule starts toodistribute traffic.</span></span>

### <a name="install-hello-app"></a><span data-ttu-id="16942-178">Установите приложение hello</span><span class="sxs-lookup"><span data-stu-id="16942-178">Install hello app</span></span> 

<span data-ttu-id="16942-179">Расширения виртуальных машин Azure, используемых tooautomate задачи настройки виртуальной машины, такие как установка приложений и настройка hello операционной системы.</span><span class="sxs-lookup"><span data-stu-id="16942-179">Azure virtual machine extensions are used tooautomate virtual machine configuration tasks such as installing applications and configuring hello operating system.</span></span> <span data-ttu-id="16942-180">Hello [расширение пользовательского скрипта для Windows](./../virtual-machines-windows-extensions-customscript.md) является используется toorun любой сценарий PowerShell на виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="16942-180">hello [custom script extension for Windows](./../virtual-machines-windows-extensions-customscript.md) is used toorun any PowerShell script on hello virtual machine.</span></span> <span data-ttu-id="16942-181">сценарий Hello могут хранится в хранилище Azure, любой доступный конечной точкой HTTP, или внедрены в конфигурации расширения пользовательского скрипта hello.</span><span class="sxs-lookup"><span data-stu-id="16942-181">hello script can be stored in Azure storage, any accessible HTTP endpoint, or embedded in hello custom script extension configuration.</span></span> <span data-ttu-id="16942-182">При использовании hello расширение пользовательского скрипта, агент ВМ Azure hello управляет выполнением скрипта hello.</span><span class="sxs-lookup"><span data-stu-id="16942-182">When using hello custom script extension, hello Azure VM agent manages hello script execution.</span></span>

<span data-ttu-id="16942-183">Используйте [AzureRmVMExtension набор](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello настраиваемое расширение сценария.</span><span class="sxs-lookup"><span data-stu-id="16942-183">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello custom script extension.</span></span> <span data-ttu-id="16942-184">Здравствуйте, выполняется расширение `powershell Add-WindowsFeature Web-Server` веб-сервер IIS hello tooinstall:</span><span class="sxs-lookup"><span data-stu-id="16942-184">hello extension runs `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS webserver:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server"}' `
     -Location westeurope
}
```

### <a name="test-your-app"></a><span data-ttu-id="16942-185">Тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="16942-185">Test your app</span></span>

<span data-ttu-id="16942-186">Получить hello общедоступный IP-адрес балансировки нагрузки, с [Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="16942-186">Obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="16942-187">Hello следующий пример извлекает hello IP-адрес для `myPublicIP` созданную ранее:</span><span class="sxs-lookup"><span data-stu-id="16942-187">hello following example obtains hello IP address for `myPublicIP` created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroup -Name myPublicIP | select IpAddress
```

<span data-ttu-id="16942-188">Введите hello общедоступный IP-адрес в tooa веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="16942-188">Enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="16942-189">С помощью правила NSG hello в месте отображается веб-сайт IIS по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="16942-189">With hello NSG rule in place, hello default IIS website is displayed.</span></span> 

![Сайт IIS по умолчанию](media/load-balanced-iis-tutorial/iis.png)

## <a name="step-6--management-tasks"></a><span data-ttu-id="16942-191">Шаг 6. Задачи управления</span><span class="sxs-lookup"><span data-stu-id="16942-191">Step 6 – Management tasks</span></span>

<span data-ttu-id="16942-192">Может потребоваться tooperform обслуживания на hello приложения, таких как установка обновления ОС работающих виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="16942-192">You may need tooperform maintenance on hello VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="16942-193">toodeal с приложением tooyour большего объема трафика, может потребоваться tooadd дополнительных ВМ.</span><span class="sxs-lookup"><span data-stu-id="16942-193">toodeal with increased traffic tooyour app, you may need tooadd additional VMs.</span></span> <span data-ttu-id="16942-194">В этом разделе показано, как tooremove или добавить виртуальную Машину из балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="16942-194">This section shows you how tooremove or add a VM from hello load balancer.</span></span> 

### <a name="remove-a-vm-from-hello-load-balancer"></a><span data-ttu-id="16942-195">Удалите виртуальную Машину из балансировки нагрузки hello</span><span class="sxs-lookup"><span data-stu-id="16942-195">Remove a VM from hello load balancer</span></span>

<span data-ttu-id="16942-196">Удалите виртуальную Машину из пула адресов серверной части hello, сбросив свойство пулы Loadbalancerbackendaddresspool hello hello сетевой интерфейсной платы.</span><span class="sxs-lookup"><span data-stu-id="16942-196">Remove a VM from hello backend address pool by resetting hello LoadBalancerBackendAddressPools property of hello network interface card.</span></span>

<span data-ttu-id="16942-197">Получить hello сетевой адаптер с [Get AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="16942-197">Get hello network interface card with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface):</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic2
``` 

<span data-ttu-id="16942-198">Задайте для свойства пулы Loadbalancerbackendaddresspool hello hello сетевой интерфейсной платы слишком $null:</span><span class="sxs-lookup"><span data-stu-id="16942-198">Set hello LoadBalancerBackendAddressPools property of hello network interface card too$null:</span></span>

```powershell
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
```

<span data-ttu-id="16942-199">Обновление hello сетевой адаптер:</span><span class="sxs-lookup"><span data-stu-id="16942-199">Update hello network interface card:</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

### <a name="add-a-vm-toohello-load-balancer"></a><span data-ttu-id="16942-200">Добавляет подсистему балансировки нагрузки виртуальной Машины toohello</span><span class="sxs-lookup"><span data-stu-id="16942-200">Add a VM toohello load balancer</span></span>

<span data-ttu-id="16942-201">После обслуживания виртуальной Машины, или если требуется емкость tooexpand добавления hello сетевой Адаптер подсистемы балансировки нагрузки hello пула адресов серверной части toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="16942-201">After performing VM maintenance, or if you need tooexpand capacity, adding hello NIC of a VM toohello backend address pool of hello load balancer.</span></span>

<span data-ttu-id="16942-202">Получите hello балансировки нагрузки:</span><span class="sxs-lookup"><span data-stu-id="16942-202">Get hello load balancer:</span></span>

```powershell
$lb = Get-AzureRMLoadBalancer -ResourceGroupName myResourceGroup -Name myLoadBalancer 
```

<span data-ttu-id="16942-203">Добавление пула адресов серверной части hello hello подсистемы балансировки нагрузки toohello сетевой интерфейсной платы:</span><span class="sxs-lookup"><span data-stu-id="16942-203">Add hello backend address pool of hello load balancer toohello network interface card:</span></span>

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
```

<span data-ttu-id="16942-204">Обновление hello сетевой адаптер:</span><span class="sxs-lookup"><span data-stu-id="16942-204">Update hello network interface card:</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a><span data-ttu-id="16942-205">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="16942-205">Next Steps</span></span>

<span data-ttu-id="16942-206">[Примеры PowerShell для виртуальной машины Azure](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="16942-206">Samples – [Azure Virtual Machine PowerShell sample scripts](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
