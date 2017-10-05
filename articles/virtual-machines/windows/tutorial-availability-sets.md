---
title: "Руководство по группам доступности для виртуальных машин Windows в Azure | Документация Майкрософт"
description: "Узнайте о группах доступности для виртуальных машин Windows в Azure."
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
ms.openlocfilehash: d918362106ef93cf47620e0018d363cd510884b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-availability-sets"></a><span data-ttu-id="af53e-103">Использование групп доступности</span><span class="sxs-lookup"><span data-stu-id="af53e-103">How to use availability sets</span></span>

<span data-ttu-id="af53e-104">В этом руководстве вы узнаете, как повысить доступность и надежность решений виртуальных машин в Azure с помощью групп доступности.</span><span class="sxs-lookup"><span data-stu-id="af53e-104">In this tutorial, you will learn how to increase the availability and reliability of your Virtual Machine solutions on Azure using a capability called Availability Sets.</span></span> <span data-ttu-id="af53e-105">При развертывании виртуальных машин в Azure группа доступности распределяет их между несколькими изолированными аппаратными кластерами.</span><span class="sxs-lookup"><span data-stu-id="af53e-105">Availability sets ensure that the VMs you deploy on Azure are distributed across multiple isolated hardware clusters.</span></span> <span data-ttu-id="af53e-106">Таким образом, в случае сбоя оборудования или программного обеспечения в Azure будет затронуто только подмножество виртуальных машин, а общее решение останется доступным для использования (с точки зрения использующих его клиентов).</span><span class="sxs-lookup"><span data-stu-id="af53e-106">Doing this ensures that if a hardware or software failure within Azure happens, only a sub-set of your VMs will be impacted and that your overall solution will remain available and operational from the perspective of your customers using it.</span></span> 

<span data-ttu-id="af53e-107">Из этого руководства вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="af53e-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="af53e-108">"Создать группу доступности"</span><span class="sxs-lookup"><span data-stu-id="af53e-108">Create an availability set</span></span>
> * <span data-ttu-id="af53e-109">Создание виртуальной машины в группе доступности</span><span class="sxs-lookup"><span data-stu-id="af53e-109">Create a VM in an availability set</span></span>
> * <span data-ttu-id="af53e-110">Проверка доступных размеров виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="af53e-110">Check available VM sizes</span></span>

