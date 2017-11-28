---
title: "Создание виртуальной машины из управляемого образа виртуальной машины в Azure | Документация Майкрософт"
description: "Создание виртуальной машины Windows из универсального управляемого образа виртуальной машины с использованием Azure PowerShell в модели развертывания с помощью Resource Manager."
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
ms.openlocfilehash: 2bb2d66271178a64ec0f4642e46b23f5618a56d9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-vm-from-a-managed-image"></a><span data-ttu-id="1411a-103">Создание виртуальной машины из управляемого образа</span><span class="sxs-lookup"><span data-stu-id="1411a-103">Create a VM from a managed image</span></span>

<span data-ttu-id="1411a-104">Можно создать несколько виртуальных машин из управляемого образа виртуальной машины в Azure.</span><span class="sxs-lookup"><span data-stu-id="1411a-104">You can create multiple VMs from a managed VM image in Azure.</span></span> <span data-ttu-id="1411a-105">Управляемый образ виртуальной машины содержит сведения, необходимые для создания виртуальной машины, включая диски ОС и диски данных.</span><span class="sxs-lookup"><span data-stu-id="1411a-105">A managed VM image contains the information necessary to create a VM, including the OS and data disks.</span></span> <span data-ttu-id="1411a-106">Виртуальные жесткие диски, входящие в образ, включая диски ОС и диски данных, хранятся в виде управляемых дисков.</span><span class="sxs-lookup"><span data-stu-id="1411a-106">The VHDs that make up the image, including both the OS disks and any data disks, are stored as managed disks.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="1411a-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1411a-107">Prerequisites</span></span>

<span data-ttu-id="1411a-108">Для создания новой виртуальной машины необходим [управляемый образ виртуальной машины](capture-image-resource.md).</span><span class="sxs-lookup"><span data-stu-id="1411a-108">You need to have already [created a managed VM image](capture-image-resource.md) to use for creating the new VM.</span></span> 

<span data-ttu-id="1411a-109">Убедитесь, что у вас установлены последние версии модулей PowerShell AzureRM.Compute и AzureRM.Network PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1411a-109">Make sure that you have the latest versions of the AzureRM.Compute and AzureRM.Network PowerShell modules.</span></span> <span data-ttu-id="1411a-110">Чтобы установить их, откройте командную строку PowerShell с правами администратора и выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="1411a-110">Open a PowerShell prompt as an Administrator and run the following command to install them.</span></span>

