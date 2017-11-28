---
title: "aaaAvailability задает учебника для виртуальных машин Windows в Azure | Документы Microsoft"
description: "Дополнительные сведения о hello доступности наборов для виртуальных машин Windows в Azure."
documentationcenter: 
services: virtual-machines-windows
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 853775c5f126dd815c1933f9d71d2274a75ea661
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a><span data-ttu-id="7d761-103">Каким образом задает toouse доступности</span><span class="sxs-lookup"><span data-stu-id="7d761-103">How toouse availability sets</span></span>

<span data-ttu-id="7d761-104">В этом учебнике вы узнаете, как tooincrease hello доступность и надежность решений для виртуальной машины в Azure, используя возможность вызывать группы доступности.</span><span class="sxs-lookup"><span data-stu-id="7d761-104">In this tutorial, you will learn how tooincrease hello availability and reliability of your Virtual Machine solutions on Azure using a capability called Availability Sets.</span></span> <span data-ttu-id="7d761-105">Группы доступности убедитесь, что hello, развертываемым в Azure виртуальные машины распределены по нескольким кластерам изолированное оборудовании.</span><span class="sxs-lookup"><span data-stu-id="7d761-105">Availability sets ensure that hello VMs you deploy on Azure are distributed across multiple isolated hardware clusters.</span></span> <span data-ttu-id="7d761-106">Это гарантирует, что если происходит сбой оборудования или программного обеспечения в Azure, будут затронуты только подмножество виртуальных машин и что всего решения будет оставаться доступными и функциональными с точки зрения hello ваших клиентов, используя его.</span><span class="sxs-lookup"><span data-stu-id="7d761-106">Doing this ensures that if a hardware or software failure within Azure happens, only a sub-set of your VMs will be impacted and that your overall solution will remain available and operational from hello perspective of your customers using it.</span></span> 

<span data-ttu-id="7d761-107">Из этого руководства вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="7d761-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7d761-108">"Создать группу доступности"</span><span class="sxs-lookup"><span data-stu-id="7d761-108">Create an availability set</span></span>
> * <span data-ttu-id="7d761-109">Создание виртуальной машины в группе доступности</span><span class="sxs-lookup"><span data-stu-id="7d761-109">Create a VM in an availability set</span></span>
> * <span data-ttu-id="7d761-110">Проверка доступных размеров виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="7d761-110">Check available VM sizes</span></span>

