---
title: "Задает aaaCreating масштабирования виртуальных машин с помощью командлетов PowerShell | Документы Microsoft"
description: "Приступите к созданию своего первого масштабируемого набора виртуальных машин Azure и научитесь им управлять с помощью Azure PowerShell."
services: virtual-machines-windows
documentationcenter: 
author: danielsollondon
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 430d9d64-1f35-48f0-a4fd-9b69910ffa59
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: danielsollondon
ms.openlocfilehash: 7979be367d04c904b60d78849c1b751a52cc8caf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="creating-virtual-machine-scale-sets-using-powershell-cmdlets"></a><span data-ttu-id="16023-103">Создание масштабируемых наборов виртуальных машин с помощью командлетов PowerShell</span><span class="sxs-lookup"><span data-stu-id="16023-103">Creating Virtual Machine Scale Sets using PowerShell cmdlets</span></span>
<span data-ttu-id="16023-104">В этой статье рассматриваются примером как toocreate набора масштабирования виртуальных машин (VMSS).</span><span class="sxs-lookup"><span data-stu-id="16023-104">This article walks through an example of how toocreate a Virtual Machine scale set (VMSS).</span></span> <span data-ttu-id="16023-105">В нем создается масштабируемый набор из трех узлов со связанными сетью и хранилищем.</span><span class="sxs-lookup"><span data-stu-id="16023-105">It creates a scale set of three nodes, with associated Networking and Storage.</span></span>

