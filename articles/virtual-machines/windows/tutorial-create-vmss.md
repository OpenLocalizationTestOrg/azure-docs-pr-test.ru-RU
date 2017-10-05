---
title: "Создание масштабируемых наборов виртуальных машин для Windows в Azure | Документация Майкрософт"
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
ms.openlocfilehash: 6600d3b401495f6c291249935b16bcc36c9b8f4b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-windows"></a><span data-ttu-id="b8556-103">Создание масштабируемого набора виртуальных машин и развертывание высокодоступного приложения в Windows</span><span class="sxs-lookup"><span data-stu-id="b8556-103">Create a Virtual Machine Scale Set and deploy a highly available app on Windows</span></span>
<span data-ttu-id="b8556-104">Масштабируемый набор виртуальных машин обеспечивает развертывание и администрирование набора идентичных автомасштабируемых виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="b8556-104">A virtual machine scale set allows you to deploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="b8556-105">Можно вручную изменить число виртуальных машин в масштабируемом наборе или определить правила для автоматического масштабирования на основе использования ЦП, объема памяти или сетевого трафика.</span><span class="sxs-lookup"><span data-stu-id="b8556-105">You can scale the number of VMs in the scale set manually, or define rules to autoscale based on CPU usage, memory demand, or network traffic.</span></span> <span data-ttu-id="b8556-106">В рамках этого руководства вы развернете масштабируемый набор виртуальных машин в Azure.</span><span class="sxs-lookup"><span data-stu-id="b8556-106">In this tutorial, you deploy a virtual machine scale set in Azure.</span></span> <span data-ttu-id="b8556-107">Вы узнаете, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="b8556-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b8556-108">Использование расширения пользовательских скриптов для определения масштабируемого сайта IIS</span><span class="sxs-lookup"><span data-stu-id="b8556-108">Use the Custom Script Extension to define an IIS site to scale</span></span>
> * <span data-ttu-id="b8556-109">Создание балансировщика нагрузки для масштабируемого набора</span><span class="sxs-lookup"><span data-stu-id="b8556-109">Create a load balancer for your scale set</span></span>
> * <span data-ttu-id="b8556-110">Создание масштабируемого набора виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="b8556-110">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="b8556-111">Увеличение или уменьшение количества экземпляров в масштабируемом наборе</span><span class="sxs-lookup"><span data-stu-id="b8556-111">Increase or decrease the number of instances in a scale set</span></span>
> * <span data-ttu-id="b8556-112">Создание правил автомасштабирования</span><span class="sxs-lookup"><span data-stu-id="b8556-112">Create autoscale rules</span></span>

