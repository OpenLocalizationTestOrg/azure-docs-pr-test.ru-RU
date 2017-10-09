---
title: "aaaCreate виртуальной Машины из управляемый образ виртуальной Машины в Azure | Документы Microsoft"
description: "Создание виртуальной машины Windows из общего управляемого образа виртуальной Машины с помощью Azure PowerShell, в модели развертывания диспетчера ресурсов hello."
services: virtual-machines-windows
documentationcenter: 
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
ms.date: 05/22/2017
ms.author: cynthn
ms.openlocfilehash: 5036ef1533c144a9a328e94599b359e0166f337d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-managed-image"></a><span data-ttu-id="1d64b-103">Создание виртуальной машины из управляемого образа</span><span class="sxs-lookup"><span data-stu-id="1d64b-103">Create a VM from a managed image</span></span>

<span data-ttu-id="1d64b-104">Можно создать несколько виртуальных машин из управляемого образа виртуальной машины в Azure.</span><span class="sxs-lookup"><span data-stu-id="1d64b-104">You can create multiple VMs from a managed VM image in Azure.</span></span> <span data-ttu-id="1d64b-105">Управляемый образ ВМ содержит toocreate необходимые сведения hello виртуальной Машины, включая hello ОС и дисков данных.</span><span class="sxs-lookup"><span data-stu-id="1d64b-105">A managed VM image contains hello information necessary toocreate a VM, including hello OS and data disks.</span></span> <span data-ttu-id="1d64b-106">Здравствуйте, виртуальные жесткие диски, составляющие hello изображения, включая диски hello ОС и дисков данных, хранятся в виде управляемых дисков.</span><span class="sxs-lookup"><span data-stu-id="1d64b-106">hello VHDs that make up hello image, including both hello OS disks and any data disks, are stored as managed disks.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="1d64b-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1d64b-107">Prerequisites</span></span>

<span data-ttu-id="1d64b-108">Требуется toohave уже [создан управляемый образ виртуальной Машины](capture-image-resource.md) Здравствуйте, toouse для создания новой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="1d64b-108">You need toohave already [created a managed VM image](capture-image-resource.md) toouse for creating hello new VM.</span></span> 

<span data-ttu-id="1d64b-109">Убедитесь, что последние версии hello hello AzureRM.Compute и AzureRM.Network модули PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1d64b-109">Make sure that you have hello latest versions of hello AzureRM.Compute and AzureRM.Network PowerShell modules.</span></span> <span data-ttu-id="1d64b-110">Откройте командную строку PowerShell с правами администратора и выполните следующие команды tooinstall hello их.</span><span class="sxs-lookup"><span data-stu-id="1d64b-110">Open a PowerShell prompt as an Administrator and run hello following command tooinstall them.</span></span>