## <a name="first-steps"></a><span data-ttu-id="16023-106">Первые шаги</span><span class="sxs-lookup"><span data-stu-id="16023-106">First Steps</span></span>
<span data-ttu-id="16023-107">Убедитесь, у вас есть hello установить последнюю версию модуля Azure PowerShell, необходимые toomaintain toomake том, что у вас есть командлеты PowerShell hello и создания набора масштабирования.</span><span class="sxs-lookup"><span data-stu-id="16023-107">Ensure you have hello latest Azure PowerShell module installed, toomake sure you have hello PowerShell commandlets needed toomaintain, and create scale sets.</span></span>
<span data-ttu-id="16023-108">Go средства командной строки toohello [здесь](http://aka.ms/webpi-azps) для hello последние доступные модули Azure.</span><span class="sxs-lookup"><span data-stu-id="16023-108">Go toohello command line tools [here](http://aka.ms/webpi-azps) for hello latest available Azure Modules.</span></span>

<span data-ttu-id="16023-109">toofind VMSS связанные командлеты, используйте строку hello поиска \*VMSS\*.</span><span class="sxs-lookup"><span data-stu-id="16023-109">toofind VMSS related commandlets, use hello search string \*VMSS\*.</span></span> <span data-ttu-id="16023-110">Например, _gcm *vmss*_.</span><span class="sxs-lookup"><span data-stu-id="16023-110">For example, _gcm *vmss*_</span></span>

## <a name="creating-a-vmss"></a><span data-ttu-id="16023-111">Создание VMSS</span><span class="sxs-lookup"><span data-stu-id="16023-111">Creating a VMSS</span></span>
#### <a name="create-resource-group"></a><span data-ttu-id="16023-112">Создать группу ресурсов</span><span class="sxs-lookup"><span data-stu-id="16023-112">Create Resource Group</span></span>
```
$loc = 'westus';
$rgname = 'mynewrgwu';
  New-AzureRmResourceGroup -Name $rgname -Location $loc -Force;
```

### <a name="create-networking-vnet--subnet"></a><span data-ttu-id="16023-113">Создание сетевой инфраструктуры (виртуальной сети и подсети)</span><span class="sxs-lookup"><span data-stu-id="16023-113">Create Networking (VNET / Subnet)</span></span>
#### <a name="subnet-specification"></a><span data-ttu-id="16023-114">Спецификация подсети</span><span class="sxs-lookup"><span data-stu-id="16023-114">Subnet Specification</span></span>
```
$subnetName = 'websubnet'
  $subnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix "10.0.0.0/24";
```

#### <a name="vnet-specification"></a><span data-ttu-id="16023-115">Спецификация виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="16023-115">VNET Specification</span></span>
```
$vnet = New-AzureRmVirtualNetwork -Force -Name ('vnet' + $rgname) -ResourceGroupName $rgname -Location $loc -AddressPrefix "10.0.0.0/16" -Subnet $subnet;
$vnet = Get-AzureRmVirtualNetwork -Name ('vnet' + $rgname) -ResourceGroupName $rgname;

# In this case assume hello new subnet is hello only one
$subnetId = $vnet.Subnets[0].Id;
```

#### <a name="create-public-ip-resource-tooallow-external-access"></a><span data-ttu-id="16023-116">Создание общих IP-ресурс tooAllow внешнего доступа</span><span class="sxs-lookup"><span data-stu-id="16023-116">Create Public IP Resource tooAllow External Access</span></span>
<span data-ttu-id="16023-117">Это будет привязанного toohello подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="16023-117">This will be bound toohello Load Balancer.</span></span>

```
$pubip = New-AzureRmPublicIpAddress -Force -Name ('pubip' + $rgname) -ResourceGroupName $rgname -Location $loc -AllocationMethod Dynamic -DomainNameLabel ('pubip' + $rgname);
$pubip = Get-AzureRmPublicIpAddress -Name ('pubip' + $rgname) -ResourceGroupName $rgname;
```

#### <a name="create-load-balancer"></a><span data-ttu-id="16023-118">Создание балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="16023-118">Create Load Balancer</span></span>
```
$frontendName = 'fe' + $rgname
$backendAddressPoolName = 'bepool' + $rgname
$probeName = 'vmssprobe' + $rgname
$inboundNatPoolName = 'innatpool' + $rgname
$lbruleName = 'lbrule' + $rgname
$lbName = 'vmsslb' + $rgname

# Bind Public IP tooLoad Balancer
$frontend = New-AzureRmLoadBalancerFrontendIpConfig -Name $frontendName -PublicIpAddress $pubip
```

#### <a name="configure-load-balancer"></a><span data-ttu-id="16023-119">Настройка балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="16023-119">Configure Load Balancer</span></span>
<span data-ttu-id="16023-120">Создать конфигурацию пула адресов серверной части, это будет совместно использоваться hello сетевые адаптеры виртуальных машин hello в наборе масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="16023-120">Create Backend Address Pool Config, this will be shared by hello NICs of hello VMs in hello scale set.</span></span>

```
$backendAddressPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name $backendAddressPoolName
```

<span data-ttu-id="16023-121">Необходимо задать порт пробы балансировкой нагрузки, изменить параметры hello в зависимости от приложения.</span><span class="sxs-lookup"><span data-stu-id="16023-121">Set Load Balanced Probe Port, change hello settings as appropriate for your application.</span></span>

```
$probe = New-AzureRmLoadBalancerProbeConfig -Name $probeName -RequestPath healthcheck.aspx -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
```

<span data-ttu-id="16023-122">Создайте пул NAT входящего трафика для прямого подключения перенаправленное (не Балансировка) toohello виртуальных машин в hello масштабирования, заданные через hello подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="16023-122">Create an inbound NAT pool for direct routed connectivity (not load balanced) toohello VMs in hello scale set via hello Load Balancer.</span></span> <span data-ttu-id="16023-123">Это toodemonstrate, с помощью протокола удаленного рабочего СТОЛА и могут не потребоваться в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="16023-123">This is toodemonstrate using RDP and may not be required in your application.</span></span>

```
$frontendpoolrangestart = 3360
$frontendpoolrangeend = 3370
$backendvmport = 3389
$inboundNatPool = New-AzureRmLoadBalancerInboundNatPoolConfig -Name $inboundNatPoolName -FrontendIPConfigurationId `
$frontend.Id -Protocol Tcp -FrontendPortRangeStart $frontendpoolrangestart -FrontendPortRangeEnd $frontendpoolrangeend -BackendPort $backendvmport;
```

<span data-ttu-id="16023-124">Создайте hello правило балансировки нагрузки в этом примере показано нагрузки балансировки порт 80 запросов, с использованием параметров hello из предыдущих шагов.</span><span class="sxs-lookup"><span data-stu-id="16023-124">Create hello Load Balanced Rule, this example shows load balancing port 80 requests, using hello settings from previous steps.</span></span>

```
$protocol = 'Tcp'
$feLBPort = 80
$beLBPort = 80

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name $lbruleName `
-FrontendIPConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -Protocol $protocol -FrontendPort $feLBPort -BackendPort $beLBPort `
-IdleTimeoutInMinutes 15 -EnableFloatingIP -LoadDistribution SourceIP -Verbose;
```

<span data-ttu-id="16023-125">Создайте балансировщик нагрузки с конфигурацией.</span><span class="sxs-lookup"><span data-stu-id="16023-125">Create Load Balancer with configuration.</span></span>

```
$actualLb = New-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname -Location $loc `
-FrontendIpConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -LoadBalancingRule $lbrule -InboundNatPool $inboundNatPool -Verbose;
```

<span data-ttu-id="16023-126">Проверьте параметры балансировки Нагрузки, проверьте нагрузки балансировкой порт конфигураций, обратите внимание, что вы не увидите создаются правила NAT для входящего трафика до hello виртуальные машины в наборе масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="16023-126">Check  LB settings, check load balanced port configs, note, you will not see Inbound NAT rules until hello VMs in hello scale set are created.</span></span>

```
$expectedLb = Get-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname
```

##### <a name="configure-and-create-hello-scale-set"></a><span data-ttu-id="16023-127">Настройка и создание hello в наборе</span><span class="sxs-lookup"><span data-stu-id="16023-127">Configure and Create hello scale set</span></span>
<span data-ttu-id="16023-128">Обратите внимание, что в этом примере инфраструктуры показано, как распространить tooset вверх и масштабирования веб-трафик через набор масштабирования hello, но hello образы виртуальных машин, указанные здесь нет установлен веб-служб.</span><span class="sxs-lookup"><span data-stu-id="16023-128">Note, this infrastructure example shows how tooset up distribute and scale web traffic across hello scale set, but hello VMs Images specified here do not have any web services installed.</span></span>

```
# specify scale set Name
$vmssName = 'vmss' + $rgname;

## specify VMSS specific details
$adminUsername = 'azadmin';
$adminPassword = "Password1234!";

$PublisherName = 'MicrosoftWindowsServer'
$Offer         = 'WindowsServer'
$Sku          = '2012-R2-Datacenter'
$Version       = 'latest'
$vmNamePrefix = 'winvmss'

###add an extension
$extname = 'BGInfo';
$publisher = 'Microsoft.Compute';
$exttype = 'BGInfo';
$extver = '2.1';
```

<span data-ttu-id="16023-129">Привязки Сетевых tooLoad балансировки и подсети</span><span class="sxs-lookup"><span data-stu-id="16023-129">Bind NIC tooLoad Balancer and Subnet</span></span>

```
$ipCfg = New-AzureRmVmssIPConfig -Name 'nic' `
-LoadBalancerInboundNatPoolsId $actualLb.InboundNatPools[0].Id `
-LoadBalancerBackendAddressPoolsId $actualLb.BackendAddressPools[0].Id `
-SubnetId $subnetId;
```

<span data-ttu-id="16023-130">Создание конфигурации масштабируемого набора</span><span class="sxs-lookup"><span data-stu-id="16023-130">Create scale set Config</span></span>

```
# Specify number of nodes
$numberofnodes = 3

$vmss = New-AzureRmVmssConfig -Location $loc -SkuCapacity $numberofnodes -SkuName 'Standard_A2' -UpgradePolicyMode 'automatic' `
    | Add-AzureRmVmssNetworkInterfaceConfiguration -Name $subnetName -Primary $true -IPConfiguration $ipCfg `
    | Set-AzureRmVmssOSProfile -ComputerNamePrefix $vmNamePrefix -AdminUsername $adminUsername -AdminPassword $adminPassword `
    | Set-AzureRmVmssStorageProfile -OsDiskCreateOption 'FromImage' -OsDiskCaching 'None' `
    -ImageReferenceOffer $Offer -ImageReferenceSku $Sku -ImageReferenceVersion $Version `
    -ImageReferencePublisher $PublisherName `
    | Add-AzureRmVmssExtension -Name $extname -Publisher $publisher -Type $exttype -TypeHandlerVersion $extver -AutoUpgradeMinorVersion $true
```

<span data-ttu-id="16023-131">Сборка конфигурации масштабируемого набора</span><span class="sxs-lookup"><span data-stu-id="16023-131">Build scale set configuration</span></span>

```
New-AzureRmVmss -ResourceGroupName $rgname -Name $vmssName -VirtualMachineScaleSet $vmss -Verbose;
```

<span data-ttu-id="16023-132">Теперь вы создали набор масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="16023-132">Now you have created hello scale set.</span></span> <span data-ttu-id="16023-133">Можно проверить подключение toohello отдельных виртуальных Машин с помощью протокола удаленного рабочего СТОЛА в этом примере:</span><span class="sxs-lookup"><span data-stu-id="16023-133">You can test connecting toohello individual VM using RDP in this example:</span></span>

```
VM0 : pubipmynewrgwu.westus.cloudapp.azure.com:3360
VM1 : pubipmynewrgwu.westus.cloudapp.azure.com:3361
VM2 : pubipmynewrgwu.westus.cloudapp.azure.com:3362
```