<span data-ttu-id="b8556-113">Для работы с этим руководством требуется модуль Azure PowerShell версии не ниже 3.6.</span><span class="sxs-lookup"><span data-stu-id="b8556-113">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="b8556-114">Чтобы узнать версию, выполните команду ` Get-Module -ListAvailable AzureRM`.</span><span class="sxs-lookup"><span data-stu-id="b8556-114">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="b8556-115">Если вам необходимо выполнить обновление, ознакомьтесь со статьей, посвященной [установке модуля Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="b8556-115">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="scale-set-overview"></a><span data-ttu-id="b8556-116">Обзор масштабируемого набора</span><span class="sxs-lookup"><span data-stu-id="b8556-116">Scale Set overview</span></span>
<span data-ttu-id="b8556-117">Масштабируемые наборы используют те же принципы, которые вы изучили в предыдущем руководстве по [созданию высокодоступных виртуальных машин](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="b8556-117">Scale sets use similar concepts as you learned about in the previous tutorial to [Create highly available VMs](tutorial-availability-sets.md).</span></span> <span data-ttu-id="b8556-118">Виртуальные машины в масштабируемом наборе распределяются по доменам сбоя и доменам обновления, как и виртуальные машины в группе доступности.</span><span class="sxs-lookup"><span data-stu-id="b8556-118">VMs in a scale set are distributed across fault and update domains just like VMs in an availability set.</span></span>

<span data-ttu-id="b8556-119">Виртуальные машины создаются в масштабируемом наборе по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="b8556-119">VMs are created as needed in a scale set.</span></span> <span data-ttu-id="b8556-120">Можно определить правила автомасштабирования, чтобы управлять добавлением и удалением виртуальных машин в масштабируемом наборе.</span><span class="sxs-lookup"><span data-stu-id="b8556-120">You define autoscale rules to control how and when VMs are added or removed from the scale set.</span></span> <span data-ttu-id="b8556-121">Эти правила могут активироваться на основе метрик, таких как использование ЦП, использование памяти или сетевой трафик.</span><span class="sxs-lookup"><span data-stu-id="b8556-121">These rules can trigger based on metrics such as CPU load, memory usage, or network traffic.</span></span>

<span data-ttu-id="b8556-122">При использовании образа платформы Azure масштабируемые наборы поддерживают до 1000 виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="b8556-122">Scale sets support up to 1,000 VMs when you use an Azure platform image.</span></span> <span data-ttu-id="b8556-123">Для рабочих нагрузок, требующих установки значительного числа компонентов или сложной настройки виртуальных машин, вы можете [создать образ виртуальной машины](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="b8556-123">For workloads with significant installation or VM customization requirements, you may wish to [Create a custom VM image](tutorial-custom-images.md).</span></span> <span data-ttu-id="b8556-124">При использовании пользовательского образа в масштабируемом наборе можно создать до 100 виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="b8556-124">You can create up to 100 VMs in a scale set when using a custom image.</span></span>


## <a name="create-an-app-to-scale"></a><span data-ttu-id="b8556-125">Создание приложения для масштабирования</span><span class="sxs-lookup"><span data-stu-id="b8556-125">Create an app to scale</span></span>
<span data-ttu-id="b8556-126">Прежде чем создать масштабируемый набор, выполните команду [az group create](/powershell/module/azurerm.resources/new-azurermresourcegroup) для создания группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b8556-126">Before you can create a scale set, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="b8556-127">В следующем примере создается группа ресурсов с именем *myResourceGroupAutomate* в расположении *EastUS*.</span><span class="sxs-lookup"><span data-stu-id="b8556-127">The following example creates a resource group named *myResourceGroupAutomate* in the *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupScaleSet -Location EastUS
```

<span data-ttu-id="b8556-128">В предыдущем руководстве вы узнали, как [автоматизировать настройку виртуальных машин](tutorial-automate-vm-deployment.md) с помощью расширения пользовательских сценариев.</span><span class="sxs-lookup"><span data-stu-id="b8556-128">In an earlier tutorial, you learned how to [Automate VM configuration](tutorial-automate-vm-deployment.md) using the Custom Script Extension.</span></span> <span data-ttu-id="b8556-129">Создайте конфигурацию масштабируемого набора, а затем примените расширение пользовательских сценариев, чтобы установить и настроить IIS.</span><span class="sxs-lookup"><span data-stu-id="b8556-129">Create a scale set configuration then apply a Custom Script Extension to install and configure IIS:</span></span>

```powershell
# Create a config object
$vmssConfig = New-AzureRmVmssConfig `
    -Location EastUS `
    -SkuCapacity 2 `
    -SkuName Standard_DS2 `
    -UpgradePolicyMode Automatic

# Define the script for your Custom Script Extension to run
$publicSettings = @{
    "fileUris" = (,"https://raw.githubusercontent.com/iainfoulds/azure-samples/master/automate-iis.ps1");
    "commandToExecute" = "powershell -ExecutionPolicy Unrestricted -File automate-iis.ps1"
}

# Use Custom Script Extension to install IIS and configure basic website
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig `
    -Name "customScript" `
    -Publisher "Microsoft.Compute" `
    -Type "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -Setting $publicSettings
```

## <a name="create-scale-load-balancer"></a><span data-ttu-id="b8556-130">Создание подсистемы балансировки нагрузки для масштабируемого набора</span><span class="sxs-lookup"><span data-stu-id="b8556-130">Create scale load balancer</span></span>
<span data-ttu-id="b8556-131">Azure Load Balancer представляет собой балансировщик нагрузки уровня 4 (TCP, UDP), который обеспечивает высокий уровень доступности, распределяя входящий трафик между работоспособными виртуальными машинами.</span><span class="sxs-lookup"><span data-stu-id="b8556-131">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="b8556-132">Проба работоспособности позволяет отслеживать данный порт на каждой виртуальной машине и передавать трафик только в рабочую виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="b8556-132">A load balancer health probe monitors a given port on each VM and only distributes traffic to an operational VM.</span></span> <span data-ttu-id="b8556-133">Дополнительные сведения см. в следующем руководстве, [Балансировка нагрузки виртуальных машин Windows в Azure для создания высокодоступного приложения](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="b8556-133">For more information, see the next tutorial on [How to load balance Windows virtual machines](tutorial-load-balancer.md).</span></span>

<span data-ttu-id="b8556-134">Создайте подсистему балансировки нагрузки с общедоступным IP-адресом, которая распределяет веб-трафик через порт 80.</span><span class="sxs-lookup"><span data-stu-id="b8556-134">Create a load balancer that has a public IP address and distributes web traffic on port 80:</span></span>

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

# Create the load balancer
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

# Create a load balancer rule to distribute traffic on port 80
Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80

# Update the load balancer configuration
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="create-a-scale-set"></a><span data-ttu-id="b8556-135">Создание масштабируемого набора</span><span class="sxs-lookup"><span data-stu-id="b8556-135">Create a scale set</span></span>
<span data-ttu-id="b8556-136">Теперь создайте масштабируемый набор виртуальных машин с помощью командлета [New-AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="b8556-136">Now create a virtual machine scale set with [New-AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="b8556-137">Приведенный ниже пример создает масштабируемый набор *myScaleSet*.</span><span class="sxs-lookup"><span data-stu-id="b8556-137">The following example creates a scale set named *myScaleSet*:</span></span>

```powershell
# Reference a virtual machine image from the gallery
Set-AzureRmVmssStorageProfile $vmssConfig `
  -ImageReferencePublisher MicrosoftWindowsServer `
  -ImageReferenceOffer WindowsServer `
  -ImageReferenceSku 2016-Datacenter `
  -ImageReferenceVersion latest

# Set up information for authenticating with the virtual machine
Set-AzureRmVmssOsProfile $vmssConfig `
  -AdminUsername azureuser `
  -AdminPassword P@ssword! `
  -ComputerNamePrefix myVM

# Create the virtual network resources
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

# Attach the virtual network to the config object
Add-AzureRmVmssNetworkInterfaceConfiguration `
  -VirtualMachineScaleSet $vmssConfig `
  -Name "network-config" `
  -Primary $true `
  -IPConfiguration $ipConfig

# Create the scale set with the config object (this step might take a few minutes)
New-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -Name myScaleSet `
  -VirtualMachineScaleSet $vmssConfig
```

<span data-ttu-id="b8556-138">Создание и настройка всех ресурсов и виртуальных машин масштабируемого набора занимает несколько минут.</span><span class="sxs-lookup"><span data-stu-id="b8556-138">It takes a few minutes to create and configure all the scale set resources and VMs.</span></span>


## <a name="test-your-app"></a><span data-ttu-id="b8556-139">Тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="b8556-139">Test your app</span></span>
<span data-ttu-id="b8556-140">Чтобы изучить работу веб-сайта IIS, получите общедоступный IP-адрес своей подсистемы балансировки нагрузки с помощью командлета [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="b8556-140">To see your IIS website in action, obtain the public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="b8556-141">Следующий пример получает IP-адрес элемента *myPublicIP*, созданного ранее вместе с масштабируемым набором.</span><span class="sxs-lookup"><span data-stu-id="b8556-141">The following example obtains the IP address for *myPublicIP* created as part of the scale set:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupScaleSet -Name myPublicIP | select IpAddress
```

<span data-ttu-id="b8556-142">Введите общедоступный IP-адрес в веб-браузер.</span><span class="sxs-lookup"><span data-stu-id="b8556-142">Enter the public IP address in to a web browser.</span></span> <span data-ttu-id="b8556-143">Отобразится приложение, а также имя узла виртуальной машины, на которую балансировщик нагрузки направил трафик.</span><span class="sxs-lookup"><span data-stu-id="b8556-143">The app is displayed, including the hostname of the VM that the load balancer distributed traffic to:</span></span>

![Выполнение сайта IIS](./media/tutorial-create-vmss/running-iis-site.png)

<span data-ttu-id="b8556-145">Чтобы познакомиться с работой масштабируемого набора, принудительно обновите окно веб-браузера, чтобы увидеть, как балансировщик нагрузки распределяет трафик между всеми виртуальными машинами, где выполняется приложение.</span><span class="sxs-lookup"><span data-stu-id="b8556-145">To see the scale set in action, you can force-refresh your web browser to see the load balancer distribute traffic across all the VMs running your app.</span></span>


## <a name="management-tasks"></a><span data-ttu-id="b8556-146">Задачи управления</span><span class="sxs-lookup"><span data-stu-id="b8556-146">Management tasks</span></span>
<span data-ttu-id="b8556-147">На протяжении жизненного цикла масштабируемого набора может возникнуть необходимость выполнить одну или несколько задач управления.</span><span class="sxs-lookup"><span data-stu-id="b8556-147">Throughout the lifecycle of the scale set, you may need to run one or more management tasks.</span></span> <span data-ttu-id="b8556-148">Кроме того, можно создавать сценарии для автоматизации различных задач жизненного цикла.</span><span class="sxs-lookup"><span data-stu-id="b8556-148">Additionally, you may want to create scripts that automate various lifecycle-tasks.</span></span> <span data-ttu-id="b8556-149">Azure PowerShell позволяет быстро выполнять эти задачи.</span><span class="sxs-lookup"><span data-stu-id="b8556-149">Azure PowerShell provides a quick way to do those tasks.</span></span> <span data-ttu-id="b8556-150">Ниже приведено несколько распространенных задач.</span><span class="sxs-lookup"><span data-stu-id="b8556-150">Here are a few common tasks.</span></span>

### <a name="view-vms-in-a-scale-set"></a><span data-ttu-id="b8556-151">Просмотр виртуальных машин в масштабируемом наборе</span><span class="sxs-lookup"><span data-stu-id="b8556-151">View VMs in a scale set</span></span>
<span data-ttu-id="b8556-152">Чтобы просмотреть список виртуальных машин, запущенных в масштабируемом наборе, выполните командлет [Get-AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) следующим образом.</span><span class="sxs-lookup"><span data-stu-id="b8556-152">To view a list of VMs running in your scale set, use [Get-AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) as follows:</span></span>

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Loop through the instanaces in your scale set
for ($i=1; $i -le ($scaleset.Sku.Capacity - 1); $i++) {
    Get-AzureRmVmssVM -ResourceGroupName myResourceGroupScaleSet `
      -VMScaleSetName myScaleSet `
      -InstanceId $i
}
```


### <a name="increase-or-decrease-vm-instances"></a><span data-ttu-id="b8556-153">Увеличение или уменьшение числа экземпляров виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="b8556-153">Increase or decrease VM instances</span></span>
<span data-ttu-id="b8556-154">Чтобы просмотреть количество экземпляров, присутствующих в масштабируемом наборе, выполните командлет [Get-AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) и отправьте запрос для *sku.capacity*.</span><span class="sxs-lookup"><span data-stu-id="b8556-154">To see the number of instances you currently have in a scale set, use [Get-AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) and query on *sku.capacity*:</span></span>

```powershell
Get-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -VMScaleSetName myScaleSet | `
    Select -ExpandProperty Sku
```

<span data-ttu-id="b8556-155">После этого можно вручную увеличить или уменьшить число виртуальных машин в масштабируемом наборе, выполнив командлет [Update-AzureRmVmss](/powershell/module/azurerm.compute/update-azurermvmss).</span><span class="sxs-lookup"><span data-stu-id="b8556-155">You can then manually increase or decrease the number of virtual machines in the scale set with [Update-AzureRmVmss](/powershell/module/azurerm.compute/update-azurermvmss).</span></span> <span data-ttu-id="b8556-156">Приведенный ниже пример задает число виртуальных машин в масштабируемом наборе, равное *5*.</span><span class="sxs-lookup"><span data-stu-id="b8556-156">The following example sets the number of VMs in your scale set to *5*:</span></span>

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Set and update the capacity of your scale set
$scaleset.sku.capacity = 5
Update-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -Name myScaleSet `
    -VirtualMachineScaleSet $scaleset
```

<span data-ttu-id="b8556-157">Обновление числа экземпляров в масштабируемом наборе занимает несколько минут.</span><span class="sxs-lookup"><span data-stu-id="b8556-157">If takes a few minutes to update the specified number of instances in your scale set.</span></span>


### <a name="configure-autoscale-rules"></a><span data-ttu-id="b8556-158">Настройка правил автомасштабирования</span><span class="sxs-lookup"><span data-stu-id="b8556-158">Configure autoscale rules</span></span>
<span data-ttu-id="b8556-159">Вместо установки числа экземпляров в масштабируемом наборе вручную можно определить правила автомасштабирования.</span><span class="sxs-lookup"><span data-stu-id="b8556-159">Rather than manually scaling the number of instances in your scale set, you define autoscale rules.</span></span> <span data-ttu-id="b8556-160">С помощью правил среда отслеживает экземпляры в масштабируемом наборе и реагирует соответствующим образом на основе определенных метрик и пороговых значений.</span><span class="sxs-lookup"><span data-stu-id="b8556-160">These rules monitor the instances in your scale set and respond accordingly based on metrics and thresholds you define.</span></span> <span data-ttu-id="b8556-161">Приведенный ниже пример увеличивает число экземпляров на один, когда средняя загрузка ЦП превышает 60 % в течение 5 минут.</span><span class="sxs-lookup"><span data-stu-id="b8556-161">The following example scales out the number of instances by one when the average CPU load is greater than 60% over a 5 minute period.</span></span> <span data-ttu-id="b8556-162">Если затем средняя загрузка ЦП не превышает 30 % в течение 5 минут, то число экземпляров уменьшается на один.</span><span class="sxs-lookup"><span data-stu-id="b8556-162">If the average CPU load then drops below 30% over a 5 minute period, the instances are scaled in by one instance:</span></span>

```powershell
# Define your scale set information
$mySubscriptionId = (Get-AzureRmSubscription).Id
$myResourceGroup = "myResourceGroupScaleSet"
$myScaleSet = "myScaleSet"
$myLocation = "East US"

# Create a scale up rule to increase the number instances after 60% average CPU usage exceeded for a 5 minute period
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

# Create a scale down rule to decrease the number of instances after 30% average CPU usage over a 5 minute period
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

# Apply the autoscale rules
Add-AzureRmAutoscaleSetting `
  -Location $myLocation `
  -Name "autosetting" `
  -ResourceGroup $myResourceGroup `
  -TargetResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -AutoscaleProfiles $myScaleProfile
```


## <a name="next-steps"></a><span data-ttu-id="b8556-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b8556-163">Next steps</span></span>
<span data-ttu-id="b8556-164">В рамках этого руководства вы создали набор масштабирования виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="b8556-164">In this tutorial, you created a virtual machine scale set.</span></span> <span data-ttu-id="b8556-165">Вы научились выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="b8556-165">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b8556-166">Использование расширения пользовательских скриптов для определения масштабируемого сайта IIS</span><span class="sxs-lookup"><span data-stu-id="b8556-166">Use the Custom Script Extension to define an IIS site to scale</span></span>
> * <span data-ttu-id="b8556-167">Создание балансировщика нагрузки для масштабируемого набора</span><span class="sxs-lookup"><span data-stu-id="b8556-167">Create a load balancer for your scale set</span></span>
> * <span data-ttu-id="b8556-168">Создание масштабируемого набора виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="b8556-168">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="b8556-169">Увеличение или уменьшение количества экземпляров в масштабируемом наборе</span><span class="sxs-lookup"><span data-stu-id="b8556-169">Increase or decrease the number of instances in a scale set</span></span>
> * <span data-ttu-id="b8556-170">Создание правил автомасштабирования</span><span class="sxs-lookup"><span data-stu-id="b8556-170">Create autoscale rules</span></span>

<span data-ttu-id="b8556-171">Перейдите к следующему руководству, чтобы узнать о принципах балансировки нагрузки для виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="b8556-171">Advance to the next tutorial to learn more about load balancing concepts for virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b8556-172">Балансировка нагрузки между виртуальными машинами</span><span class="sxs-lookup"><span data-stu-id="b8556-172">Load balance virtual machines</span></span>](tutorial-load-balancer.md)