```powershell
Install-Module AzureRM.Compute,AzureRM.Network
```
<span data-ttu-id="1d64b-111">Дополнительные сведения см. в разделе [об управлении версиями Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1d64b-111">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>



## <a name="collect-information-about-hello-image"></a><span data-ttu-id="1d64b-112">Собирать данные об образе hello</span><span class="sxs-lookup"><span data-stu-id="1d64b-112">Collect information about hello image</span></span>

<span data-ttu-id="1d64b-113">Сначала нам нужна toogather основные сведения о hello и создайте переменную для hello образа.</span><span class="sxs-lookup"><span data-stu-id="1d64b-113">First we need toogather basic information about hello image and create a variable for hello image.</span></span> <span data-ttu-id="1d64b-114">В этом примере используется управляемый образ виртуальной Машины с именем **myImage** именно в hello **myResourceGroup** группы ресурсов в hello **Западная центральной части США** расположение.</span><span class="sxs-lookup"><span data-stu-id="1d64b-114">This example uses a managed VM image named **myImage** that is in hello **myResourceGroup** resource group in hello **West Central US** location.</span></span> 

```powershell
$rgName = "myResourceGroup"
$location = "West Central US"
$imageName = "myImage"
$image = Get-AzureRMImage -ImageName $imageName -ResourceGroupName $rgName
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="1d64b-115">Создать виртуальную сеть</span><span class="sxs-lookup"><span data-stu-id="1d64b-115">Create a virtual network</span></span>
<span data-ttu-id="1d64b-116">Создание виртуальной сети hello и подсеть hello [виртуальной сети](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1d64b-116">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="1d64b-117">Создайте подсеть hello.</span><span class="sxs-lookup"><span data-stu-id="1d64b-117">Create hello subnet.</span></span> <span data-ttu-id="1d64b-118">В этом примере создается подсеть с именем **mySubnet** с префикс адреса hello **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="1d64b-118">This example creates a subnet named **mySubnet** with hello address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="1d64b-119">Создайте виртуальную сеть hello.</span><span class="sxs-lookup"><span data-stu-id="1d64b-119">Create hello virtual network.</span></span> <span data-ttu-id="1d64b-120">В этом примере создается виртуальная сеть с именем **myVnet** с префикс адреса hello **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="1d64b-120">This example creates a virtual network named **myVnet** with hello address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="1d64b-121">Создание общедоступного IP-адреса и сетевого интерфейса</span><span class="sxs-lookup"><span data-stu-id="1d64b-121">Create a public IP address and network interface</span></span>

<span data-ttu-id="1d64b-122">требуется tooenable взаимодействия с виртуальной машиной hello в виртуальной сети hello, [общедоступный IP-адрес](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) и сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="1d64b-122">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="1d64b-123">Создание общедоступного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="1d64b-123">Create a public IP address.</span></span> <span data-ttu-id="1d64b-124">В этом примере создается общедоступный IP-адрес с именем **myPip**.</span><span class="sxs-lookup"><span data-stu-id="1d64b-124">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="1d64b-125">Создайте сетевую карту hello.</span><span class="sxs-lookup"><span data-stu-id="1d64b-125">Create hello NIC.</span></span> <span data-ttu-id="1d64b-126">В этом примере создается сетевая карта с именем **myNic**.</span><span class="sxs-lookup"><span data-stu-id="1d64b-126">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="1d64b-127">Создание группы безопасности сети hello и правило протокола удаленного рабочего СТОЛА</span><span class="sxs-lookup"><span data-stu-id="1d64b-127">Create hello network security group and an RDP rule</span></span>

<span data-ttu-id="1d64b-128">возможности toolog toobe в tooyour виртуальную Машину с помощью протокола удаленного рабочего СТОЛА, необходимо toohave правило сетевой безопасности (NSG), позволяющий RDP-доступ через порт 3389.</span><span class="sxs-lookup"><span data-stu-id="1d64b-128">toobe able toolog in tooyour VM using RDP, you need toohave a network security rule (NSG) that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="1d64b-129">В этом примере создается группа безопасности сети с именем **myNsg**, которая содержит правило с именем **myRdpRule**, разрешающее трафик RDP через порт 3389.</span><span class="sxs-lookup"><span data-stu-id="1d64b-129">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="1d64b-130">Дополнительные сведения о Nsg см. в разделе [Открытие портов tooa ВМ в Azure с помощью PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1d64b-130">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"
$ruleName = "myRdpRule"
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="1d64b-131">Создайте переменную для hello виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="1d64b-131">Create a variable for hello virtual network</span></span>

<span data-ttu-id="1d64b-132">Создайте переменную для завершения hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="1d64b-132">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-hello-credentials-for-hello-vm"></a><span data-ttu-id="1d64b-133">Получить учетные данные hello для hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="1d64b-133">Get hello credentials for hello VM</span></span>

<span data-ttu-id="1d64b-134">Hello следующий командлет будет открыто окно, можно будет ввести имя и пароль toouse пользователя новый под учетной записью локального администратора hello удаленного доступа hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="1d64b-134">hello following cmdlet will open a window where you will enter a new user name and password toouse as hello local administrator account for remotely accessing hello VM.</span></span> 

```powershell
$cred = Get-Credential
```

## <a name="set-variables-for-hello-vm-name-computer-name-and-hello-size-of-hello-vm"></a><span data-ttu-id="1d64b-135">Набор переменных для hello виртуальной Машины, имя, имя компьютера и hello размер hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="1d64b-135">Set variables for hello VM name, computer name and hello size of hello VM</span></span>

1. <span data-ttu-id="1d64b-136">Создайте переменные hello имя виртуальной Машины и имя компьютера.</span><span class="sxs-lookup"><span data-stu-id="1d64b-136">Create variables for hello VM name and computer name.</span></span> <span data-ttu-id="1d64b-137">В этом примере задает имя виртуальной Машины hello как **myVM** и имя компьютера hello как **myComputer**.</span><span class="sxs-lookup"><span data-stu-id="1d64b-137">This example sets hello VM name as **myVM** and hello computer name as **myComputer**.</span></span>

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    ```
2. <span data-ttu-id="1d64b-138">Задайте размер hello hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="1d64b-138">Set hello size of hello virtual machine.</span></span> <span data-ttu-id="1d64b-139">В этом примере создается виртуальная машина размера **Standard_DS1_v2**.</span><span class="sxs-lookup"><span data-stu-id="1d64b-139">This example creates **Standard_DS1_v2** sized VM.</span></span> <span data-ttu-id="1d64b-140">В разделе hello [размеры виртуальных Машин](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) Дополнительные сведения см.</span><span class="sxs-lookup"><span data-stu-id="1d64b-140">See hello [VM sizes](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) documentation for more information.</span></span>

    ```powershell
    $vmSize = "Standard_DS1_v2"
    ```

3. <span data-ttu-id="1d64b-141">Добавьте hello имя виртуальной Машины и конфигурация виртуальной Машины toohello размера.</span><span class="sxs-lookup"><span data-stu-id="1d64b-141">Add hello VM name and size toohello VM configuration.</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a><span data-ttu-id="1d64b-142">Образ виртуальной Машины hello набор как источник изображения hello новой виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="1d64b-142">Set hello VM image as source image for hello new VM</span></span>

<span data-ttu-id="1d64b-143">Задать hello исходного образа с помощью идентификатора hello hello управляемый образ виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="1d64b-143">Set hello source image using hello ID of hello managed VM image.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a><span data-ttu-id="1d64b-144">Задание конфигурации hello ОС и добавление hello сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="1d64b-144">Set hello OS configuration and add hello NIC.</span></span>

<span data-ttu-id="1d64b-145">Введите тип хранения hello (PremiumLRS или StandardLRS) и hello размер диска операционной системы hello.</span><span class="sxs-lookup"><span data-stu-id="1d64b-145">Enter hello storage type (PremiumLRS or StandardLRS) and hello size of hello OS disk.</span></span> <span data-ttu-id="1d64b-146">В следующем примере тип учетной записи hello слишком**PremiumLRS**, hello размер диска слишком**128 ГБ** и их кэширование слишком**ReadWrite**.</span><span class="sxs-lookup"><span data-stu-id="1d64b-146">This example sets hello account type too**PremiumLRS**, hello disk size too**128 GB** and disk caching too**ReadWrite**.</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm  -StorageAccountType PremiumLRS -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a><span data-ttu-id="1d64b-147">Создание виртуальной Машины hello</span><span class="sxs-lookup"><span data-stu-id="1d64b-147">Create hello VM</span></span>

<span data-ttu-id="1d64b-148">Создание новой виртуальной машины с помощью конфигурации hello, мы строится и хранится в hello hello **$vm** переменной.</span><span class="sxs-lookup"><span data-stu-id="1d64b-148">Create hello new Vm using hello configuration that we have built and stored in hello **$vm** variable.</span></span>

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="1d64b-149">Убедитесь, что hello создания виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="1d64b-149">Verify that hello VM was created</span></span>
<span data-ttu-id="1d64b-150">По завершении вы увидите только что созданный виртуальной Машины в hello hello [портал Azure](https://portal.azure.com) под **Обзор** > **виртуальные машины**, или с помощью следующих hello Команды PowerShell:</span><span class="sxs-lookup"><span data-stu-id="1d64b-150">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="1d64b-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1d64b-151">Next steps</span></span>
<span data-ttu-id="1d64b-152">см. на новую виртуальную машину с помощью Azure PowerShell toomanage [Создание и управление виртуальными машинами Windows с помощью модуля Azure PowerShell hello](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1d64b-152">toomanage your new virtual machine with Azure PowerShell, see [Create and manage Windows VMs with hello Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

