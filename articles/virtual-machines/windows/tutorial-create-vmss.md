---
title: "aaaCreate виртуальной машины шкалы наборов для Windows в Azure | Документы Microsoft"
description: "Создание и развертывание высокодоступного приложения на виртуальных машинах Windows с помощью масштабируемого набора виртуальных машин."
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: 
ms.topic: article
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: a3914571005c28a492c069d880992630851afae7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-windows"></a><span data-ttu-id="025b9-103">Создание масштабируемого набора виртуальных машин и развертывание высокодоступного приложения в Windows</span><span class="sxs-lookup"><span data-stu-id="025b9-103">Create a Virtual Machine Scale Set and deploy a highly available app on Windows</span></span>
<span data-ttu-id="025b9-104">Набор масштабирования виртуальной машины дает toodeploy и управление набором идентичными, автоматического масштабирования виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="025b9-104">A virtual machine scale set allows you toodeploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="025b9-105">Можно вручную масштабировать hello число виртуальных машин в наборе масштабирования hello, или определить tooautoscale правила на основе использования ЦП, объем памяти или сетевой трафик.</span><span class="sxs-lookup"><span data-stu-id="025b9-105">You can scale hello number of VMs in hello scale set manually, or define rules tooautoscale based on CPU usage, memory demand, or network traffic.</span></span> <span data-ttu-id="025b9-106">В рамках этого руководства вы развернете масштабируемый набор виртуальных машин в Azure.</span><span class="sxs-lookup"><span data-stu-id="025b9-106">In this tutorial, you deploy a virtual machine scale set in Azure.</span></span> <span data-ttu-id="025b9-107">Вы узнаете, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="025b9-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="025b9-108">Использовать настраиваемое расширение скриптов hello toodefine tooscale узла IIS</span><span class="sxs-lookup"><span data-stu-id="025b9-108">Use hello Custom Script Extension toodefine an IIS site tooscale</span></span>
> * <span data-ttu-id="025b9-109">Создание балансировщика нагрузки для масштабируемого набора</span><span class="sxs-lookup"><span data-stu-id="025b9-109">Create a load balancer for your scale set</span></span>
> * <span data-ttu-id="025b9-110">создавать масштабируемый набор виртуальных машин;</span><span class="sxs-lookup"><span data-stu-id="025b9-110">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="025b9-111">Увеличение или уменьшение числа hello экземпляров в наборе масштабирования</span><span class="sxs-lookup"><span data-stu-id="025b9-111">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="025b9-112">Создание правил автомасштабирования</span><span class="sxs-lookup"><span data-stu-id="025b9-112">Create autoscale rules</span></span>