<span data-ttu-id="af53e-111">Для работы с этим руководством требуется модуль Azure PowerShell версии не ниже 3.6.</span><span class="sxs-lookup"><span data-stu-id="af53e-111">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="af53e-112">Чтобы узнать версию, выполните команду ` Get-Module -ListAvailable AzureRM`.</span><span class="sxs-lookup"><span data-stu-id="af53e-112">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="af53e-113">Если вам необходимо выполнить обновление, ознакомьтесь со статьей, посвященной [установке модуля Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="af53e-113">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="availability-set-overview"></a><span data-ttu-id="af53e-114">Обзор групп доступности</span><span class="sxs-lookup"><span data-stu-id="af53e-114">Availability set overview</span></span>

<span data-ttu-id="af53e-115">Группа доступности — это логическая группа функций, которые можно использовать в Azure, чтобы гарантировать изоляцию ресурсов виртуальной машины во время развертывания в центре обработки данных Azure.</span><span class="sxs-lookup"><span data-stu-id="af53e-115">An Availability Set is a logical grouping capability that you can use in Azure to ensure that the VM resources you place within it are isolated from each other when they are deployed within an Azure datacenter.</span></span> <span data-ttu-id="af53e-116">Azure гарантирует, что виртуальные машины, размещенные в группе доступности, выполняются на нескольких физических серверах, в вычислительных стойках, в пределах единиц хранения и сетевых коммутаторов.</span><span class="sxs-lookup"><span data-stu-id="af53e-116">Azure ensures that the VMs you place within an Availability Set run across multiple physical servers, compute racks, storage units, and network switches.</span></span> <span data-ttu-id="af53e-117">Таким образом, в случае сбоя оборудования или программного обеспечения в Azure будет затронуто только подмножество виртуальных машин, а приложение продолжит работать и останется доступным для клиентов.</span><span class="sxs-lookup"><span data-stu-id="af53e-117">This ensures that in the event of a hardware or Azure software failure, only a subset of your VMs will be impacted, and your overall application will stay up and continue to be available to your customers.</span></span> <span data-ttu-id="af53e-118">Группы доступности — это важный элемент при создании надежных облачных решений.</span><span class="sxs-lookup"><span data-stu-id="af53e-118">Using Availability Sets is an essential capability to leverage when you want to build reliable cloud solutions.</span></span>

<span data-ttu-id="af53e-119">Рассмотрим стандартное решение на основе виртуальной машины, в котором может находиться 4 внешних веб-сервера и использоваться 2 внутренние виртуальные машины, содержащие базу данных.</span><span class="sxs-lookup"><span data-stu-id="af53e-119">Let’s consider a typical VM-based solution where you might have 4 front-end web servers and use 2 back-end VMs that host a database.</span></span> <span data-ttu-id="af53e-120">С помощью Azure вы можете определить 2 группы доступности перед развертыванием виртуальных машин: группу доступности для веб-уровня и группу доступности для уровня базы данных.</span><span class="sxs-lookup"><span data-stu-id="af53e-120">With Azure, you’d want to define two availability sets before you deploy your VMs: one availability set for the “web” tier and one availability set for the “database” tier.</span></span> <span data-ttu-id="af53e-121">Затем при создании виртуальной машины можно указать группу доступности в качестве параметра для команды az vm create. Azure автоматически изолирует виртуальные машины, созданные в группе доступности, в нескольких ресурсах физического оборудования.</span><span class="sxs-lookup"><span data-stu-id="af53e-121">When you create a new VM you can then specify the availability set as a parameter to the az vm create command, and Azure will automatically ensure that the VMs you create within the available set are isolated across multiple physical hardware resources.</span></span> <span data-ttu-id="af53e-122">Это означает, что если возникла проблема с физическим оборудованием, на котором запущены виртуальные машины сервера базы данных или веб-сервера, то другие экземпляры этих виртуальных машин будут по-прежнему нормально работать, так как они используют другое оборудование.</span><span class="sxs-lookup"><span data-stu-id="af53e-122">This means that if the physical hardware that one of your Web Server or Database Server VMs is running on has a problem, you know that the other instances of your Web Server and Database VMs will remain running fine because they are on different hardware.</span></span>

<span data-ttu-id="af53e-123">Если требуется развернуть надежные решения на основе виртуальной машины в Azure, следует всегда использовать группы доступности.</span><span class="sxs-lookup"><span data-stu-id="af53e-123">You should always use Availability Sets when you want to deploy reliable VM based solutions within Azure.</span></span>

## <a name="create-an-availability-set"></a><span data-ttu-id="af53e-124">"Создать группу доступности"</span><span class="sxs-lookup"><span data-stu-id="af53e-124">Create an availability set</span></span>

<span data-ttu-id="af53e-125">Создать группу доступности можно с помощью командлета [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="af53e-125">You can create an availability set using [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="af53e-126">В этом примере мы задали число доменов обновления и сбоя равным *2* для группы доступности *myAvailabilitySet* в группе ресурсов *myResourceGroupAvailability*.</span><span class="sxs-lookup"><span data-stu-id="af53e-126">In this example, we set both the number of update and fault domains at *2* for the availability set named *myAvailabilitySet* in the *myResourceGroupAvailability* resource group.</span></span>

<span data-ttu-id="af53e-127">Создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="af53e-127">Create a resource group.</span></span>

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

## <a name="create-vms-inside-an-availability-set"></a><span data-ttu-id="af53e-128">Создание виртуальных машин в группе доступности</span><span class="sxs-lookup"><span data-stu-id="af53e-128">Create VMs inside an availability set</span></span>

<span data-ttu-id="af53e-129">Чтобы виртуальные машины правильно распределялись по оборудованию, их нужно создать внутри группы доступности.</span><span class="sxs-lookup"><span data-stu-id="af53e-129">VMs need to be created within the availability set to make sure they are correctly distributed across the hardware.</span></span> <span data-ttu-id="af53e-130">Существующую виртуальную машину невозможно добавить в группу доступности после создания.</span><span class="sxs-lookup"><span data-stu-id="af53e-130">You can't add an existing VM to an availability set after it is created.</span></span> 

<span data-ttu-id="af53e-131">Оборудование в расположении делится на несколько доменов обновления и доменов сбоя.</span><span class="sxs-lookup"><span data-stu-id="af53e-131">The hardware in a location is divided in to multiple update domains and fault domains.</span></span> <span data-ttu-id="af53e-132">**Домен обновления** — это группа виртуальных машин и базового физического оборудования, которую можно перезагрузить одновременно.</span><span class="sxs-lookup"><span data-stu-id="af53e-132">An **update domain** is a group of VMs and underlying physical hardware that can be rebooted at the same time.</span></span> <span data-ttu-id="af53e-133">Виртуальные машины в одном **домене сбоя** совместно используют общее хранилище, а также общий источник питания и сетевой коммутатор.</span><span class="sxs-lookup"><span data-stu-id="af53e-133">VMs in the same **fault domain** share common storage as well as a common power source and network switch.</span></span> 

<span data-ttu-id="af53e-134">При создании виртуальной машины с указанием конфигурации с помощью командлета [New-AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) можно указать группу доступности, задав ее идентификатор в параметре `-AvailabilitySetId`.</span><span class="sxs-lookup"><span data-stu-id="af53e-134">When you create a VM using configuration using [New-AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) you specify the availability set using the `-AvailabilitySetId` parameter to specify the ID of the availability set.</span></span>

<span data-ttu-id="af53e-135">Создайте две виртуальные машины в группе доступности с помощью командлета [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="af53e-135">Create 2 VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) in the availability set.</span></span>

```powershell
$availabilitySet = Get-AzureRmAvailabilitySet `
    -ResourceGroupName myResourceGroupAvailability `
    -Name myAvailabilitySet

$cred = Get-Credential -Message "Enter a username and password for the virtual machine."

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

   # Here is where we specify the availability set
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

<span data-ttu-id="af53e-136">Создание и настройка двух виртуальных машин занимает несколько минут.</span><span class="sxs-lookup"><span data-stu-id="af53e-136">It takes a few minutes to create and configure both VMs.</span></span> <span data-ttu-id="af53e-137">По завершении у вас будут две виртуальные машины, распределенные по базовому оборудованию.</span><span class="sxs-lookup"><span data-stu-id="af53e-137">When finished, you will have 2 virtual machines distributed across the underlying hardware.</span></span> 

## <a name="check-for-available-vm-sizes"></a><span data-ttu-id="af53e-138">Знакомство с доступными размерами виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="af53e-138">Check for available VM sizes</span></span> 

<span data-ttu-id="af53e-139">Позднее вы можете добавить в группу доступности другие виртуальные машины, но следует понимать, какие размеры виртуальных машин доступны на оборудовании.</span><span class="sxs-lookup"><span data-stu-id="af53e-139">You can add more VMs to the availability set later, but you need to know what VM sizes are available on the hardware.</span></span> <span data-ttu-id="af53e-140">Выполните командлет [Get-AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) для получения списка всех доступных размеров в аппаратном кластере для группы доступности.</span><span class="sxs-lookup"><span data-stu-id="af53e-140">Use [Get-AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) to list all the available sizes on the hardware cluster for the availability set.</span></span>

```powershell
Get-AzureRmVMSize `
   -AvailabilitySetName myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability  
```

## <a name="next-steps"></a><span data-ttu-id="af53e-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="af53e-141">Next steps</span></span>

<span data-ttu-id="af53e-142">Из этого руководства вы узнали, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="af53e-142">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="af53e-143">"Создать группу доступности"</span><span class="sxs-lookup"><span data-stu-id="af53e-143">Create an availability set</span></span>
> * <span data-ttu-id="af53e-144">Создание виртуальной машины в группе доступности</span><span class="sxs-lookup"><span data-stu-id="af53e-144">Create a VM in an availability set</span></span>
> * <span data-ttu-id="af53e-145">Проверка доступных размеров виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="af53e-145">Check available VM sizes</span></span>

<span data-ttu-id="af53e-146">Перейдите к следующему руководству, чтобы узнать о масштабируемых наборах виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="af53e-146">Advance to the next tutorial to learn about virtual machine scale sets.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="af53e-147">Создание масштабируемого набора виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="af53e-147">Create a VM scale set</span></span>](tutorial-create-vmss.md)