<span data-ttu-id="7d761-111">Этот учебник требует hello Azure PowerShell модуль версии 3.6 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="7d761-111">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="7d761-112">Запустите ` Get-Module -ListAvailable AzureRM` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="7d761-112">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="7d761-113">Получить tooupgrade [установите Azure PowerShell модуль](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="7d761-113">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="availability-set-overview"></a><span data-ttu-id="7d761-114">Обзор групп доступности</span><span class="sxs-lookup"><span data-stu-id="7d761-114">Availability set overview</span></span>

<span data-ttu-id="7d761-115">Группа доступности — возможность логическое группирование, который можно использовать в Azure tooensure, изолированы друг от друга ресурсы hello виртуальных Машин, размещаемых в ней при развертывании в центре обработки данных Azure.</span><span class="sxs-lookup"><span data-stu-id="7d761-115">An Availability Set is a logical grouping capability that you can use in Azure tooensure that hello VM resources you place within it are isolated from each other when they are deployed within an Azure datacenter.</span></span> <span data-ttu-id="7d761-116">Azure гарантирует, что hello поместить в группу доступности, запустите несколько физических серверов, виртуальных машин, вычислений стойки, устройства хранения и сетевых коммутаторов.</span><span class="sxs-lookup"><span data-stu-id="7d761-116">Azure ensures that hello VMs you place within an Availability Set run across multiple physical servers, compute racks, storage units, and network switches.</span></span> <span data-ttu-id="7d761-117">Это гарантирует, что в событии hello оборудования или программного обеспечения Azure сбоя, будут затронуты только подмножество виртуальных машин и общую приложения будет работать и продолжить toobe tooyour доступны клиентам.</span><span class="sxs-lookup"><span data-stu-id="7d761-117">This ensures that in hello event of a hardware or Azure software failure, only a subset of your VMs will be impacted, and your overall application will stay up and continue toobe available tooyour customers.</span></span> <span data-ttu-id="7d761-118">С помощью групп доступности, tooleverage основных возможностей можно создать toobuild надежного облачных решений.</span><span class="sxs-lookup"><span data-stu-id="7d761-118">Using Availability Sets is an essential capability tooleverage when you want toobuild reliable cloud solutions.</span></span>

<span data-ttu-id="7d761-119">Рассмотрим стандартное решение на основе виртуальной машины, в котором может находиться 4 внешних веб-сервера и использоваться 2 внутренние виртуальные машины, содержащие базу данных.</span><span class="sxs-lookup"><span data-stu-id="7d761-119">Let’s consider a typical VM-based solution where you might have 4 front-end web servers and use 2 back-end VMs that host a database.</span></span> <span data-ttu-id="7d761-120">С помощью Azure необходимо два набора доступности toodefine перед развертыванием виртуальных машин: группа доступности одного уровня «web» hello и один набор доступности для уровня «database» hello.</span><span class="sxs-lookup"><span data-stu-id="7d761-120">With Azure, you’d want toodefine two availability sets before you deploy your VMs: one availability set for hello “web” tier and one availability set for hello “database” tier.</span></span> <span data-ttu-id="7d761-121">При создании новой виртуальной Машины, можно указать hello доступности виртуальной машины az toohello параметр «Создать», а Azure автоматически гарантирует, что hello виртуальных машин, создаваемых внутри hello доступных набор изолированы по нескольким ресурсам физического оборудования.</span><span class="sxs-lookup"><span data-stu-id="7d761-121">When you create a new VM you can then specify hello availability set as a parameter toohello az vm create command, and Azure will automatically ensure that hello VMs you create within hello available set are isolated across multiple physical hardware resources.</span></span> <span data-ttu-id="7d761-122">Это означает, что если hello физическое оборудование, на котором один из веб-сервер или ВМ сервера базы данных выполняется на проблемы, вы знаете, hello другие экземпляры веб-сервера и базы данных виртуальных машин сможет продолжить работу нормально, так как они находятся на другое оборудование.</span><span class="sxs-lookup"><span data-stu-id="7d761-122">This means that if hello physical hardware that one of your Web Server or Database Server VMs is running on has a problem, you know that hello other instances of your Web Server and Database VMs will remain running fine because they are on different hardware.</span></span>

<span data-ttu-id="7d761-123">При необходимости toodeploy надежные решения на основе виртуальной Машины в Azure, следует всегда использовать группы доступности.</span><span class="sxs-lookup"><span data-stu-id="7d761-123">You should always use Availability Sets when you want toodeploy reliable VM based solutions within Azure.</span></span>

## <a name="create-an-availability-set"></a><span data-ttu-id="7d761-124">"Создать группу доступности"</span><span class="sxs-lookup"><span data-stu-id="7d761-124">Create an availability set</span></span>

<span data-ttu-id="7d761-125">Создать группу доступности можно с помощью командлета [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="7d761-125">You can create an availability set using [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="7d761-126">В этом примере задается количество доменах обновления и отказоустойчивости на обоих hello *2* для обеспечения доступности hello набор *myAvailabilitySet* в hello *myResourceGroupAvailability*группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7d761-126">In this example, we set both hello number of update and fault domains at *2* for hello availability set named *myAvailabilitySet* in hello *myResourceGroupAvailability* resource group.</span></span>

<span data-ttu-id="7d761-127">Создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7d761-127">Create a resource group.</span></span>

```powershell
New-AzureRmResourceGroup -Name myResourceGroupAvailability -Location EastUS
```


```powershell
New-AzureRmAvailabilitySet `
   -Location EastUS `
   -Name myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability `
   -Managed `
   -PlatformFaultDomainCount 2 `
   -PlatformUpdateDomainCount 2
```

## <a name="create-vms-inside-an-availability-set"></a><span data-ttu-id="7d761-128">Создание виртуальных машин в группе доступности</span><span class="sxs-lookup"><span data-stu-id="7d761-128">Create VMs inside an availability set</span></span>

<span data-ttu-id="7d761-129">Виртуальные машины должны toobe создается в том, что правильно распределены по оборудованию hello toomake набор доступности hello.</span><span class="sxs-lookup"><span data-stu-id="7d761-129">VMs need toobe created within hello availability set toomake sure they are correctly distributed across hello hardware.</span></span> <span data-ttu-id="7d761-130">Не удается добавить группу существующей виртуальной Машины tooan доступности после его создания.</span><span class="sxs-lookup"><span data-stu-id="7d761-130">You can't add an existing VM tooan availability set after it is created.</span></span> 

<span data-ttu-id="7d761-131">оборудование Hello в расположении делится на toomultiple домены обновления и домены отказоустойчивости.</span><span class="sxs-lookup"><span data-stu-id="7d761-131">hello hardware in a location is divided in toomultiple update domains and fault domains.</span></span> <span data-ttu-id="7d761-132">**Домен обновления** — это группа виртуальных машин и физического оборудования, можно перезагрузить в hello то же время.</span><span class="sxs-lookup"><span data-stu-id="7d761-132">An **update domain** is a group of VMs and underlying physical hardware that can be rebooted at hello same time.</span></span> <span data-ttu-id="7d761-133">Виртуальные машины в hello же **домен сбоя** совместно используют общее хранилище, а также общие выключателем источника и сети.</span><span class="sxs-lookup"><span data-stu-id="7d761-133">VMs in hello same **fault domain** share common storage as well as a common power source and network switch.</span></span> 

<span data-ttu-id="7d761-134">При создании виртуальной Машины с помощью конфигурации с помощью [New AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) укажите hello доступности с помощью hello `-AvailabilitySetId` параметр toospecify hello идентификатор набора доступности hello.</span><span class="sxs-lookup"><span data-stu-id="7d761-134">When you create a VM using configuration using [New-AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) you specify hello availability set using hello `-AvailabilitySetId` parameter toospecify hello ID of hello availability set.</span></span>

<span data-ttu-id="7d761-135">Создать 2 виртуальные машины с [New AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) в группе доступности hello.</span><span class="sxs-lookup"><span data-stu-id="7d761-135">Create 2 VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) in hello availability set.</span></span>

```powershell
$availabilitySet = Get-AzureRmAvailabilitySet `
    -ResourceGroupName myResourceGroupAvailability `
    -Name myAvailabilitySet

$cred = Get-Credential -Message "Enter a username and password for hello virtual machine."

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupAvailability `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

for ($i=1; $i -le 2; $i++)
{
   $pip = New-AzureRmPublicIpAddress `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name "mypublicdns$(Get-Random)" `
        -AllocationMethod Static `
        -IdleTimeoutInMinutes 4

   $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
        -Name myNetworkSecurityGroupRuleRDP$i `
        -Protocol Tcp `
        -Direction Inbound `
        -Priority 1000 `
        -SourceAddressPrefix * `
        -SourcePortRange * `
        -DestinationAddressPrefix * `
        -DestinationPortRange 3389 `
        -Access Allow

   $nsg = New-AzureRmNetworkSecurityGroup `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name myNetworkSecurityGroup$i `
        -SecurityRules $nsgRuleRDP

   $nic = New-AzureRmNetworkInterface `
        -Name myNic$i `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -SubnetId $vnet.Subnets[0].Id `
        -PublicIpAddressId $pip.Id `
        -NetworkSecurityGroupId $nsg.Id

   # Here is where we specify hello availability set
   $vm = New-AzureRmVMConfig `
        -VMName myVM$i `
        -VMSize Standard_D1 `
        -AvailabilitySetId $availabilitySet.Id

   $vm = Set-AzureRmVMOperatingSystem `
        -VM $vm `
        -Windows -ComputerName myVM$i `   
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
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -VM $vm
}

```

<span data-ttu-id="7d761-136">Он принимает toocreate несколько минут, а также настроить обе виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="7d761-136">It takes a few minutes toocreate and configure both VMs.</span></span> <span data-ttu-id="7d761-137">По завершении вы получите 2 виртуальные машины, распределенные по hello базового оборудования.</span><span class="sxs-lookup"><span data-stu-id="7d761-137">When finished, you will have 2 virtual machines distributed across hello underlying hardware.</span></span> 

## <a name="check-for-available-vm-sizes"></a><span data-ttu-id="7d761-138">Знакомство с доступными размерами виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="7d761-138">Check for available VM sizes</span></span> 

<span data-ttu-id="7d761-139">Можно добавить дополнительные виртуальные машины toohello доступности более поздней версии, но необходимо tooknow какие размеры виртуальных Машин доступны на оборудовании hello.</span><span class="sxs-lookup"><span data-stu-id="7d761-139">You can add more VMs toohello availability set later, but you need tooknow what VM sizes are available on hello hardware.</span></span> <span data-ttu-id="7d761-140">Используйте [Get AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) toolist все доступные размеры hello на оборудовании hello кластера для группы доступности hello.</span><span class="sxs-lookup"><span data-stu-id="7d761-140">Use [Get-AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) toolist all hello available sizes on hello hardware cluster for hello availability set.</span></span>

```powershell
Get-AzureRmVMSize `
   -AvailabilitySetName myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability  
```

## <a name="next-steps"></a><span data-ttu-id="7d761-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7d761-141">Next steps</span></span>

<span data-ttu-id="7d761-142">Из этого руководства вы узнали, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="7d761-142">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7d761-143">"Создать группу доступности"</span><span class="sxs-lookup"><span data-stu-id="7d761-143">Create an availability set</span></span>
> * <span data-ttu-id="7d761-144">Создание виртуальной машины в группе доступности</span><span class="sxs-lookup"><span data-stu-id="7d761-144">Create a VM in an availability set</span></span>
> * <span data-ttu-id="7d761-145">Проверка доступных размеров виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="7d761-145">Check available VM sizes</span></span>

<span data-ttu-id="7d761-146">Переместить следующий учебник toolearn toohello о наборы масштабирования виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="7d761-146">Advance toohello next tutorial toolearn about virtual machine scale sets.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7d761-147">Создание масштабируемого набора виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="7d761-147">Create a VM scale set</span></span>](tutorial-create-vmss.md)


