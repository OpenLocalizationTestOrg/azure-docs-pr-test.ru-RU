---
title: "aaaCreate и управление виртуальными машинами Windows в Azure, использовать несколько сетевых адаптеров | Документы Microsoft"
description: "Узнайте, как toocreate и управление виртуальной Машины Windows с несколькими tooit подключенных сетевых адаптеров, используя шаблоны Azure PowerShell или диспетчер ресурсов."
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
ms.openlocfilehash: c3c7d7569aca6f047238146d84b2ffccf05d4079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-windows-virtual-machine-that-has-multiple-nics"></a><span data-ttu-id="44942-103">Создание виртуальной машины Windows, использующей несколько сетевых адаптеров, и управление ею</span><span class="sxs-lookup"><span data-stu-id="44942-103">Create and manage a Windows virtual machine that has multiple NICs</span></span>
<span data-ttu-id="44942-104">Виртуальные машины (ВМ в Azure) может иметь несколько toothem карты (NIC) присоединенного интерфейс виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="44942-104">Virtual machines (VMs) in Azure can have multiple virtual network interface cards (NICs) attached toothem.</span></span> <span data-ttu-id="44942-105">Типичный сценарий состоит в разных подсетях toohave для внешнего и внутреннего интерфейса подключения или сеть, выделенная tooa наблюдения или решение для резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="44942-105">A common scenario is toohave different subnets for front-end and back-end connectivity, or a network dedicated tooa monitoring or backup solution.</span></span> <span data-ttu-id="44942-106">В этой статье указаны как toocreate виртуальной Машины с несколькими сетевыми картами присоединенного tooit.</span><span class="sxs-lookup"><span data-stu-id="44942-106">This article details how toocreate a VM that has multiple NICs attached tooit.</span></span> <span data-ttu-id="44942-107">Вы также узнаете, как tooadd или удаление сетевых адаптеров в существующей виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="44942-107">You also learn how tooadd or remove NICs from an existing VM.</span></span> <span data-ttu-id="44942-108">Различные [размеры виртуальных машин](sizes.md) поддерживают разное число сетевых карт, так что выбирайте соответствующий размер виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="44942-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="44942-109">Дополнительные сведения, включая toocreate несколько сетевых адаптеров в собственных сценариев PowerShell см. в [развертывание виртуальных машин с несколькими сетевыми Картами](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="44942-109">For detailed information, including how toocreate multiple NICs within your own PowerShell scripts, see [deploying multiple-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44942-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="44942-110">Prerequisites</span></span>
<span data-ttu-id="44942-111">Убедитесь, что имеется hello [последнюю версию Azure PowerShell устанавливается и настраивается](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="44942-111">Make sure that you have hello [latest Azure PowerShell version installed and configured](/powershell/azure/overview).</span></span>

<span data-ttu-id="44942-112">В hello следующих примерах замените примеры имен параметров собственные значения.</span><span class="sxs-lookup"><span data-stu-id="44942-112">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="44942-113">Примеры имен параметров: *myResourceGroup*, *myVnet* и *myVM*.</span><span class="sxs-lookup"><span data-stu-id="44942-113">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>


## <a name="create-a-vm-with-multiple-nics"></a><span data-ttu-id="44942-114">Создание виртуальной машины с несколькими сетевыми адаптерами</span><span class="sxs-lookup"><span data-stu-id="44942-114">Create a VM with multiple NICs</span></span>
<span data-ttu-id="44942-115">Сначала создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="44942-115">First, create a resource group.</span></span> <span data-ttu-id="44942-116">Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *EastUs* расположение:</span><span class="sxs-lookup"><span data-stu-id="44942-116">hello following example creates a resource group named *myResourceGroup* in hello *EastUs* location:</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "EastUS"
```

### <a name="create-virtual-network-and-subnets"></a><span data-ttu-id="44942-117">Создание виртуальных сетей и подсетей</span><span class="sxs-lookup"><span data-stu-id="44942-117">Create virtual network and subnets</span></span>
<span data-ttu-id="44942-118">Распространенным сценарием является для toohave виртуальной сети двух или нескольких подсетях.</span><span class="sxs-lookup"><span data-stu-id="44942-118">A common scenario is for a virtual network toohave two or more subnets.</span></span> <span data-ttu-id="44942-119">Одна подсеть может быть трафика переднего плана, hello других для трафика серверной части.</span><span class="sxs-lookup"><span data-stu-id="44942-119">One subnet may be for front-end traffic, hello other for back-end traffic.</span></span> <span data-ttu-id="44942-120">tooconnect tooboth подсети, после этого использовать несколько сетевых адаптеров на виртуальной Машине.</span><span class="sxs-lookup"><span data-stu-id="44942-120">tooconnect tooboth subnets, you then use multiple NICs on your VM.</span></span>

1. <span data-ttu-id="44942-121">Определите две подсети виртуальной сети с помощью [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="44942-121">Define two virtual network subnets with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="44942-122">Hello следующий пример определяет hello подсетей для *mySubnetFrontEnd* и *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="44942-122">hello following example defines hello subnets for *mySubnetFrontEnd* and *mySubnetBackEnd*:</span></span>

    ```powershell
    $mySubnetFrontEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetFrontEnd" `
        -AddressPrefix "192.168.1.0/24"
    $mySubnetBackEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetBackEnd" `
        -AddressPrefix "192.168.2.0/24"
    ```

2. <span data-ttu-id="44942-123">Создайте виртуальную сеть и подсети с помощью командлета [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="44942-123">Create your virtual network and subnets with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="44942-124">Hello следующий пример создает виртуальную сеть с именем *myVnet*:</span><span class="sxs-lookup"><span data-stu-id="44942-124">hello following example creates a virtual network named *myVnet*:</span></span>

    ```powershell
    $myVnet = New-AzureRmVirtualNetwork -ResourceGroupName "myResourceGroup" `
        -Location "EastUs" `
        -Name "myVnet" `
        -AddressPrefix "192.168.0.0/16" `
        -Subnet $mySubnetFrontEnd,$mySubnetBackEnd
    ```


### <a name="create-multiple-nics"></a><span data-ttu-id="44942-125">Создание нескольких сетевых карт</span><span class="sxs-lookup"><span data-stu-id="44942-125">Create multiple NICs</span></span>
<span data-ttu-id="44942-126">Создайте два сетевых адаптера с помощью командлета [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="44942-126">Create two NICs with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="44942-127">Присоедините одну подсеть сетевого Адаптера toohello переднего плана и одной подсети внутренней toohello сетевого Адаптера.</span><span class="sxs-lookup"><span data-stu-id="44942-127">Attach one NIC toohello front-end subnet and one NIC toohello back-end subnet.</span></span> <span data-ttu-id="44942-128">Hello следующий пример создает сетевых адаптеров с именем *myNic1* и *myNic2*:</span><span class="sxs-lookup"><span data-stu-id="44942-128">hello following example creates NICs named *myNic1* and *myNic2*:</span></span>

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

<span data-ttu-id="44942-129">Обычно также создать [сетевой группы безопасности](../../virtual-network/virtual-networks-nsg.md) или [подсистемы балансировки нагрузки](../../load-balancer/load-balancer-overview.md) toohelp управлять и распределять трафик между виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="44942-129">Typically you also create a [network security group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) toohelp manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="44942-130">Hello [более подробные виртуальной Машины нескольких Сетевых](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) статье описывается создание группы безопасности сети и назначение сетевых адаптеров.</span><span class="sxs-lookup"><span data-stu-id="44942-130">hello [more detailed multiple-NIC VM](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) article guides you through creating a network security group and assigning NICs.</span></span>

### <a name="create-hello-virtual-machine"></a><span data-ttu-id="44942-131">Создание виртуальной машины hello</span><span class="sxs-lookup"><span data-stu-id="44942-131">Create hello virtual machine</span></span>
<span data-ttu-id="44942-132">Теперь запустите toobuild конфигурации своей виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="44942-132">Now start toobuild your VM configuration.</span></span> <span data-ttu-id="44942-133">Размер каждой виртуальной Машины имеет ограничение hello общее количество сетевых адаптеров, вы можете добавить tooa виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="44942-133">Each VM size has a limit for hello total number of NICs that you can add tooa VM.</span></span> <span data-ttu-id="44942-134">Дополнительные сведения см. в статье [Размеры виртуальных машин Windows в Azure](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="44942-134">For more information, see [Windows VM sizes](sizes.md).</span></span>

1. <span data-ttu-id="44942-135">Задайте учетные данные вашей виртуальной Машины toohello `$cred` переменной следующим образом:</span><span class="sxs-lookup"><span data-stu-id="44942-135">Set your VM credentials toohello `$cred` variable as follows:</span></span>

    ```powershell
    $cred = Get-Credential
    ```

2. <span data-ttu-id="44942-136">Определите виртуальную машину с помощью [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig).</span><span class="sxs-lookup"><span data-stu-id="44942-136">Define your VM with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig).</span></span> <span data-ttu-id="44942-137">Hello следующий пример определяет Виртуальную машину с именем *myVM* и использует размер виртуальной Машины, которая поддерживает более двух сетевых адаптеров (*Standard_DS3_v2*):</span><span class="sxs-lookup"><span data-stu-id="44942-137">hello following example defines a VM named *myVM* and uses a VM size that supports more than two NICs (*Standard_DS3_v2*):</span></span>

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS3_v2"
    ```

3. <span data-ttu-id="44942-138">Создание hello остальной части конфигурации своей виртуальной Машины с [набор AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) и [AzureRmVMSourceImage набор](/powershell/module/azurerm.compute/set-azurermvmsourceimage).</span><span class="sxs-lookup"><span data-stu-id="44942-138">Create hello rest of your VM configuration with [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) and [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage).</span></span> <span data-ttu-id="44942-139">Следующий пример Hello создает виртуальную Машину Windows Server 2016:</span><span class="sxs-lookup"><span data-stu-id="44942-139">hello following example creates a Windows Server 2016 VM:</span></span>

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

4. <span data-ttu-id="44942-140">Присоединение hello двух сетевых адаптеров, которые были созданы ранее с [AzureRmVMNetworkInterface добавить](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="44942-140">Attach hello two NICs that you previously created with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic2.Id
    ```

5. <span data-ttu-id="44942-141">Наконец, создайте виртуальную машину с помощью [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="44942-141">Finally, create your VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):</span></span>

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName "myResourceGroup" -Location "EastUs"
    ```

## <a name="add-a-nic-tooan-existing-vm"></a><span data-ttu-id="44942-142">Добавьте сетевой Адаптер tooan существующей виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="44942-142">Add a NIC tooan existing VM</span></span>
<span data-ttu-id="44942-143">tooadd виртуального сетевого Адаптера tooan существующих виртуальных Машин, deallocate hello виртуальной Машины, добавьте hello виртуальный сетевой Адаптер, а затем запустить hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="44942-143">tooadd a virtual NIC tooan existing VM, you deallocate hello VM, add hello virtual NIC, then start hello VM.</span></span>

1. <span data-ttu-id="44942-144">DEALLOCATE hello виртуальной Машины с [Stop AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="44942-144">Deallocate hello VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="44942-145">Hello следующий пример отменяет выделение hello виртуальной Машины с именем *myVM* в *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="44942-145">hello following example deallocates hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="44942-146">Получить конфигурацию существующего hello hello виртуальной Машины с [Get AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="44942-146">Get hello existing configuration of hello VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="44942-147">Hello следующий пример получает сведения для виртуальной Машины с именем hello *myVM* в *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="44942-147">hello following example gets information for hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="44942-148">Hello следующем примере создается виртуальный сетевой Адаптер с [New AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) с именем *myNic3* слишком присоединяется*mySubnetBackEnd*.</span><span class="sxs-lookup"><span data-stu-id="44942-148">hello following example creates a virtual NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) named *myNic3* that is attached too*mySubnetBackEnd*.</span></span> <span data-ttu-id="44942-149">Привет, виртуальный сетевой Адаптер будет подключен toohello виртуальной Машины с именем *myVM* в *myResourceGroup* с [AzureRmVMNetworkInterface добавить](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="44942-149">hello virtual NIC is then attached toohello VM named *myVM* in *myResourceGroup* with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

    ```powershell
    # Get info for hello back end subnet
    $myVnet = Get-AzureRmVirtualNetwork -Name "myVnet" -ResourceGroupName "myResourceGroup"
    $backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}

    # Create a virtual NIC
    $myNic3 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
        -Name "myNic3" `
        -Location "EastUs" `
        -SubnetId $backEnd.Id

    # Get hello ID of hello new virtual NIC and add tooVM
    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "MyNic3").Id
    Add-AzureRmVMNetworkInterface -VM $vm -Id $nicId | Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```

    ### <a name="primary-virtual-nics"></a><span data-ttu-id="44942-150">Главные виртуальные сетевые карты</span><span class="sxs-lookup"><span data-stu-id="44942-150">Primary virtual NICs</span></span>
    <span data-ttu-id="44942-151">Один из сетевых адаптеров на виртуальной Машине multi-NIC hello должен toobe первичной.</span><span class="sxs-lookup"><span data-stu-id="44942-151">One of hello NICs on a multi-NIC VM needs toobe primary.</span></span> <span data-ttu-id="44942-152">Если один из hello существующих виртуальных сетевых адаптеров на hello виртуальная машина уже задан как первичный, этот шаг можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="44942-152">If one of hello existing virtual NICs on hello VM is already set as primary, you can skip this step.</span></span> <span data-ttu-id="44942-153">Hello в примере предполагается, что два виртуальных сетевых адаптеров на виртуальной Машине теперь присутствуют и вы хотите tooadd hello первый сетевой Адаптер (`[0]`) как основной hello:</span><span class="sxs-lookup"><span data-stu-id="44942-153">hello following example assumes that two virtual NICs are now present on a VM and you wish tooadd hello first NIC (`[0]`) as hello primary:</span></span>
        
    ```powershell
    # List existing NICs on hello VM and find which one is primary
    $vm.NetworkProfile.NetworkInterfaces
    
    # Set NIC 0 toobe primary
    $vm.NetworkProfile.NetworkInterfaces[0].Primary = $true
    $vm.NetworkProfile.NetworkInterfaces[1].Primary = $false
    
    # Update hello VM state in Azure
    Update-AzureRmVM -VM $vm -ResourceGroupName "myResourceGroup"
    ```

4. <span data-ttu-id="44942-154">Запуск hello виртуальной Машины с [AzureRmVm начала](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="44942-154">Start hello VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

## <a name="remove-a-nic-from-an-existing-vm"></a><span data-ttu-id="44942-155">Удаление сетевой карты из существующей виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="44942-155">Remove a NIC from an existing VM</span></span>
<span data-ttu-id="44942-156">tooremove виртуальный сетевой Адаптер из существующей виртуальной Машины, можно освободить hello виртуальной Машины, удалите hello виртуальный сетевой Адаптер, а затем hello запуска виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="44942-156">tooremove a virtual NIC from an existing VM, you deallocate hello VM, remove hello virtual NIC, then start hello VM.</span></span>

1. <span data-ttu-id="44942-157">DEALLOCATE hello виртуальной Машины с [Stop AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="44942-157">Deallocate hello VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="44942-158">Hello следующий пример отменяет выделение hello виртуальной Машины с именем *myVM* в *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="44942-158">hello following example deallocates hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="44942-159">Получить конфигурацию существующего hello hello виртуальной Машины с [Get AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="44942-159">Get hello existing configuration of hello VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="44942-160">Hello следующий пример получает сведения для виртуальной Машины с именем hello *myVM* в *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="44942-160">hello following example gets information for hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="44942-161">Получение сведений о hello, удалите сетевой Адаптер с [Get AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="44942-161">Get information about hello NIC remove with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface).</span></span> <span data-ttu-id="44942-162">Hello следующий пример возвращает сведения *myNic3*:</span><span class="sxs-lookup"><span data-stu-id="44942-162">hello following example gets information about *myNic3*:</span></span>

    ```powershell
    # List existing NICs on hello VM if you need toodetermine NIC name
    $vm.NetworkProfile.NetworkInterfaces

    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "myNic3").Id   
    ```

4. <span data-ttu-id="44942-163">Удалите hello сетевого Адаптера с [удаление AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) и только затем hello виртуальной Машины с [AzureRmVm обновление](/powershell/module/azurerm.compute/update-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="44942-163">Remove hello NIC with [Remove-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) and then update hello VM with [Update-AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm).</span></span> <span data-ttu-id="44942-164">Hello следующий пример удаляет *myNic3* полученных `$nicId` в hello предшествующий шаг:</span><span class="sxs-lookup"><span data-stu-id="44942-164">hello following example removes *myNic3* as obtained by `$nicId` in hello preceding step:</span></span>

    ```powershell
    Remove-AzureRmVMNetworkInterface -VM $vm -NetworkInterfaceIDs $nicId | `
        Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```   

5. <span data-ttu-id="44942-165">Запуск hello виртуальной Машины с [AzureRmVm начала](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="44942-165">Start hello VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```   

## <a name="create-multiple-nics-with-templates"></a><span data-ttu-id="44942-166">Создание нескольких сетевых адаптеров с помощью шаблонов</span><span class="sxs-lookup"><span data-stu-id="44942-166">Create multiple NICs with templates</span></span>
<span data-ttu-id="44942-167">Шаблоны Azure Resource Manager предоставить несколько экземпляров ресурса toocreate образом во время развертывания, таких как создание нескольких сетевых адаптеров.</span><span class="sxs-lookup"><span data-stu-id="44942-167">Azure Resource Manager templates provide a way toocreate multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="44942-168">Шаблоны диспетчера ресурсов среду использовать декларативные toodefine файлы JSON.</span><span class="sxs-lookup"><span data-stu-id="44942-168">Resource Manager templates use declarative JSON files toodefine your environment.</span></span> <span data-ttu-id="44942-169">Дополнительные сведения см. в статье [Общие сведения о диспетчере ресурсов Azure](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="44942-169">For more information, see [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="44942-170">Можно использовать *копирования* toospecify hello число экземпляров toocreate:</span><span class="sxs-lookup"><span data-stu-id="44942-170">You can use *copy* toospecify hello number of instances toocreate:</span></span>

```json
"copy": {
    "name": "multiplenics",
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="44942-171">Дополнительные сведения см. в статье [Развертывание нескольких экземпляров ресурса или свойства в шаблонах Azure Resource Manager*копирования*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="44942-171">For more information, see [creating multiple instances by using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="44942-172">Можно также использовать `copyIndex()` tooappend номеров tooa имя ресурса.</span><span class="sxs-lookup"><span data-stu-id="44942-172">You can also use `copyIndex()` tooappend a number tooa resource name.</span></span> <span data-ttu-id="44942-173">Затем вы можете создать сетевые адаптеры с именами *myNic1*, *MyNic2* и т. д.</span><span class="sxs-lookup"><span data-stu-id="44942-173">You can then create *myNic1*, *MyNic2* and so on.</span></span> <span data-ttu-id="44942-174">Hello следующий код является примером добавления hello значение индекса:</span><span class="sxs-lookup"><span data-stu-id="44942-174">hello following code shows an example of appending hello index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="44942-175">Вы можете ознакомиться с полным примером [создания нескольких сетевых адаптеров с помощью шаблонов Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="44942-175">You can read a complete example of [creating multiple NICs by using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="44942-176">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="44942-176">Next steps</span></span>
<span data-ttu-id="44942-177">Просмотрите [размеры виртуальных Машин Windows](sizes.md) когда вы пытаетесь toocreate виртуальной Машины, которая имеет несколько сетевых адаптеров.</span><span class="sxs-lookup"><span data-stu-id="44942-177">Review [Windows VM sizes](sizes.md) when you're trying toocreate a VM that has multiple NICs.</span></span> <span data-ttu-id="44942-178">Обратите внимание toohello максимальное количество сетевых адаптеров, поддерживаемых для каждого размера виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="44942-178">Pay attention toohello maximum number of NICs that each VM size supports.</span></span> 


