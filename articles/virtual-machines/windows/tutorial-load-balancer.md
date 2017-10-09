---
title: "aaaHow tooload распределения виртуальной машины Windows Azure | Документы Microsoft"
description: "Узнайте, как toouse hello Azure распределять балансировки toocreate высокой доступности и безопасного приложения в три виртуальные машины Windows"
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
ms.openlocfilehash: bfbd6a24e90a33e60d7d4f7b0c471af5d4e71f45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-windows-virtual-machines-in-azure-toocreate-a-highly-available-application"></a><span data-ttu-id="35208-103">Как tooload сбалансировать виртуальных машинах в Azure toocreate приложение с высокой доступностью</span><span class="sxs-lookup"><span data-stu-id="35208-103">How tooload balance Windows virtual machines in Azure toocreate a highly available application</span></span>
<span data-ttu-id="35208-104">Балансировка нагрузки обеспечивает более высокий уровень доступности за счет распределения входящих запросов между несколькими виртуальными машинами.</span><span class="sxs-lookup"><span data-stu-id="35208-104">Load balancing provides a higher level of availability by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="35208-105">В этом учебнике вы узнаете о hello различных компонентов подсистемы балансировки нагрузки Azure hello, распределения трафика и обеспечения высокого уровня доступности.</span><span class="sxs-lookup"><span data-stu-id="35208-105">In this tutorial, you learn about hello different components of hello Azure load balancer that distribute traffic and provide high availability.</span></span> <span data-ttu-id="35208-106">Вы узнаете, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="35208-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="35208-107">Создание Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="35208-107">Create an Azure load balancer</span></span>
> * <span data-ttu-id="35208-108">Создание пробы работоспособности балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="35208-108">Create a load balancer health probe</span></span>
> * <span data-ttu-id="35208-109">создавать правила трафика подсистемы балансировки нагрузки;</span><span class="sxs-lookup"><span data-stu-id="35208-109">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="35208-110">Использовать настраиваемое расширение скриптов hello toocreate простого узла IIS</span><span class="sxs-lookup"><span data-stu-id="35208-110">Use hello Custom Script Extension toocreate a basic IIS site</span></span>
> * <span data-ttu-id="35208-111">Создание виртуальных машин и присоединения tooa балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="35208-111">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="35208-112">Просмотр балансировщика нагрузки в действии</span><span class="sxs-lookup"><span data-stu-id="35208-112">View a load balancer in action</span></span>
> * <span data-ttu-id="35208-113">добавлять и удалять виртуальные машины из подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="35208-113">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="35208-114">Этот учебник требует hello Azure PowerShell модуль версии 3.6 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="35208-114">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="35208-115">Запустите ` Get-Module -ListAvailable AzureRM` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="35208-115">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="35208-116">Получить tooupgrade [установите Azure PowerShell модуль](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="35208-116">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="azure-load-balancer-overview"></a><span data-ttu-id="35208-117">Обзор Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="35208-117">Azure load balancer overview</span></span>
<span data-ttu-id="35208-118">Azure Load Balancer представляет собой балансировщик нагрузки уровня 4 (TCP, UDP), который обеспечивает высокий уровень доступности, распределяя входящий трафик между работоспособными виртуальными машинами.</span><span class="sxs-lookup"><span data-stu-id="35208-118">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="35208-119">Отслеживает данный порт на каждой виртуальной Машине зонда работоспособности подсистемы балансировки нагрузки и только распределяет трафик tooan оперативной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="35208-119">A load balancer health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span>

<span data-ttu-id="35208-120">Вы определяете интерфейсную конфигурацию IP-адресов, содержащую один или несколько общедоступных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="35208-120">You define a front-end IP configuration that contains one or more public IP addresses.</span></span> <span data-ttu-id="35208-121">Эту интерфейсный IP-конфигурацию позволяет вашей toobe нагрузки балансировки и приложения доступны через Интернет hello.</span><span class="sxs-lookup"><span data-stu-id="35208-121">This front-end IP configuration allows your load balancer and applications toobe accessible over hello Internet.</span></span> 

<span data-ttu-id="35208-122">Виртуальные машины подключены tooa подсистемы балансировки нагрузки с помощью их виртуальный сетевой адаптер (NIC).</span><span class="sxs-lookup"><span data-stu-id="35208-122">Virtual machines connect tooa load balancer using their virtual network interface card (NIC).</span></span> <span data-ttu-id="35208-123">toodistribute toohello трафика виртуальных машин, пул адресов серверной части содержит IP-адреса hello hello виртуальный (NIC) подключенных toohello подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="35208-123">toodistribute traffic toohello VMs, a back-end address pool contains hello IP addresses of hello virtual (NICs) connected toohello load balancer.</span></span>

<span data-ttu-id="35208-124">toocontrol hello потока трафика, определить правила подсистемы балансировки нагрузки для определенных портов и протоколов, сопоставить виртуальные машины tooyour.</span><span class="sxs-lookup"><span data-stu-id="35208-124">toocontrol hello flow of traffic, you define load balancer rules for specific ports and protocols that map tooyour VMs.</span></span>


## <a name="create-azure-load-balancer"></a><span data-ttu-id="35208-125">Создание Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="35208-125">Create Azure load balancer</span></span>
<span data-ttu-id="35208-126">В этом разделе описаны создание и настройка каждого компонента балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="35208-126">This section details how you can create and configure each component of hello load balancer.</span></span> <span data-ttu-id="35208-127">Прежде чем создать балансировщик нагрузки, выполните команду [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) для создания группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="35208-127">Before you can create your load balancer, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="35208-128">Hello следующий пример создает группу ресурсов с именем *myResourceGroupLoadBalancer* в hello *EastUS* расположение:</span><span class="sxs-lookup"><span data-stu-id="35208-128">hello following example creates a resource group named *myResourceGroupLoadBalancer* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS
```

### <a name="create-a-public-ip-address"></a><span data-ttu-id="35208-129">Создание общедоступного IP-адреса</span><span class="sxs-lookup"><span data-stu-id="35208-129">Create a public IP address</span></span>
<span data-ttu-id="35208-130">tooaccess приложения на Здравствуйте Интернет, необходимые для балансировки нагрузки hello общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="35208-130">tooaccess your app on hello Internet, you need a public IP address for hello load balancer.</span></span> <span data-ttu-id="35208-131">Создайте общедоступный IP-адрес с помощью командлета [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="35208-131">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="35208-132">Hello следующий пример создает общедоступный IP-адрес с именем *myPublicIP* в hello *myResourceGroupLoadBalancer* группа ресурсов:</span><span class="sxs-lookup"><span data-stu-id="35208-132">hello following example creates a public IP address named *myPublicIP* in hello *myResourceGroupLoadBalancer* resource group:</span></span>

```powershell
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-a-load-balancer"></a><span data-ttu-id="35208-133">Создание балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="35208-133">Create a load balancer</span></span>
<span data-ttu-id="35208-134">Создайте интерфейсный IP-адрес с помощью командлета [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="35208-134">Create a frontend IP address with [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span></span> <span data-ttu-id="35208-135">Hello следующий пример создает интерфейсный IP-адрес с именем *myFrontEndPool*:</span><span class="sxs-lookup"><span data-stu-id="35208-135">hello following example creates a frontend IP address named *myFrontEndPool*:</span></span> 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
```

<span data-ttu-id="35208-136">Создайте внутренний пул адресов с помощью командлета [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span><span class="sxs-lookup"><span data-stu-id="35208-136">Create a backend address pool with [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span></span> <span data-ttu-id="35208-137">Hello следующий пример создает пул адресов серверной части с именем *myBackEndPool*:</span><span class="sxs-lookup"><span data-stu-id="35208-137">hello following example creates a backend address pool named *myBackEndPool*:</span></span>

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

<span data-ttu-id="35208-138">Теперь создадим hello подсистемы балансировки нагрузки с [New AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span><span class="sxs-lookup"><span data-stu-id="35208-138">Now, create hello load balancer with [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span></span> <span data-ttu-id="35208-139">Hello следующий пример создает подсистемы балансировки нагрузки с именем *myLoadBalancer* с помощью hello *myPublicIP* адрес:</span><span class="sxs-lookup"><span data-stu-id="35208-139">hello following example creates a load balancer named *myLoadBalancer* using hello *myPublicIP* address:</span></span>

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-a-health-probe"></a><span data-ttu-id="35208-140">Создание пробы работоспособности</span><span class="sxs-lookup"><span data-stu-id="35208-140">Create a health probe</span></span>
<span data-ttu-id="35208-141">tooallow hello балансировки toomonitor hello состояние загрузки приложения, используйте проверки работоспособности.</span><span class="sxs-lookup"><span data-stu-id="35208-141">tooallow hello load balancer toomonitor hello status of your app, you use a health probe.</span></span> <span data-ttu-id="35208-142">Проверка работоспособности Hello динамически добавляет или удаляет виртуальные машины из ротации подсистемы балансировки нагрузки hello, в зависимости от их проверки toohealth ответа.</span><span class="sxs-lookup"><span data-stu-id="35208-142">hello health probe dynamically adds or removes VMs from hello load balancer rotation based on their response toohealth checks.</span></span> <span data-ttu-id="35208-143">По умолчанию виртуальная машина удаляется из распределения подсистемы балансировки нагрузки hello после двух последовательных сбоев каждые 15 секунд.</span><span class="sxs-lookup"><span data-stu-id="35208-143">By default, a VM is removed from hello load balancer distribution after two consecutive failures at 15-second intervals.</span></span> <span data-ttu-id="35208-144">Пробу работоспособности можно создать на основе протокола или конкретной страницы проверки работоспособности приложения.</span><span class="sxs-lookup"><span data-stu-id="35208-144">You create a health probe based on a protocol or a specific health check page for your app.</span></span> 

<span data-ttu-id="35208-145">Следующий пример Hello создает TCP-зонды.</span><span class="sxs-lookup"><span data-stu-id="35208-145">hello following example creates a TCP probe.</span></span> <span data-ttu-id="35208-146">Вы также можете создать настраиваемую пробу HTTP для более детальных проверок.</span><span class="sxs-lookup"><span data-stu-id="35208-146">You can also create custom HTTP probes for more fine grained health checks.</span></span> <span data-ttu-id="35208-147">При использовании пользовательских проверку HTTP, необходимо создать страницу проверки работоспособности hello, таких как *healthcheck.aspx*.</span><span class="sxs-lookup"><span data-stu-id="35208-147">When using a custom HTTP probe, you must create hello health check page, such as *healthcheck.aspx*.</span></span> <span data-ttu-id="35208-148">Hello пробы должен возвращать **HTTP 200 OK** ответа для узла hello tookeep подсистемы балансировки нагрузки hello в поворота.</span><span class="sxs-lookup"><span data-stu-id="35208-148">hello probe must return an **HTTP 200 OK** response for hello load balancer tookeep hello host in rotation.</span></span>

<span data-ttu-id="35208-149">использовать toocreate TCP-зонды работоспособности [AzureRmLoadBalancerProbeConfig добавить](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span><span class="sxs-lookup"><span data-stu-id="35208-149">toocreate a TCP health probe, you use [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span></span> <span data-ttu-id="35208-150">Hello следующий пример создает зонда работоспособности с именем *myHealthProbe* , отслеживает каждой виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="35208-150">hello following example creates a health probe named *myHealthProbe* that monitors each VM:</span></span>

```powershell
Add-AzureRmLoadBalancerProbeConfig `
  -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

<span data-ttu-id="35208-151">Обновление подсистемы балансировки нагрузки hello с [AzureRmLoadBalancer набор](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="35208-151">Update hello load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="35208-152">Создание правила балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="35208-152">Create a load balancer rule</span></span>
<span data-ttu-id="35208-153">Правило подсистемы балансировки нагрузки — toodefine используется как трафика является распределенной toohello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="35208-153">A load balancer rule is used toodefine how traffic is distributed toohello VMs.</span></span> <span data-ttu-id="35208-154">Можно определить hello интерфейсный IP-конфигурацию для hello входящий трафик и hello серверной части IP пула tooreceive hello трафика, а также требуемых исходных hello и порт назначения.</span><span class="sxs-lookup"><span data-stu-id="35208-154">You define hello front-end IP configuration for hello incoming traffic and hello back-end IP pool tooreceive hello traffic, along with hello required source and destination port.</span></span> <span data-ttu-id="35208-155">toomake убедиться, что только работоспособное ВМ получать трафик также определять toouse проверки работоспособности hello.</span><span class="sxs-lookup"><span data-stu-id="35208-155">toomake sure only healthy VMs receive traffic, you also define hello health probe toouse.</span></span>

<span data-ttu-id="35208-156">Создайте правило балансировщика нагрузки с помощью командлета [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span><span class="sxs-lookup"><span data-stu-id="35208-156">Create a load balancer rule with [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span></span> <span data-ttu-id="35208-157">Hello следующий пример создает правила подсистемы балансировки нагрузки с именем *myLoadBalancerRule* и распределяет трафик через порт *80*:</span><span class="sxs-lookup"><span data-stu-id="35208-157">hello following example creates a load balancer rule named *myLoadBalancerRule* and balances traffic on port *80*:</span></span>

```powershell
$probe = Get-AzureRmLoadBalancerProbeConfig -LoadBalancer $lb -Name myHealthProbe

Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80 `
  -Probe $probe
```

<span data-ttu-id="35208-158">Обновление подсистемы балансировки нагрузки hello с [AzureRmLoadBalancer набор](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="35208-158">Update hello load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```


## <a name="configure-virtual-network"></a><span data-ttu-id="35208-159">Настройка виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="35208-159">Configure virtual network</span></span>
<span data-ttu-id="35208-160">Перед развертыванием некоторые виртуальные машины и можно проверить балансировки, создайте hello, поддерживающие ресурсы виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="35208-160">Before you deploy some VMs and can test your balancer, create hello supporting virtual network resources.</span></span> <span data-ttu-id="35208-161">Дополнительные сведения о виртуальных сетях см. в разделе hello [управление виртуальными сетями Azure](tutorial-virtual-network.md) учебника.</span><span class="sxs-lookup"><span data-stu-id="35208-161">For more information about virtual networks, see hello [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="35208-162">Создание сетевых ресурсов</span><span class="sxs-lookup"><span data-stu-id="35208-162">Create network resources</span></span>
<span data-ttu-id="35208-163">Создайте виртуальную сеть с помощью командлета [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="35208-163">Create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="35208-164">Hello следующий пример создает виртуальную сеть с именем *myVnet* с *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="35208-164">hello following example creates a virtual network named *myVnet* with *mySubnet*:</span></span>

```powershell
# Create subnet config
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create hello virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

<span data-ttu-id="35208-165">Создайте правило группы безопасности сети с помощью командлета [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), а затем группу безопасности сети с помощью [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span><span class="sxs-lookup"><span data-stu-id="35208-165">Create a network security group rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), then create a network security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span></span> <span data-ttu-id="35208-166">Добавить подсеть toohello группы безопасности сети hello с [набор AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) и обновите hello виртуальную сеть с [AzureRmVirtualNetwork набор](/powershell/module/azurerm.network/set-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="35208-166">Add hello network security group toohello subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) and then update hello virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork).</span></span> 

<span data-ttu-id="35208-167">Hello следующий пример создает правило группы сетевой безопасности с именем *myNetworkSecurityGroup* и применяет его слишком*mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="35208-167">hello following example creates a network security group rule named *myNetworkSecurityGroup* and applies it too*mySubnet*:</span></span>

```powershell
# Create security rule config
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

# Create hello network security group
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule

# Apply hello network security group tooa subnet
Set-AzureRmVirtualNetworkSubnetConfig `
  -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24

# Update hello virtual network
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

<span data-ttu-id="35208-168">Для создания виртуальных сетевых карт используется командлет [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="35208-168">Virtual NICs are created with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="35208-169">Hello следующий пример создает три виртуальных сетевых адаптеров.</span><span class="sxs-lookup"><span data-stu-id="35208-169">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="35208-170">(Один виртуальный сетевой Адаптер для каждой виртуальной Машины, создать приложение hello следующих шагов).</span><span class="sxs-lookup"><span data-stu-id="35208-170">(One virtual NIC for each VM you create for your app in hello following steps).</span></span> <span data-ttu-id="35208-171">Можно создать в любое время дополнительных виртуальных сетевых адаптеров и виртуальные машины и добавить их toohello балансировки нагрузки:</span><span class="sxs-lookup"><span data-stu-id="35208-171">You can create additional virtual NICs and VMs at any time and add them toohello load balancer:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -Name myNic$i `
     -Location EastUS `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}
```

## <a name="create-virtual-machines"></a><span data-ttu-id="35208-172">Создание виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="35208-172">Create virtual machines</span></span>
<span data-ttu-id="35208-173">tooimprove hello высокий уровень доступности приложения, поместите виртуальные машины в группу доступности.</span><span class="sxs-lookup"><span data-stu-id="35208-173">tooimprove hello high availability of your app, place your VMs in an availability set.</span></span>

<span data-ttu-id="35208-174">Создайте группу доступности с помощью командлета [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="35208-174">Create an availability set with [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="35208-175">Hello следующий пример создает именованный набор доступности *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="35208-175">hello following example creates an availability set named *myAvailabilitySet*:</span></span>

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myAvailabilitySet `
  -Location EastUS `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

<span data-ttu-id="35208-176">Набор администратору имя пользователя и пароль для виртуальных машин hello с [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="35208-176">Set an administrator username and password for hello VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="35208-177">Теперь можно создавать виртуальные машины hello с [New AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="35208-177">Now you can create hello VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="35208-178">Следующий пример Hello создает три виртуальные машины:</span><span class="sxs-lookup"><span data-stu-id="35208-178">hello following example creates three VMs:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
  $vm = New-AzureRmVMConfig `
    -VMName myVM$i `
    -VMSize Standard_D1 `
    -AvailabilitySetId $availabilitySet.Id
  $vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM$i `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
  $vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
  $vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk$i `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
  $nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic$i
  $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
  New-AzureRmVM `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Location EastUS `
    -VM $vm
}
```

<span data-ttu-id="35208-179">Он занимает несколько минут toocreate и настроить все три виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="35208-179">It takes a few minutes toocreate and configure all three VMs.</span></span>

### <a name="install-iis-with-custom-script-extension"></a><span data-ttu-id="35208-180">Установка IIS с помощью расширения пользовательских сценариев</span><span class="sxs-lookup"><span data-stu-id="35208-180">Install IIS with Custom Script Extension</span></span>
<span data-ttu-id="35208-181">В предыдущем учебнике на [как toocustomize виртуальной машины Windows](tutorial-automate-vm-deployment.md), вы узнали, каким образом tooautomate настройки виртуальной Машины с hello пользовательский скрипт расширения для Windows.</span><span class="sxs-lookup"><span data-stu-id="35208-181">In a previous tutorial on [How toocustomize a Windows virtual machine](tutorial-automate-vm-deployment.md), you learned how tooautomate VM customization with hello Custom Script Extension for Windows.</span></span> <span data-ttu-id="35208-182">Можно использовать hello же подходов tooinstall и настройте службы IIS на виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="35208-182">You can use hello same approach tooinstall and configure IIS on your VMs.</span></span>

<span data-ttu-id="35208-183">Используйте [AzureRmVMExtension набор](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello настраиваемого расширения скриптов.</span><span class="sxs-lookup"><span data-stu-id="35208-183">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello Custom Script Extension.</span></span> <span data-ttu-id="35208-184">Здравствуйте, выполняется расширение `powershell Add-WindowsFeature Web-Server` tooinstall hello веб-сервере IIS, а затем обновления hello *Default.htm* страницы tooshow hello имя узла виртуальной Машины hello:</span><span class="sxs-lookup"><span data-stu-id="35208-184">hello extension runs `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS webserver and then updates hello *Default.htm* page tooshow hello hostname of hello VM:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
     -Location EastUS
}
```

## <a name="test-load-balancer"></a><span data-ttu-id="35208-185">Проверка балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="35208-185">Test load balancer</span></span>
<span data-ttu-id="35208-186">Получить hello общедоступный IP-адрес балансировки нагрузки, с [Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="35208-186">Obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="35208-187">Hello следующий пример извлекает hello IP-адрес для *myPublicIP* созданную ранее:</span><span class="sxs-lookup"><span data-stu-id="35208-187">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myPublicIP | select IpAddress
```

<span data-ttu-id="35208-188">После этого можно вводить hello общедоступный IP-адрес в tooa веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="35208-188">You can then enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="35208-189">отображается Hello веб-сайта, включая имя узла виртуальной Машины hello hello балансировки нагрузки, hello распределенных tooas трафика в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="35208-189">hello website is displayed, including hello hostname of hello VM that hello load balancer distributed traffic tooas in hello following example:</span></span>

![Выполнение веб-сайта IIS](./media/tutorial-load-balancer/running-iis-website.png)

<span data-ttu-id="35208-191">Подсистема балансировки нагрузки hello toosee распределять трафик между все три виртуальные машины, запускающий ваше приложение, вы может принудительно обновить веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="35208-191">toosee hello load balancer distribute traffic across all three VMs running your app, you can force-refresh your web browser.</span></span>


## <a name="add-and-remove-vms"></a><span data-ttu-id="35208-192">Добавление и удаление виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="35208-192">Add and remove VMs</span></span>
<span data-ttu-id="35208-193">Может потребоваться tooperform обслуживания на hello приложения, таких как установка обновления ОС работающих виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="35208-193">You may need tooperform maintenance on hello VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="35208-194">toodeal с приложением tooyour большего объема трафика, может потребоваться tooadd дополнительных ВМ.</span><span class="sxs-lookup"><span data-stu-id="35208-194">toodeal with increased traffic tooyour app, you may need tooadd additional VMs.</span></span> <span data-ttu-id="35208-195">В этом разделе показано, как tooremove или добавить виртуальную Машину из балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="35208-195">This section shows you how tooremove or add a VM from hello load balancer.</span></span>

### <a name="remove-a-vm-from-hello-load-balancer"></a><span data-ttu-id="35208-196">Удалите виртуальную Машину из балансировки нагрузки hello</span><span class="sxs-lookup"><span data-stu-id="35208-196">Remove a VM from hello load balancer</span></span>
<span data-ttu-id="35208-197">Получить hello сетевой адаптер с [Get AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), затем набор hello *пулы Loadbalancerbackendaddresspool* свойство hello виртуального сетевого Адаптера в слишком*$null*.</span><span class="sxs-lookup"><span data-stu-id="35208-197">Get hello network interface card with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), then set hello *LoadBalancerBackendAddressPools* property of hello virtual NIC too*$null*.</span></span> <span data-ttu-id="35208-198">Наконец обновите hello виртуального сетевого адаптера.:</span><span class="sxs-lookup"><span data-stu-id="35208-198">Finally, update hello virtual NIC.:</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic2
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="35208-199">подсистемы балансировки нагрузки hello toosee распределять трафик между hello остальные две виртуальные машины под управлением приложения вы можно принудительно обновить веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="35208-199">toosee hello load balancer distribute traffic across hello remaining two VMs running your app you can force-refresh your web browser.</span></span> <span data-ttu-id="35208-200">Теперь можно выполнить обслуживание на hello виртуальной Машины, таких как установка обновлений операционной системы или перезагрузки виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="35208-200">You can now perform maintenance on hello VM, such as installing OS updates or performing a VM reboot.</span></span>