<span data-ttu-id="025b9-113">Этот учебник требует hello Azure PowerShell модуль версии 3.6 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="025b9-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="025b9-114">Запустите ` Get-Module -ListAvailable AzureRM` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="025b9-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="025b9-115">Получить tooupgrade [установите Azure PowerShell модуль](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="025b9-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="scale-set-overview"></a><span data-ttu-id="025b9-116">Обзор масштабируемого набора</span><span class="sxs-lookup"><span data-stu-id="025b9-116">Scale Set overview</span></span>
<span data-ttu-id="025b9-117">Наборы масштабирования используются одинаковые принципы, как вы узнали о в предыдущем учебнике hello слишком[создать высокодоступные виртуальные машины](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="025b9-117">Scale sets use similar concepts as you learned about in hello previous tutorial too[Create highly available VMs](tutorial-availability-sets.md).</span></span> <span data-ttu-id="025b9-118">Виртуальные машины в масштабируемом наборе распределяются по доменам сбоя и доменам обновления, как и виртуальные машины в группе доступности.</span><span class="sxs-lookup"><span data-stu-id="025b9-118">VMs in a scale set are distributed across fault and update domains just like VMs in an availability set.</span></span>

<span data-ttu-id="025b9-119">Виртуальные машины создаются в масштабируемом наборе по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="025b9-119">VMs are created as needed in a scale set.</span></span> <span data-ttu-id="025b9-120">Определение правила toocontrol автомасштабирования как и когда добавляются или удаляются из hello масштабный набор виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="025b9-120">You define autoscale rules toocontrol how and when VMs are added or removed from hello scale set.</span></span> <span data-ttu-id="025b9-121">Эти правила могут активироваться на основе метрик, таких как использование ЦП, использование памяти или сетевой трафик.</span><span class="sxs-lookup"><span data-stu-id="025b9-121">These rules can trigger based on metrics such as CPU load, memory usage, or network traffic.</span></span>

<span data-ttu-id="025b9-122">Масштаб задает поддержки вверх too1 000 виртуальных машин при использовании образа платформы Azure.</span><span class="sxs-lookup"><span data-stu-id="025b9-122">Scale sets support up too1,000 VMs when you use an Azure platform image.</span></span> <span data-ttu-id="025b9-123">Для рабочих нагрузок с значительные установки или настройки требования виртуальной Машины, вы можете слишком[создать образ виртуальной Машины](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="025b9-123">For workloads with significant installation or VM customization requirements, you may wish too[Create a custom VM image](tutorial-custom-images.md).</span></span> <span data-ttu-id="025b9-124">Можно создать too100 виртуальных машин в наборе, при использовании настраиваемого образа масштабирования.</span><span class="sxs-lookup"><span data-stu-id="025b9-124">You can create up too100 VMs in a scale set when using a custom image.</span></span>


## <a name="create-an-app-tooscale"></a><span data-ttu-id="025b9-125">Создание приложения tooscale</span><span class="sxs-lookup"><span data-stu-id="025b9-125">Create an app tooscale</span></span>
<span data-ttu-id="025b9-126">Прежде чем создать масштабируемый набор, выполните команду [az group create](/powershell/module/azurerm.resources/new-azurermresourcegroup) для создания группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="025b9-126">Before you can create a scale set, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="025b9-127">Hello следующий пример создает группу ресурсов с именем *myResourceGroupAutomate* в hello *EastUS* расположение:</span><span class="sxs-lookup"><span data-stu-id="025b9-127">hello following example creates a resource group named *myResourceGroupAutomate* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupScaleSet -Location EastUS
```

<span data-ttu-id="025b9-128">В более ранних учебника вы узнали, каким образом слишком[конфигурацию виртуальной Машины автоматизировать](tutorial-automate-vm-deployment.md) с использованием настраиваемого расширения скриптов "hello".</span><span class="sxs-lookup"><span data-stu-id="025b9-128">In an earlier tutorial, you learned how too[Automate VM configuration](tutorial-automate-vm-deployment.md) using hello Custom Script Extension.</span></span> <span data-ttu-id="025b9-129">Создание конфигурации набор масштабирования и применить tooinstall настраиваемое расширение скриптов и настроить службы IIS:</span><span class="sxs-lookup"><span data-stu-id="025b9-129">Create a scale set configuration then apply a Custom Script Extension tooinstall and configure IIS:</span></span>

```powershell
# Create a config object
$vmssConfig = New-AzureRmVmssConfig `
    -Location EastUS `
    -SkuCapacity 2 `
    -SkuName Standard_DS2 `
    -UpgradePolicyMode Automatic

# Define hello script for your Custom Script Extension toorun
$publicSettings = @{
    "fileUris" = (,"https://raw.githubusercontent.com/iainfoulds/azure-samples/master/automate-iis.ps1");
    "commandToExecute" = "powershell -ExecutionPolicy Unrestricted -File automate-iis.ps1"
}

# Use Custom Script Extension tooinstall IIS and configure basic website
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig `
    -Name "customScript" `
    -Publisher "Microsoft.Compute" `
    -Type "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -Setting $publicSettings
```

## <a name="create-scale-load-balancer"></a><span data-ttu-id="025b9-130">Создание подсистемы балансировки нагрузки для масштабируемого набора</span><span class="sxs-lookup"><span data-stu-id="025b9-130">Create scale load balancer</span></span>
<span data-ttu-id="025b9-131">Azure Load Balancer представляет собой балансировщик нагрузки уровня 4 (TCP, UDP), который обеспечивает высокий уровень доступности, распределяя входящий трафик между работоспособными виртуальными машинами.</span><span class="sxs-lookup"><span data-stu-id="025b9-131">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="025b9-132">Отслеживает данный порт на каждой виртуальной Машине зонда работоспособности подсистемы балансировки нагрузки и только распределяет трафик tooan оперативной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="025b9-132">A load balancer health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span> <span data-ttu-id="025b9-133">Дополнительные сведения см. Далее учебнике hello на [как tooload сбалансировать виртуальных машин Windows](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="025b9-133">For more information, see hello next tutorial on [How tooload balance Windows virtual machines](tutorial-load-balancer.md).</span></span>

<span data-ttu-id="025b9-134">Создайте подсистему балансировки нагрузки с общедоступным IP-адресом, которая распределяет веб-трафик через порт 80.</span><span class="sxs-lookup"><span data-stu-id="025b9-134">Create a load balancer that has a public IP address and distributes web traffic on port 80:</span></span>

```powershell
# Create a public IP address
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupScaleSet `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP

# Create a frontend and backend IP pool
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool

# Create hello load balancer
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupScaleSet `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool

# Create a load balancer health probe on port 80
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2

# Create a load balancer rule toodistribute traffic on port 80
Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80

# Update hello load balancer configuration
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="create-a-scale-set"></a><span data-ttu-id="025b9-135">Создание масштабируемого набора</span><span class="sxs-lookup"><span data-stu-id="025b9-135">Create a scale set</span></span>
<span data-ttu-id="025b9-136">Теперь создайте масштабируемый набор виртуальных машин с помощью командлета [New-AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="025b9-136">Now create a virtual machine scale set with [New-AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="025b9-137">Hello следующий пример создает именованный наборе масштабирования *myScaleSet*:</span><span class="sxs-lookup"><span data-stu-id="025b9-137">hello following example creates a scale set named *myScaleSet*:</span></span>

```powershell
# Reference a virtual machine image from hello gallery
Set-AzureRmVmssStorageProfile $vmssConfig `
  -ImageReferencePublisher MicrosoftWindowsServer `
  -ImageReferenceOffer WindowsServer `
  -ImageReferenceSku 2016-Datacenter `
  -ImageReferenceVersion latest

# Set up information for authenticating with hello virtual machine
Set-AzureRmVmssOsProfile $vmssConfig `
  -AdminUsername azureuser `
  -AdminPassword P@ssword! `
  -ComputerNamePrefix myVM

# Create hello virtual network resources
$subnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name "mySubnet" `
  -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName "myResourceGroupScaleSet" `
  -Name "myVnet" `
  -Location "EastUS" `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $subnet
$ipConfig = New-AzureRmVmssIpConfig `
  -Name "myIPConfig" `
  -LoadBalancerBackendAddressPoolsId $lb.BackendAddressPools[0].Id `
  -SubnetId $vnet.Subnets[0].Id

# Attach hello virtual network toohello config object
Add-AzureRmVmssNetworkInterfaceConfiguration `
  -VirtualMachineScaleSet $vmssConfig `
  -Name "network-config" `
  -Primary $true `
  -IPConfiguration $ipConfig

# Create hello scale set with hello config object (this step might take a few minutes)
New-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -Name myScaleSet `
  -VirtualMachineScaleSet $vmssConfig
```

<span data-ttu-id="025b9-138">Он занимает несколько минут toocreate и настроить все hello масштабирования набор ресурсов виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="025b9-138">It takes a few minutes toocreate and configure all hello scale set resources and VMs.</span></span>


## <a name="test-your-app"></a><span data-ttu-id="025b9-139">Тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="025b9-139">Test your app</span></span>
<span data-ttu-id="025b9-140">toosee веб-сайта IIS в действии, получить hello общедоступный IP-адрес балансировки нагрузки, с [Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="025b9-140">toosee your IIS website in action, obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="025b9-141">Hello следующий пример извлекает hello IP-адрес для *myPublicIP* создана как часть набора масштабирования hello:</span><span class="sxs-lookup"><span data-stu-id="025b9-141">hello following example obtains hello IP address for *myPublicIP* created as part of hello scale set:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupScaleSet -Name myPublicIP | select IpAddress
```

<span data-ttu-id="025b9-142">Введите hello общедоступный IP-адрес в tooa веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="025b9-142">Enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="025b9-143">будут отображены приложение Hello, включая имя узла виртуальной Машины, hello нагрузки трафика балансировки распределенных для hello hello:</span><span class="sxs-lookup"><span data-stu-id="025b9-143">hello app is displayed, including hello hostname of hello VM that hello load balancer distributed traffic to:</span></span>

![Выполнение сайта IIS](./media/tutorial-create-vmss/running-iis-site.png)

<span data-ttu-id="025b9-145">набор в действии масштабирования hello toosee, вы может принудительное обновление вашего веб-браузера toosee hello нагрузку балансировки распределения трафика между все виртуальные машины hello, запускающий ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="025b9-145">toosee hello scale set in action, you can force-refresh your web browser toosee hello load balancer distribute traffic across all hello VMs running your app.</span></span>


## <a name="management-tasks"></a><span data-ttu-id="025b9-146">Задачи управления</span><span class="sxs-lookup"><span data-stu-id="025b9-146">Management tasks</span></span>
<span data-ttu-id="025b9-147">На протяжении жизненного цикла hello набора масштабирования hello, может потребоваться toorun одну или несколько задач управления.</span><span class="sxs-lookup"><span data-stu-id="025b9-147">Throughout hello lifecycle of hello scale set, you may need toorun one or more management tasks.</span></span> <span data-ttu-id="025b9-148">Кроме того вы можете toocreate скрипты, автоматизирующие различные жизненного цикла задачи.</span><span class="sxs-lookup"><span data-stu-id="025b9-148">Additionally, you may want toocreate scripts that automate various lifecycle-tasks.</span></span> <span data-ttu-id="025b9-149">Azure PowerShell предоставляет toodo быстро этих задач.</span><span class="sxs-lookup"><span data-stu-id="025b9-149">Azure PowerShell provides a quick way toodo those tasks.</span></span> <span data-ttu-id="025b9-150">Ниже приведено несколько распространенных задач.</span><span class="sxs-lookup"><span data-stu-id="025b9-150">Here are a few common tasks.</span></span>

### <a name="view-vms-in-a-scale-set"></a><span data-ttu-id="025b9-151">Просмотр виртуальных машин в масштабируемом наборе</span><span class="sxs-lookup"><span data-stu-id="025b9-151">View VMs in a scale set</span></span>
<span data-ttu-id="025b9-152">Список виртуальных машин, работающих в шкалу tooview набора, используйте [Get AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) следующим образом:</span><span class="sxs-lookup"><span data-stu-id="025b9-152">tooview a list of VMs running in your scale set, use [Get-AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) as follows:</span></span>

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Loop through hello instanaces in your scale set
for ($i=1; $i -le ($scaleset.Sku.Capacity - 1); $i++) {
    Get-AzureRmVmssVM -ResourceGroupName myResourceGroupScaleSet `
      -VMScaleSetName myScaleSet `
      -InstanceId $i
}
```


### <a name="increase-or-decrease-vm-instances"></a><span data-ttu-id="025b9-153">Увеличение или уменьшение числа экземпляров виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="025b9-153">Increase or decrease VM instances</span></span>
<span data-ttu-id="025b9-154">число экземпляров hello toosee в настоящее время на шкале установки, используйте [Get AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) и запросов на *sku.capacity*:</span><span class="sxs-lookup"><span data-stu-id="025b9-154">toosee hello number of instances you currently have in a scale set, use [Get-AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) and query on *sku.capacity*:</span></span>

```powershell
Get-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -VMScaleSetName myScaleSet | `
    Select -ExpandProperty Sku
```

<span data-ttu-id="025b9-155">Можно затем вручную увеличить или уменьшить hello количество виртуальных машин в наборе с масштабирования hello [AzureRmVmss обновление](/powershell/module/azurerm.compute/update-azurermvmss).</span><span class="sxs-lookup"><span data-stu-id="025b9-155">You can then manually increase or decrease hello number of virtual machines in hello scale set with [Update-AzureRmVmss](/powershell/module/azurerm.compute/update-azurermvmss).</span></span> <span data-ttu-id="025b9-156">Hello следующий пример задает hello число виртуальных машин в ваш набор слишком масштабирования*5*:</span><span class="sxs-lookup"><span data-stu-id="025b9-156">hello following example sets hello number of VMs in your scale set too*5*:</span></span>

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Set and update hello capacity of your scale set
$scaleset.sku.capacity = 5
Update-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -Name myScaleSet `
    -VirtualMachineScaleSet $scaleset
```

<span data-ttu-id="025b9-157">Если несколько минут tooupdate hello указанного числа экземпляров в наборе масштабирования.</span><span class="sxs-lookup"><span data-stu-id="025b9-157">If takes a few minutes tooupdate hello specified number of instances in your scale set.</span></span>


### <a name="configure-autoscale-rules"></a><span data-ttu-id="025b9-158">Настройка правил автомасштабирования</span><span class="sxs-lookup"><span data-stu-id="025b9-158">Configure autoscale rules</span></span>
<span data-ttu-id="025b9-159">Вместо установки вручную масштабирование hello число экземпляров в на шкале, можно определить правила автомасштабирования.</span><span class="sxs-lookup"><span data-stu-id="025b9-159">Rather than manually scaling hello number of instances in your scale set, you define autoscale rules.</span></span> <span data-ttu-id="025b9-160">Эти правила отслеживать hello экземпляры в шкалу задать и реагировать соответствующим образом на основе метрик и порогов, определенных пользователем.</span><span class="sxs-lookup"><span data-stu-id="025b9-160">These rules monitor hello instances in your scale set and respond accordingly based on metrics and thresholds you define.</span></span> <span data-ttu-id="025b9-161">Следующий пример Hello масштабируемостью hello число экземпляров на единицу при hello среднюю нагрузку ЦП больше, чем на 60% в течение 5 минут.</span><span class="sxs-lookup"><span data-stu-id="025b9-161">hello following example scales out hello number of instances by one when hello average CPU load is greater than 60% over a 5 minute period.</span></span> <span data-ttu-id="025b9-162">Если затем нагрузки Средняя нагрузка на ЦП hello падает ниже 30% в течение 5 минут, экземпляры hello масштабируются в одним экземпляром:</span><span class="sxs-lookup"><span data-stu-id="025b9-162">If hello average CPU load then drops below 30% over a 5 minute period, hello instances are scaled in by one instance:</span></span>

```powershell
# Define your scale set information
$mySubscriptionId = (Get-AzureRmSubscription).Id
$myResourceGroup = "myResourceGroupScaleSet"
$myScaleSet = "myScaleSet"
$myLocation = "East US"

# Create a scale up rule tooincrease hello number instances after 60% average CPU usage exceeded for a 5 minute period
$myRuleScaleUp = New-AzureRmAutoscaleRule `
  -MetricName "Percentage CPU" `
  -MetricResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -Operator GreaterThan `
  -MetricStatistic Average `
  -Threshold 60 `
  -TimeGrain 00:01:00 `
  -TimeWindow 00:05:00 `
  -ScaleActionCooldown 00:05:00 `
  -ScaleActionDirection Increase `
  -ScaleActionValue 1

# Create a scale down rule toodecrease hello number of instances after 30% average CPU usage over a 5 minute period
$myRuleScaleDown = New-AzureRmAutoscaleRule `
  -MetricName "Percentage CPU" `
  -MetricResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -Operator LessThan `
  -MetricStatistic Average `
  -Threshold 30 `
  -TimeGrain 00:01:00 `
  -TimeWindow 00:05:00 `
  -ScaleActionCooldown 00:05:00 `
  -ScaleActionDirection Decrease `
  -ScaleActionValue 1

# Create a scale profile with your scale up and scale down rules
$myScaleProfile = New-AzureRmAutoscaleProfile `
  -DefaultCapacity 2  `
  -MaximumCapacity 10 `
  -MinimumCapacity 2 `
  -Rules $myRuleScaleUp,$myRuleScaleDown `
  -Name "autoprofile"

# Apply hello autoscale rules
Add-AzureRmAutoscaleSetting `
  -Location $myLocation `
  -Name "autosetting" `
  -ResourceGroup $myResourceGroup `
  -TargetResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -AutoscaleProfiles $myScaleProfile
```


## <a name="next-steps"></a><span data-ttu-id="025b9-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="025b9-163">Next steps</span></span>
<span data-ttu-id="025b9-164">В рамках этого руководства вы создали набор масштабирования виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="025b9-164">In this tutorial, you created a virtual machine scale set.</span></span> <span data-ttu-id="025b9-165">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="025b9-165">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="025b9-166">Использовать настраиваемое расширение скриптов hello toodefine tooscale узла IIS</span><span class="sxs-lookup"><span data-stu-id="025b9-166">Use hello Custom Script Extension toodefine an IIS site tooscale</span></span>
> * <span data-ttu-id="025b9-167">Создание балансировщика нагрузки для масштабируемого набора</span><span class="sxs-lookup"><span data-stu-id="025b9-167">Create a load balancer for your scale set</span></span>
> * <span data-ttu-id="025b9-168">создавать масштабируемый набор виртуальных машин;</span><span class="sxs-lookup"><span data-stu-id="025b9-168">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="025b9-169">Увеличение или уменьшение числа hello экземпляров в наборе масштабирования</span><span class="sxs-lookup"><span data-stu-id="025b9-169">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="025b9-170">Создание правил автомасштабирования</span><span class="sxs-lookup"><span data-stu-id="025b9-170">Create autoscale rules</span></span>

<span data-ttu-id="025b9-171">Дополнительные сведения о понятиях и принципах работы виртуальных машин балансировки нагрузки передвинута Далее учебника toolearn toohello.</span><span class="sxs-lookup"><span data-stu-id="025b9-171">Advance toohello next tutorial toolearn more about load balancing concepts for virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="025b9-172">Балансировка нагрузки между виртуальными машинами</span><span class="sxs-lookup"><span data-stu-id="025b9-172">Load balance virtual machines</span></span>](tutorial-load-balancer.md)
