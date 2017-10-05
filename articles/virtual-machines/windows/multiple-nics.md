---
title: "Создание виртуальных машин Windows, использующих несколько сетевых адаптеров, и управление ими в Azure | Документация Майкрософт"
description: "Узнайте, как создать виртуальную машину Windows с несколькими сетевыми адаптерами с помощью Azure PowerShell или шаблонов Resource Manager, а также, как управлять ими."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 9bff5b6d-79ac-476b-a68f-6f8754768413
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: 3bd99a67dae41de3533d7f6e244eb7ee3ecc4049
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-a-windows-virtual-machine-that-has-multiple-nics"></a><span data-ttu-id="520f2-103">Создание виртуальной машины Windows, использующей несколько сетевых адаптеров, и управление ею</span><span class="sxs-lookup"><span data-stu-id="520f2-103">Create and manage a Windows virtual machine that has multiple NICs</span></span>
<span data-ttu-id="520f2-104">Виртуальные машины (VM) в Azure могут иметь несколько виртуальных сетевых адаптеров (NIC).</span><span class="sxs-lookup"><span data-stu-id="520f2-104">Virtual machines (VMs) in Azure can have multiple virtual network interface cards (NICs) attached to them.</span></span> <span data-ttu-id="520f2-105">Распространен сценарий, когда разные подсети используются для интерфейсных и внутренних подключений или когда для решения мониторинга либо архивации используется выделенная сеть.</span><span class="sxs-lookup"><span data-stu-id="520f2-105">A common scenario is to have different subnets for front-end and back-end connectivity, or a network dedicated to a monitoring or backup solution.</span></span> <span data-ttu-id="520f2-106">В этой статье подробно описывается, как создать виртуальную машину с несколькими сетевыми адаптерами.</span><span class="sxs-lookup"><span data-stu-id="520f2-106">This article details how to create a VM that has multiple NICs attached to it.</span></span> <span data-ttu-id="520f2-107">Вы также узнаете, как добавить или удалить сетевые адаптеры на существующей виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="520f2-107">You also learn how to add or remove NICs from an existing VM.</span></span> <span data-ttu-id="520f2-108">Различные [размеры виртуальных машин](sizes.md) поддерживают разное число сетевых карт, так что выбирайте соответствующий размер виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="520f2-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="520f2-109">Различные дополнительные сведения, а также сведения о том, как создать несколько сетевых адаптеров в собственных сценариях PowerShell, см. в статье [Создание виртуальной машины с несколькими сетевыми интерфейсами с помощью PowerShell](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="520f2-109">For detailed information, including how to create multiple NICs within your own PowerShell scripts, see [deploying multiple-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="520f2-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="520f2-110">Prerequisites</span></span>
<span data-ttu-id="520f2-111">Убедитесь, что у вас установлена и настроена [последняя версия Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="520f2-111">Make sure that you have the [latest Azure PowerShell version installed and configured](/powershell/azure/overview).</span></span>

<span data-ttu-id="520f2-112">В следующих примерах замените имена параметров собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="520f2-112">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="520f2-113">Примеры имен параметров: *myResourceGroup*, *myVnet* и *myVM*.</span><span class="sxs-lookup"><span data-stu-id="520f2-113">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>


## <a name="create-a-vm-with-multiple-nics"></a><span data-ttu-id="520f2-114">Создание виртуальной машины с несколькими сетевыми адаптерами</span><span class="sxs-lookup"><span data-stu-id="520f2-114">Create a VM with multiple NICs</span></span>
<span data-ttu-id="520f2-115">Сначала создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="520f2-115">First, create a resource group.</span></span> <span data-ttu-id="520f2-116">В следующем примере создается группа ресурсов с именем *myResourceGroup* в расположении *EastUs*:</span><span class="sxs-lookup"><span data-stu-id="520f2-116">The following example creates a resource group named *myResourceGroup* in the *EastUs* location:</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "EastUS"
```

### <a name="create-virtual-network-and-subnets"></a><span data-ttu-id="520f2-117">Создание виртуальных сетей и подсетей</span><span class="sxs-lookup"><span data-stu-id="520f2-117">Create virtual network and subnets</span></span>
<span data-ttu-id="520f2-118">Общий сценарий для виртуальной сети с двумя или большим количеством подсетей.</span><span class="sxs-lookup"><span data-stu-id="520f2-118">A common scenario is for a virtual network to have two or more subnets.</span></span> <span data-ttu-id="520f2-119">Одна подсеть может предназначаться для интерфейсного трафика, а другая — для внутреннего.</span><span class="sxs-lookup"><span data-stu-id="520f2-119">One subnet may be for front-end traffic, the other for back-end traffic.</span></span> <span data-ttu-id="520f2-120">Чтобы подключиться к двум подсетям, вам необходимо будет использовать несколько сетевых адаптеров на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="520f2-120">To connect to both subnets, you then use multiple NICs on your VM.</span></span>

1. <span data-ttu-id="520f2-121">Определите две подсети виртуальной сети с помощью [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="520f2-121">Define two virtual network subnets with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="520f2-122">В следующем примере определяются подсети для *mySubnetFrontEnd* и *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="520f2-122">The following example defines the subnets for *mySubnetFrontEnd* and *mySubnetBackEnd*:</span></span>

    ```powershell
    $mySubnetFrontEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetFrontEnd" `
        -AddressPrefix "192.168.1.0/24"
    $mySubnetBackEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetBackEnd" `
        -AddressPrefix "192.168.2.0/24"
    ```

2. <span data-ttu-id="520f2-123">Создайте виртуальную сеть и подсети с помощью командлета [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="520f2-123">Create your virtual network and subnets with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="520f2-124">В следующем примере создается виртуальная сеть с именем *myVnet*:</span><span class="sxs-lookup"><span data-stu-id="520f2-124">The following example creates a virtual network named *myVnet*:</span></span>

    ```powershell
    $myVnet = New-AzureRmVirtualNetwork -ResourceGroupName "myResourceGroup" `
        -Location "EastUs" `
        -Name "myVnet" `
        -AddressPrefix "192.168.0.0/16" `
        -Subnet $mySubnetFrontEnd,$mySubnetBackEnd
    ```


### <a name="create-multiple-nics"></a><span data-ttu-id="520f2-125">Создание нескольких сетевых карт</span><span class="sxs-lookup"><span data-stu-id="520f2-125">Create multiple NICs</span></span>
<span data-ttu-id="520f2-126">Создайте два сетевых адаптера с помощью командлета [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="520f2-126">Create two NICs with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="520f2-127">Подключите один сетевой адаптер к интерфейсной подсети, а другой — к внутренней.</span><span class="sxs-lookup"><span data-stu-id="520f2-127">Attach one NIC to the front-end subnet and one NIC to the back-end subnet.</span></span> <span data-ttu-id="520f2-128">В следующем примере создаются два сетевых адаптера с именами *myNic1* и *myNic2*:</span><span class="sxs-lookup"><span data-stu-id="520f2-128">The following example creates NICs named *myNic1* and *myNic2*:</span></span>

```powershell
$frontEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetFrontEnd'}
$myNic1 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic1" `
    -Location "EastUs" `
    -SubnetId $frontEnd.Id

$backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}
$myNic2 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic2" `
    -Location "EastUs" `
    -SubnetId $backEnd.Id
```

<span data-ttu-id="520f2-129">Обычно также создается [группа безопасности сети](../../virtual-network/virtual-networks-nsg.md) или [балансировщик нагрузки](../../load-balancer/load-balancer-overview.md) для управления трафиком и его распределения между виртуальными машинами.</span><span class="sxs-lookup"><span data-stu-id="520f2-129">Typically you also create a [network security group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) to help manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="520f2-130">Дополнительные сведения о создании группы безопасности сети и назначении сетевых адаптеров см. в статье [Создание виртуальной машины с несколькими сетевыми интерфейсами с помощью PowerShell](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="520f2-130">The [more detailed multiple-NIC VM](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) article guides you through creating a network security group and assigning NICs.</span></span>

### <a name="create-the-virtual-machine"></a><span data-ttu-id="520f2-131">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="520f2-131">Create the virtual machine</span></span>
<span data-ttu-id="520f2-132">Теперь начните создание конфигурации виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="520f2-132">Now start to build your VM configuration.</span></span> <span data-ttu-id="520f2-133">Для каждого размера виртуальной машины существует ограничение на общее количество сетевых карт, которые можно в нее добавить.</span><span class="sxs-lookup"><span data-stu-id="520f2-133">Each VM size has a limit for the total number of NICs that you can add to a VM.</span></span> <span data-ttu-id="520f2-134">Дополнительные сведения см. в статье [Размеры виртуальных машин Windows в Azure](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="520f2-134">For more information, see [Windows VM sizes](sizes.md).</span></span>

1. <span data-ttu-id="520f2-135">Задайте переменной `$cred` учетные данные виртуальной машины, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="520f2-135">Set your VM credentials to the `$cred` variable as follows:</span></span>

    ```powershell
    $cred = Get-Credential
    ```

2. <span data-ttu-id="520f2-136">Определите виртуальную машину с помощью [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig).</span><span class="sxs-lookup"><span data-stu-id="520f2-136">Define your VM with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig).</span></span> <span data-ttu-id="520f2-137">В следующем примере определяется виртуальная машина с именем *myVM* и используется размер виртуальной машины, поддерживающий более двух сетевых адаптеров (*Standard_DS3_v2*):</span><span class="sxs-lookup"><span data-stu-id="520f2-137">The following example defines a VM named *myVM* and uses a VM size that supports more than two NICs (*Standard_DS3_v2*):</span></span>

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS3_v2"
    ```

3. <span data-ttu-id="520f2-138">Создайте оставшуюся часть конфигурации виртуальной машины с помощью [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) и [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage).</span><span class="sxs-lookup"><span data-stu-id="520f2-138">Create the rest of your VM configuration with [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) and [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage).</span></span> <span data-ttu-id="520f2-139">В следующем примере создается виртуальная машина Windows Server 2016:</span><span class="sxs-lookup"><span data-stu-id="520f2-139">The following example creates a Windows Server 2016 VM:</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig `
        -Windows `
        -ComputerName "myVM" `
        -Credential $cred `
        -ProvisionVMAgent `
        -EnableAutoUpdate
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig `
        -PublisherName "MicrosoftWindowsServer" `
        -Offer "WindowsServer" `
        -Skus "2016-Datacenter" `
        -Version "latest"
   ```

4. <span data-ttu-id="520f2-140">Подключите два созданных ранее сетевых адаптера с помощью [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="520f2-140">Attach the two NICs that you previously created with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic2.Id
    ```

5. <span data-ttu-id="520f2-141">Наконец, создайте виртуальную машину с помощью [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="520f2-141">Finally, create your VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):</span></span>

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName "myResourceGroup" -Location "EastUs"
    ```

## <a name="add-a-nic-to-an-existing-vm"></a><span data-ttu-id="520f2-142">Добавление сетевой карты в существующую виртуальную машину</span><span class="sxs-lookup"><span data-stu-id="520f2-142">Add a NIC to an existing VM</span></span>
<span data-ttu-id="520f2-143">Чтобы добавить виртуальный сетевой адаптер в имеющуюся виртуальную машину, освободите ее, добавьте виртуальный сетевой адаптер, а затем запустите виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="520f2-143">To add a virtual NIC to an existing VM, you deallocate the VM, add the virtual NIC, then start the VM.</span></span>

1. <span data-ttu-id="520f2-144">Освободите виртуальную машину с помощью командлета [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="520f2-144">Deallocate the VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="520f2-145">В следующем примере освобождается виртуальная машина с именем *myVM* в группе ресурсов *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="520f2-145">The following example deallocates the VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="520f2-146">Получите имеющуюся конфигурацию виртуальной машины с помощью командлета [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="520f2-146">Get the existing configuration of the VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="520f2-147">В следующем примере возвращаются сведения для виртуальной машины с именем *myVM* в *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="520f2-147">The following example gets information for the VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="520f2-148">В следующем примере создается виртуальный сетевой адаптер с помощью [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) с именем *myNic3*, подключенный к *mySubnetBackEnd*.</span><span class="sxs-lookup"><span data-stu-id="520f2-148">The following example creates a virtual NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) named *myNic3* that is attached to *mySubnetBackEnd*.</span></span> <span data-ttu-id="520f2-149">Затем с помощью [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) он подключается к виртуальной машине с именем *myVM* в *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="520f2-149">The virtual NIC is then attached to the VM named *myVM* in *myResourceGroup* with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

    ```powershell
    # Get info for the back end subnet
    $myVnet = Get-AzureRmVirtualNetwork -Name "myVnet" -ResourceGroupName "myResourceGroup"
    $backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}

    # Create a virtual NIC
    $myNic3 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
        -Name "myNic3" `
        -Location "EastUs" `
        -SubnetId $backEnd.Id

    # Get the ID of the new virtual NIC and add to VM
    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "MyNic3").Id
    Add-AzureRmVMNetworkInterface -VM $vm -Id $nicId | Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```

    ### <a name="primary-virtual-nics"></a><span data-ttu-id="520f2-150">Главные виртуальные сетевые карты</span><span class="sxs-lookup"><span data-stu-id="520f2-150">Primary virtual NICs</span></span>
    <span data-ttu-id="520f2-151">Один из сетевых адаптеров на виртуальной машине с несколькими сетевыми картами должен быть главным.</span><span class="sxs-lookup"><span data-stu-id="520f2-151">One of the NICs on a multi-NIC VM needs to be primary.</span></span> <span data-ttu-id="520f2-152">Если один из имеющихся виртуальных сетевых адаптеров на виртуальной машине уже используется в качестве главного, вы можете пропустить этот шаг.</span><span class="sxs-lookup"><span data-stu-id="520f2-152">If one of the existing virtual NICs on the VM is already set as primary, you can skip this step.</span></span> <span data-ttu-id="520f2-153">Чтобы перейти к следующему примеру, предполагается, что на виртуальной машине используются два виртуальных сетевых адаптера. Добавим первый сетевой адаптер (`[0]`) в качестве главного:</span><span class="sxs-lookup"><span data-stu-id="520f2-153">The following example assumes that two virtual NICs are now present on a VM and you wish to add the first NIC (`[0]`) as the primary:</span></span>
        
    ```powershell
    # List existing NICs on the VM and find which one is primary
    $vm.NetworkProfile.NetworkInterfaces
    
    # Set NIC 0 to be primary
    $vm.NetworkProfile.NetworkInterfaces[0].Primary = $true
    $vm.NetworkProfile.NetworkInterfaces[1].Primary = $false
    
    # Update the VM state in Azure
    Update-AzureRmVM -VM $vm -ResourceGroupName "myResourceGroup"
    ```

4. <span data-ttu-id="520f2-154">Запустите виртуальную машину с помощью [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="520f2-154">Start the VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

## <a name="remove-a-nic-from-an-existing-vm"></a><span data-ttu-id="520f2-155">Удаление сетевой карты из существующей виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="520f2-155">Remove a NIC from an existing VM</span></span>
<span data-ttu-id="520f2-156">Чтобы удалить виртуальный сетевой адаптер с имеющейся виртуальной машины, освободите ее, удалите виртуальный сетевой адаптер, а затем запустите виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="520f2-156">To remove a virtual NIC from an existing VM, you deallocate the VM, remove the virtual NIC, then start the VM.</span></span>

1. <span data-ttu-id="520f2-157">Освободите виртуальную машину с помощью командлета [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="520f2-157">Deallocate the VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="520f2-158">В следующем примере освобождается виртуальная машина с именем *myVM* в группе ресурсов *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="520f2-158">The following example deallocates the VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="520f2-159">Получите имеющуюся конфигурацию виртуальной машины с помощью командлета [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="520f2-159">Get the existing configuration of the VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="520f2-160">В следующем примере возвращаются сведения для виртуальной машины с именем *myVM* в *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="520f2-160">The following example gets information for the VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="520f2-161">С помощью [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface) получите сведения об удалении сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="520f2-161">Get information about the NIC remove with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface).</span></span> <span data-ttu-id="520f2-162">В следующем примере возвращаются сведения о *myNic3*:</span><span class="sxs-lookup"><span data-stu-id="520f2-162">The following example gets information about *myNic3*:</span></span>

    ```powershell
    # List existing NICs on the VM if you need to determine NIC name
    $vm.NetworkProfile.NetworkInterfaces

    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "myNic3").Id   
    ```

4. <span data-ttu-id="520f2-163">Удалите сетевой адаптер с помощью [Remove-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface), а затем обновите виртуальную машину с помощью [Update-AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="520f2-163">Remove the NIC with [Remove-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) and then update the VM with [Update-AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm).</span></span> <span data-ttu-id="520f2-164">В следующем примере удаляется сетевой адаптер *myNic3*, полученный `$nicId` на предыдущем шаге:</span><span class="sxs-lookup"><span data-stu-id="520f2-164">The following example removes *myNic3* as obtained by `$nicId` in the preceding step:</span></span>

    ```powershell
    Remove-AzureRmVMNetworkInterface -VM $vm -NetworkInterfaceIDs $nicId | `
        Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```   