### <a name="add-a-vm-toohello-load-balancer"></a><span data-ttu-id="35208-201">Добавляет подсистему балансировки нагрузки виртуальной Машины toohello</span><span class="sxs-lookup"><span data-stu-id="35208-201">Add a VM toohello load balancer</span></span>
<span data-ttu-id="35208-202">После обслуживания виртуальной Машины или tooexpand емкости, задайте hello *пулы Loadbalancerbackendaddresspool* свойство hello виртуального сетевого Адаптера toohello *BackendAddressPool* из [ Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="35208-202">After performing VM maintenance, or if you need tooexpand capacity, set hello *LoadBalancerBackendAddressPools* property of hello virtual NIC toohello *BackendAddressPool* from [Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):</span></span>

<span data-ttu-id="35208-203">Получите hello балансировки нагрузки:</span><span class="sxs-lookup"><span data-stu-id="35208-203">Get hello load balancer:</span></span>

```powershell
$lb = Get-AzureRMLoadBalancer `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myLoadBalancer 
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a><span data-ttu-id="35208-204">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="35208-204">Next steps</span></span>

<span data-ttu-id="35208-205">В этом учебнике вы создается подсистемы балансировки нагрузки и прикрепляется tooit виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="35208-205">In this tutorial, you created a load balancer and attached VMs tooit.</span></span> <span data-ttu-id="35208-206">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="35208-206">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="35208-207">Создание Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="35208-207">Create an Azure load balancer</span></span>
> * <span data-ttu-id="35208-208">Создание пробы работоспособности балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="35208-208">Create a load balancer health probe</span></span>
> * <span data-ttu-id="35208-209">создавать правила трафика подсистемы балансировки нагрузки;</span><span class="sxs-lookup"><span data-stu-id="35208-209">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="35208-210">Использовать настраиваемое расширение скриптов hello toocreate простого узла IIS</span><span class="sxs-lookup"><span data-stu-id="35208-210">Use hello Custom Script Extension toocreate a basic IIS site</span></span>
> * <span data-ttu-id="35208-211">Создание виртуальных машин и присоединения tooa балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="35208-211">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="35208-212">Просмотр балансировщика нагрузки в действии</span><span class="sxs-lookup"><span data-stu-id="35208-212">View a load balancer in action</span></span>
> * <span data-ttu-id="35208-213">добавлять и удалять виртуальные машины из подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="35208-213">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="35208-214">Как переместить следующий учебник toolearn toohello toomanage сети виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="35208-214">Advance toohello next tutorial toolearn how toomanage VM networking.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="35208-215">Управление виртуальными сетями Azure и виртуальными машинами Linux с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="35208-215">Manage VMs and virtual networks</span></span>](./tutorial-virtual-network.md)