```powershell
Install-Module AzureRM.Compute,AzureRM.Network
```
<span data-ttu-id="1411a-111">Дополнительные сведения см. в разделе [об управлении версиями Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1411a-111">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>



## <a name="collect-information-about-the-image"></a><span data-ttu-id="1411a-112">Сбор сведений об образе</span><span class="sxs-lookup"><span data-stu-id="1411a-112">Collect information about the image</span></span>

<span data-ttu-id="1411a-113">Сначала необходимо собрать основные сведения об образе и создать для него переменную.</span><span class="sxs-lookup"><span data-stu-id="1411a-113">First we need to gather basic information about the image and create a variable for the image.</span></span> <span data-ttu-id="1411a-114">В этом примере используется управляемый образ виртуальной машины **myImage**, находящийся в группе ресурсов **myResourceGroup** в расположении **Западно-центральная часть США**.</span><span class="sxs-lookup"><span data-stu-id="1411a-114">This example uses a managed VM image named **myImage** that is in the **myResourceGroup** resource group in the **West Central US** location.</span></span> 

```powershell
$rgName = "myResourceGroup"
$location = "West Central US"
$imageName = "myImage"
$image = Get-AzureRMImage -ImageName $imageName -ResourceGroupName $rgName
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="1411a-115">Создать виртуальную сеть</span><span class="sxs-lookup"><span data-stu-id="1411a-115">Create a virtual network</span></span>
<span data-ttu-id="1411a-116">Создайте виртуальную сеть и подсеть [виртуальной сети](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1411a-116">Create the vNet and subnet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="1411a-117">Создание подсети.</span><span class="sxs-lookup"><span data-stu-id="1411a-117">Create the subnet.</span></span> <span data-ttu-id="1411a-118">В этом примере создается подсеть **mySubnet** с префиксом адреса **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="1411a-118">This example creates a subnet named **mySubnet** with the address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="1411a-119">Создание виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="1411a-119">Create the virtual network.</span></span> <span data-ttu-id="1411a-120">В этом примере создается виртуальная сеть **myVnet** с префиксом адреса **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="1411a-120">This example creates a virtual network named **myVnet** with the address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="1411a-121">Создание общедоступного IP-адреса и сетевого интерфейса</span><span class="sxs-lookup"><span data-stu-id="1411a-121">Create a public IP address and network interface</span></span>

<span data-ttu-id="1411a-122">Чтобы обеспечить обмен данными с виртуальной машиной в виртуальной сети, требуются [общедоступный IP-адрес](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) и сетевой интерфейс.</span><span class="sxs-lookup"><span data-stu-id="1411a-122">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="1411a-123">Создание общедоступного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="1411a-123">Create a public IP address.</span></span> <span data-ttu-id="1411a-124">В этом примере создается общедоступный IP-адрес с именем **myPip**.</span><span class="sxs-lookup"><span data-stu-id="1411a-124">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="1411a-125">Создание сетевой карты.</span><span class="sxs-lookup"><span data-stu-id="1411a-125">Create the NIC.</span></span> <span data-ttu-id="1411a-126">В этом примере создается сетевая карта с именем **myNic**.</span><span class="sxs-lookup"><span data-stu-id="1411a-126">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="1411a-127">Создание группы безопасности сети и правила RDP</span><span class="sxs-lookup"><span data-stu-id="1411a-127">Create the network security group and an RDP rule</span></span>

<span data-ttu-id="1411a-128">Чтобы войти на виртуальную машину с помощью RDP, необходимо настроить группу безопасности сети, которая разрешает доступ по протоколу RDP через порт 3389.</span><span class="sxs-lookup"><span data-stu-id="1411a-128">To be able to log in to your VM using RDP, you need to have a network security rule (NSG) that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="1411a-129">В этом примере создается группа безопасности сети с именем **myNsg**, которая содержит правило с именем **myRdpRule**, разрешающее трафик RDP через порт 3389.</span><span class="sxs-lookup"><span data-stu-id="1411a-129">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="1411a-130">Дополнительные сведения о группах безопасности сети см. в статье [Открытие портов для виртуальной машины в Azure с помощью PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1411a-130">For more information about NSGs, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

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


## <a name="create-a-variable-for-the-virtual-network"></a><span data-ttu-id="1411a-131">Создание переменной для виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="1411a-131">Create a variable for the virtual network</span></span>

<span data-ttu-id="1411a-132">Создайте переменную для готовой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="1411a-132">Create a variable for the completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-the-credentials-for-the-vm"></a><span data-ttu-id="1411a-133">Получение учетных данных для виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="1411a-133">Get the credentials for the VM</span></span>

<span data-ttu-id="1411a-134">Следующий командлет откроет окно, в котором необходимо ввести новое имя пользователя и пароль, используемые в качестве учетной записи локального администратора для удаленного доступа к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="1411a-134">The following cmdlet will open a window where you will enter a new user name and password to use as the local administrator account for remotely accessing the VM.</span></span> 

```powershell
$cred = Get-Credential
```

## <a name="set-variables-for-the-vm-name-computer-name-and-the-size-of-the-vm"></a><span data-ttu-id="1411a-135">Задание переменных для имени виртуальной машины, имени компьютера и размера виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="1411a-135">Set variables for the VM name, computer name and the size of the VM</span></span>

1. <span data-ttu-id="1411a-136">Создайте переменные для имени виртуальной машины и компьютера.</span><span class="sxs-lookup"><span data-stu-id="1411a-136">Create variables for the VM name and computer name.</span></span> <span data-ttu-id="1411a-137">В этом примере имя виртуальной машины задается как **myVM**, а имя компьютера — как **myComputer**.</span><span class="sxs-lookup"><span data-stu-id="1411a-137">This example sets the VM name as **myVM** and the computer name as **myComputer**.</span></span>

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    ```
2. <span data-ttu-id="1411a-138">Задайте размер виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="1411a-138">Set the size of the virtual machine.</span></span> <span data-ttu-id="1411a-139">В этом примере создается виртуальная машина размера **Standard_DS1_v2**.</span><span class="sxs-lookup"><span data-stu-id="1411a-139">This example creates **Standard_DS1_v2** sized VM.</span></span> <span data-ttu-id="1411a-140">Дополнительные сведения см. в [документации по размерам виртуальных машин](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/).</span><span class="sxs-lookup"><span data-stu-id="1411a-140">See the [VM sizes](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) documentation for more information.</span></span>

    ```powershell
    $vmSize = "Standard_DS1_v2"
    ```

3. <span data-ttu-id="1411a-141">Добавьте имя и размер виртуальной машины в конфигурацию виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="1411a-141">Add the VM name and size to the VM configuration.</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-the-vm-image-as-source-image-for-the-new-vm"></a><span data-ttu-id="1411a-142">Настройка образа виртуальной машины в качестве исходного образа для новой виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="1411a-142">Set the VM image as source image for the new VM</span></span>

<span data-ttu-id="1411a-143">Настройте исходный образ, используя идентификатор управляемого образа виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="1411a-143">Set the source image using the ID of the managed VM image.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-the-os-configuration-and-add-the-nic"></a><span data-ttu-id="1411a-144">Настройте конфигурацию операционной системы и добавьте сетевую карту.</span><span class="sxs-lookup"><span data-stu-id="1411a-144">Set the OS configuration and add the NIC.</span></span>

<span data-ttu-id="1411a-145">Введите тип хранилища (PremiumLRS или StandardLRS) и размер диска операционной системы.</span><span class="sxs-lookup"><span data-stu-id="1411a-145">Enter the storage type (PremiumLRS or StandardLRS) and the size of the OS disk.</span></span> <span data-ttu-id="1411a-146">В этом примере для типа учетной записи задается значение **PremiumLRS**, для размера диска — **128 ГБ**, а для кэширования диска — **ReadWrite**.</span><span class="sxs-lookup"><span data-stu-id="1411a-146">This example sets the account type to **PremiumLRS**, the disk size to **128 GB** and disk caching to **ReadWrite**.</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm  -StorageAccountType PremiumLRS -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-the-vm"></a><span data-ttu-id="1411a-147">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="1411a-147">Create the VM</span></span>

<span data-ttu-id="1411a-148">Создайте виртуальную машину с использованием конфигурации, созданной и хранимой в переменной **$vm**.</span><span class="sxs-lookup"><span data-stu-id="1411a-148">Create the new Vm using the configuration that we have built and stored in the **$vm** variable.</span></span>

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="1411a-149">Проверка создания виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="1411a-149">Verify that the VM was created</span></span>
<span data-ttu-id="1411a-150">После завершения процесса новая виртуальная машина должна отображаться на [портале Azure](https://portal.azure.com) (выберите элементы **Обзор** > **Виртуальные машины**). Ее можно также увидеть, выполнив следующие команды PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1411a-150">When complete, you should see the newly created VM in the [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="1411a-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1411a-151">Next steps</span></span>
<span data-ttu-id="1411a-152">Сведения об управлении новыми виртуальными машинами с помощью PowerShell см. в статье [Создание виртуальных машин Windows и управление ими с помощью модуля Azure PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1411a-152">To manage your new virtual machine with Azure PowerShell, see [Create and manage Windows VMs with the Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

