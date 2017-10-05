---
title: "Создание масштабируемых наборов виртуальных машин с помощью командлетов PowerShell | Документация Майкрософт"
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
ms.openlocfilehash: a3a36028a75d6cb7eb36277f3e2b5ab833c96a96
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="creating-virtual-machine-scale-sets-using-powershell-cmdlets"></a><span data-ttu-id="61e81-103">Создание масштабируемых наборов виртуальных машин с помощью командлетов PowerShell</span><span class="sxs-lookup"><span data-stu-id="61e81-103">Creating Virtual Machine Scale Sets using PowerShell cmdlets</span></span>
<span data-ttu-id="61e81-104">В этой статье подробно рассматривается пример того, как создать масштабируемый набор виртуальных машин (VMSS).</span><span class="sxs-lookup"><span data-stu-id="61e81-104">This article walks through an example of how to create a Virtual Machine scale set (VMSS).</span></span> <span data-ttu-id="61e81-105">В нем создается масштабируемый набор из трех узлов со связанными сетью и хранилищем.</span><span class="sxs-lookup"><span data-stu-id="61e81-105">It creates a scale set of three nodes, with associated Networking and Storage.</span></span>

## <a name="first-steps"></a><span data-ttu-id="61e81-106">Первые шаги</span><span class="sxs-lookup"><span data-stu-id="61e81-106">First Steps</span></span>
<span data-ttu-id="61e81-107">Убедитесь, что у вас установлен последний модуль Azure PowerShell и доступны командлеты PowerShell, необходимые для обслуживания и создания масштабируемых наборов.</span><span class="sxs-lookup"><span data-stu-id="61e81-107">Ensure you have the latest Azure PowerShell module installed, to make sure you have the PowerShell commandlets needed to maintain, and create scale sets.</span></span>
<span data-ttu-id="61e81-108">Перейдите к расположенным [здесь](http://aka.ms/webpi-azps) программам командной строки, чтобы узнать о последних доступных модулях Azure.</span><span class="sxs-lookup"><span data-stu-id="61e81-108">Go to the command line tools [here](http://aka.ms/webpi-azps) for the latest available Azure Modules.</span></span>

<span data-ttu-id="61e81-109">Чтобы найти связанные с VMSS командлеты, используйте строку поиска \*VMSS\*.</span><span class="sxs-lookup"><span data-stu-id="61e81-109">To find VMSS related commandlets, use the search string \*VMSS\*.</span></span> <span data-ttu-id="61e81-110">Например, _gcm *vmss*_.</span><span class="sxs-lookup"><span data-stu-id="61e81-110">For example, _gcm *vmss*_</span></span>

## <a name="creating-a-vmss"></a><span data-ttu-id="61e81-111">Создание VMSS</span><span class="sxs-lookup"><span data-stu-id="61e81-111">Creating a VMSS</span></span>
#### <a name="create-resource-group"></a><span data-ttu-id="61e81-112">Создать группу ресурсов</span><span class="sxs-lookup"><span data-stu-id="61e81-112">Create Resource Group</span></span>
```
$loc = 'westus';
$rgname = 'mynewrgwu';
  New-AzureRmResourceGroup -Name $rgname -Location $loc -Force;
```

### <a name="create-networking-vnet--subnet"></a><span data-ttu-id="61e81-113">Создание сетевой инфраструктуры (виртуальной сети и подсети)</span><span class="sxs-lookup"><span data-stu-id="61e81-113">Create Networking (VNET / Subnet)</span></span>
#### <a name="subnet-specification"></a><span data-ttu-id="61e81-114">Спецификация подсети</span><span class="sxs-lookup"><span data-stu-id="61e81-114">Subnet Specification</span></span>
```
$subnetName = 'websubnet'
  $subnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix "10.0.0.0/24";
```

#### <a name="vnet-specification"></a><span data-ttu-id="61e81-115">Спецификация виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="61e81-115">VNET Specification</span></span>
```
$vnet = New-AzureRmVirtualNetwork -Force -Name ('vnet' + $rgname) -ResourceGroupName $rgname -Location $loc -AddressPrefix "10.0.0.0/16" -Subnet $subnet;
$vnet = Get-AzureRmVirtualNetwork -Name ('vnet' + $rgname) -ResourceGroupName $rgname;

# In this case assume the new subnet is the only one
$subnetId = $vnet.Subnets[0].Id;
```

#### <a name="create-public-ip-resource-to-allow-external-access"></a><span data-ttu-id="61e81-116">Создание ресурса общедоступного IP-адреса для внешнего доступа</span><span class="sxs-lookup"><span data-stu-id="61e81-116">Create Public IP Resource to Allow External Access</span></span>
<span data-ttu-id="61e81-117">Выполняется привязка к подсистеме балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="61e81-117">This will be bound to the Load Balancer.</span></span>

```
$pubip = New-AzureRmPublicIpAddress -Force -Name ('pubip' + $rgname) -ResourceGroupName $rgname -Location $loc -AllocationMethod Dynamic -DomainNameLabel ('pubip' + $rgname);
$pubip = Get-AzureRmPublicIpAddress -Name ('pubip' + $rgname) -ResourceGroupName $rgname;
```

#### <a name="create-load-balancer"></a><span data-ttu-id="61e81-118">Создание балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="61e81-118">Create Load Balancer</span></span>
```
$frontendName = 'fe' + $rgname
$backendAddressPoolName = 'bepool' + $rgname
$probeName = 'vmssprobe' + $rgname
$inboundNatPoolName = 'innatpool' + $rgname
$lbruleName = 'lbrule' + $rgname
$lbName = 'vmsslb' + $rgname

# Bind Public IP to Load Balancer
$frontend = New-AzureRmLoadBalancerFrontendIpConfig -Name $frontendName -PublicIpAddress $pubip
```

#### <a name="configure-load-balancer"></a><span data-ttu-id="61e81-119">Настройка балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="61e81-119">Configure Load Balancer</span></span>
<span data-ttu-id="61e81-120">Создайте конфигурацию внутреннего пула адресов, которая будет совместно использоваться сетевыми картами виртуальных машин в масштабируемом наборе.</span><span class="sxs-lookup"><span data-stu-id="61e81-120">Create Backend Address Pool Config, this will be shared by the NICs of the VMs in the scale set.</span></span>

```
$backendAddressPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name $backendAddressPoolName
```

<span data-ttu-id="61e81-121">Задайте порт пробы с балансировкой нагрузки и настройте подходящие параметры для приложения.</span><span class="sxs-lookup"><span data-stu-id="61e81-121">Set Load Balanced Probe Port, change the settings as appropriate for your application.</span></span>

```
$probe = New-AzureRmLoadBalancerProbeConfig -Name $probeName -RequestPath healthcheck.aspx -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
```

<span data-ttu-id="61e81-122">Создайте пул входящих подключений NAT для подключений с прямой маршрутизацией (без балансировки) к виртуальным машинам в масштабируемом наборе с помощью подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="61e81-122">Create an inbound NAT pool for direct routed connectivity (not load balanced) to the VMs in the scale set via the Load Balancer.</span></span> <span data-ttu-id="61e81-123">Это нужно для демонстрации использования протокола RDP и может не потребоваться в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="61e81-123">This is to demonstrate using RDP and may not be required in your application.</span></span>

```
$frontendpoolrangestart = 3360
$frontendpoolrangeend = 3370
$backendvmport = 3389
$inboundNatPool = New-AzureRmLoadBalancerInboundNatPoolConfig -Name $inboundNatPoolName -FrontendIPConfigurationId `
$frontend.Id -Protocol Tcp -FrontendPortRangeStart $frontendpoolrangestart -FrontendPortRangeEnd $frontendpoolrangeend -BackendPort $backendvmport;
```

<span data-ttu-id="61e81-124">Создайте правило с балансировкой нагрузки. В этом примере показаны запросы через порт 80 для балансировки нагрузки с использованием параметров из предыдущих шагов.</span><span class="sxs-lookup"><span data-stu-id="61e81-124">Create the Load Balanced Rule, this example shows load balancing port 80 requests, using the settings from previous steps.</span></span>

```
$protocol = 'Tcp'
$feLBPort = 80
$beLBPort = 80

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name $lbruleName `
-FrontendIPConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -Protocol $protocol -FrontendPort $feLBPort -BackendPort $beLBPort `
-IdleTimeoutInMinutes 15 -EnableFloatingIP -LoadDistribution SourceIP -Verbose;
```

<span data-ttu-id="61e81-125">Создайте балансировщик нагрузки с конфигурацией.</span><span class="sxs-lookup"><span data-stu-id="61e81-125">Create Load Balancer with configuration.</span></span>

```
$actualLb = New-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname -Location $loc `
-FrontendIpConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -LoadBalancingRule $lbrule -InboundNatPool $inboundNatPool -Verbose;
```

<span data-ttu-id="61e81-126">Проверьте параметры балансировки нагрузки и конфигурации портов с балансировкой нагрузки. Помните, что правила NAT для входящего трафика отображаются только после создания виртуальных машин в масштабируемом наборе.</span><span class="sxs-lookup"><span data-stu-id="61e81-126">Check  LB settings, check load balanced port configs, note, you will not see Inbound NAT rules until the VMs in the scale set are created.</span></span>

```
$expectedLb = Get-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname
```

##### <a name="configure-and-create-the-scale-set"></a><span data-ttu-id="61e81-127">Настройка и создание масштабируемого набора</span><span class="sxs-lookup"><span data-stu-id="61e81-127">Configure and Create the scale set</span></span>
<span data-ttu-id="61e81-128">Обратите внимание, что в этом примере инфраструктуры показано, как настроить распространение и масштабирование веб-трафика в масштабируемом наборе, однако в указанных здесь образах виртуальных машин нет установленных веб-служб.</span><span class="sxs-lookup"><span data-stu-id="61e81-128">Note, this infrastructure example shows how to set up distribute and scale web traffic across the scale set, but the VMs Images specified here do not have any web services installed.</span></span>

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

<span data-ttu-id="61e81-129">Привязка сетевой карты к балансировщику нагрузки и подсети</span><span class="sxs-lookup"><span data-stu-id="61e81-129">Bind NIC to Load Balancer and Subnet</span></span>

```
$ipCfg = New-AzureRmVmssIPConfig -Name 'nic' `
-LoadBalancerInboundNatPoolsId $actualLb.InboundNatPools[0].Id `
-LoadBalancerBackendAddressPoolsId $actualLb.BackendAddressPools[0].Id `
-SubnetId $subnetId;
```

<span data-ttu-id="61e81-130">Создание конфигурации масштабируемого набора</span><span class="sxs-lookup"><span data-stu-id="61e81-130">Create scale set Config</span></span>

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

<span data-ttu-id="61e81-131">Сборка конфигурации масштабируемого набора</span><span class="sxs-lookup"><span data-stu-id="61e81-131">Build scale set configuration</span></span>

```
New-AzureRmVmss -ResourceGroupName $rgname -Name $vmssName -VirtualMachineScaleSet $vmss -Verbose;
```

<span data-ttu-id="61e81-132">Теперь вы создали масштабируемый набор.</span><span class="sxs-lookup"><span data-stu-id="61e81-132">Now you have created the scale set.</span></span> <span data-ttu-id="61e81-133">Подключение к отдельной виртуальной машине можно проверить с помощью протокола удаленного рабочего стола в этом примере:</span><span class="sxs-lookup"><span data-stu-id="61e81-133">You can test connecting to the individual VM using RDP in this example:</span></span>

```
VM0 : pubipmynewrgwu.westus.cloudapp.azure.com:3360
VM1 : pubipmynewrgwu.westus.cloudapp.azure.com:3361
VM2 : pubipmynewrgwu.westus.cloudapp.azure.com:3362
```