5. <span data-ttu-id="520f2-165">Запустите виртуальную машину с помощью [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="520f2-165">Start the VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```   

## <a name="create-multiple-nics-with-templates"></a><span data-ttu-id="520f2-166">Создание нескольких сетевых адаптеров с помощью шаблонов</span><span class="sxs-lookup"><span data-stu-id="520f2-166">Create multiple NICs with templates</span></span>
<span data-ttu-id="520f2-167">Шаблоны Azure Resource Manager дают возможность создать несколько экземпляров ресурса во время развертывания, в том числе создать несколько сетевых адаптеров.</span><span class="sxs-lookup"><span data-stu-id="520f2-167">Azure Resource Manager templates provide a way to create multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="520f2-168">В шаблонах Azure Resource Manager используются декларативные JSON-файлы для определения среды.</span><span class="sxs-lookup"><span data-stu-id="520f2-168">Resource Manager templates use declarative JSON files to define your environment.</span></span> <span data-ttu-id="520f2-169">Дополнительные сведения см. в статье [Общие сведения о диспетчере ресурсов Azure](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="520f2-169">For more information, see [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="520f2-170">Чтобы указать число создаваемых экземпляров, вы можете использовать объект *copy*:</span><span class="sxs-lookup"><span data-stu-id="520f2-170">You can use *copy* to specify the number of instances to create:</span></span>

```json
"copy": {
    "name": "multiplenics",
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="520f2-171">Дополнительные сведения см. в статье [Развертывание нескольких экземпляров ресурса или свойства в шаблонах Azure Resource Manager*копирования*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="520f2-171">For more information, see [creating multiple instances by using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="520f2-172">Вы также можете использовать `copyIndex()`, чтобы добавить номер к имени ресурса.</span><span class="sxs-lookup"><span data-stu-id="520f2-172">You can also use `copyIndex()` to append a number to a resource name.</span></span> <span data-ttu-id="520f2-173">Затем вы можете создать сетевые адаптеры с именами *myNic1*, *MyNic2* и т. д.</span><span class="sxs-lookup"><span data-stu-id="520f2-173">You can then create *myNic1*, *MyNic2* and so on.</span></span> <span data-ttu-id="520f2-174">Ниже показан пример добавления значения индекса.</span><span class="sxs-lookup"><span data-stu-id="520f2-174">The following code shows an example of appending the index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="520f2-175">Вы можете ознакомиться с полным примером [создания нескольких сетевых адаптеров с помощью шаблонов Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="520f2-175">You can read a complete example of [creating multiple NICs by using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="520f2-176">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="520f2-176">Next steps</span></span>
<span data-ttu-id="520f2-177">При создании виртуальной машины с несколькими сетевыми адаптерами ознакомьтесь со статьей [Размеры виртуальных машин Windows в Azure](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="520f2-177">Review [Windows VM sizes](sizes.md) when you're trying to create a VM that has multiple NICs.</span></span> <span data-ttu-id="520f2-178">Обратите внимание на максимальное число сетевых адаптеров, поддерживаемых каждым из размеров виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="520f2-178">Pay attention to the maximum number of NICs that each VM size supports.</span></span> 


