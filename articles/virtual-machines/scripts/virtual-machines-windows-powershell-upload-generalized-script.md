---
title: "aaaUpload обобщенный tooAzure VHD образец скрипта PowerShell | Документы Microsoft"
description: "Образец сценария tooupload обобщенный tooAzure виртуального жесткого диска и создайте новую ВМ с помощью модели развертывания диспетчера ресурсов hello и дисков, управляемых PowerShell."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/18/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 72b4ff09eb7a6ba1604b9d5cbac51e60eded7545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sample-script-tooupload-a-vhd-tooazure-and-create-a-new-vm"></a><span data-ttu-id="0dbf5-103">Пример сценария tooupload tooAzure виртуального жесткого диска и создание новой виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="0dbf5-103">Sample script tooupload a VHD tooAzure and create a new VM</span></span>

<span data-ttu-id="0dbf5-104">Этот сценарий принимает локального VHD-файл с универсальной ВМ и передает его tooAzure, создает образ диска управляемых и использует toocreate hello новой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="0dbf5-104">This script takes a local .vhd file from a generalized VM and uploads it tooAzure, creates a Managed Disk image and uses hello toocreate a new VM.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="0dbf5-105">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="0dbf5-105">Sample script</span></span>

```powershell
# Provide values for hello variables
$resourceGroup = 'myResourceGroup'
$location = 'EastUS'
$storageaccount = 'mystorageaccount'
$storageType = 'Standard_LRS'
$containername = 'mycontainer'
$localPath = 'C:\Users\Public\Documents\Hyper-V\VHDs\generalized.vhd'
$vmName = 'myVM'
$imageName = 'myImage'
$vhdName = 'myUploadedVhd.vhd'
$diskSizeGB = '128'
$subnetName = 'mySubnet'
$vnetName = 'myVnet'
$ipName = 'myPip'
$nicName = 'myNic'
$nsgName = 'myNsg'
$ruleName = 'myRdpRule'
$vmName = 'myVM'
$computerName = 'myComputerName'
$vmSize = 'Standard_DS1_v2'

# Get hello username and password toobe used for hello administrators account on hello VM. 
# This is used when connecting toohello VM using RDP.

$cred = Get-Credential

# Upload hello VHD
New-AzureRmResourceGroup -Name $resourceGroup -Location $location
New-AzureRmStorageAccount -ResourceGroupName $resourceGroup -Name $storageAccount -Location $location `
    -SkuName $storageType -Kind "Storage"
$urlOfUploadedImageVhd = ('https://' + $storageaccount + '.blob.core.windows.net/' + $containername + '/' + $vhdName)
Add-AzureRmVhd -ResourceGroupName $resourceGroup -Destination $urlOfUploadedImageVhd `
    -LocalFilePath $localPath

# Note: Uploading hello VHD may take awhile!

# Create a managed image from hello uploaded VHD 
$imageConfig = New-AzureRmImageConfig -Location $location
$imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized `
    -BlobUri $urlOfUploadedImageVhd
$image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $resourceGroup -Image $imageConfig
 
# Create hello networking resources
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $resourceGroup -Location $location `
    -AllocationMethod Dynamic
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $resourceGroup -Location $location `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description 'Allow RDP' -Access Allow `
    -Protocol Tcp -Direction Inbound -Priority 110 -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $resourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $resourceGroup -Name $vnetName

# Start building hello VM configuration
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

# Set hello VM image as source image for hello new VM
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id

# Finish hello VM configuration and add hello NIC.
$vm = Set-AzureRmVMOSDisk -VM $vm  -DiskSizeInGB $diskSizeGB -CreateOption FromImage -Caching ReadWrite
$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

# Create hello VM
New-AzureRmVM -VM $vm -ResourceGroupName $resourceGroup -Location $location

# Verify that hello VM was created
$vmList = Get-AzureRmVM -ResourceGroupName $resourceGroup
$vmList.Name


```


<!-- 
[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-iis/create-windows-vm-iis.ps1 "Create VM IIS")] -->

## <a name="clean-up-deployment"></a><span data-ttu-id="0dbf5-106">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="0dbf5-106">Clean up deployment</span></span> 

<span data-ttu-id="0dbf5-107">Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="0dbf5-107">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name $resourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="0dbf5-108">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="0dbf5-108">Script explanation</span></span>

<span data-ttu-id="0dbf5-109">Этот скрипт использует следующие команды toocreate hello развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="0dbf5-109">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="0dbf5-110">Каждый элемент в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="0dbf5-110">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="0dbf5-111">Команда</span><span class="sxs-lookup"><span data-stu-id="0dbf5-111">Command</span></span>                                                                                                             | <span data-ttu-id="0dbf5-112">Примечания</span><span class="sxs-lookup"><span data-stu-id="0dbf5-112">Notes</span></span>                                                                                                                                                                                |
|---------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="0dbf5-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0dbf5-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)                           | <span data-ttu-id="0dbf5-114">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="0dbf5-114">Creates a resource group in which all resources are stored.</span></span>                                                                                                                          |
| [<span data-ttu-id="0dbf5-115">New-AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="0dbf5-115">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.resources/new-azurermstorageaccount)                         | <span data-ttu-id="0dbf5-116">Создание учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="0dbf5-116">Creates a storage account.</span></span>                                                                                                                                                           |
| [<span data-ttu-id="0dbf5-117">Add-AzureRmVhd</span><span class="sxs-lookup"><span data-stu-id="0dbf5-117">Add-AzureRmVhd</span></span>](/powershell/module/azurerm.resources/add-azurermvhd)                                               | <span data-ttu-id="0dbf5-118">Отправка виртуального жесткого диска из локальной виртуальной машины tooa большого двоичного объекта в учетная запись облачного хранилища в Azure.</span><span class="sxs-lookup"><span data-stu-id="0dbf5-118">Uploads a virtual hard disk from an on-premises virtual machine tooa blob in a cloud storage account in Azure.</span></span>                                                                       |
| [<span data-ttu-id="0dbf5-119">New-AzureRmImageConfig</span><span class="sxs-lookup"><span data-stu-id="0dbf5-119">New-AzureRmImageConfig</span></span>](/powershell/module/azurerm.resources/new-azurermimageconfig)                               | <span data-ttu-id="0dbf5-120">Создает настраиваемый объект образа.</span><span class="sxs-lookup"><span data-stu-id="0dbf5-120">Creates a configurable image object.</span></span>                                                                                                                                                 |
| [<span data-ttu-id="0dbf5-121">Set-AzureRmImageOsDisk</span><span class="sxs-lookup"><span data-stu-id="0dbf5-121">Set-AzureRmImageOsDisk</span></span>](/powershell/module/azurerm.resources/set-azurermimageosdisk)                               | <span data-ttu-id="0dbf5-122">Задает свойства диска операционной системы hello объект image.</span><span class="sxs-lookup"><span data-stu-id="0dbf5-122">Sets hello operating system disk properties on an image object.</span></span>                                                                                                                        |
| [<span data-ttu-id="0dbf5-123">New-AzureRmImage</span><span class="sxs-lookup"><span data-stu-id="0dbf5-123">New-AzureRmImage</span></span>](/powershell/module/azurerm.resources/new-azurermimage)                                           | <span data-ttu-id="0dbf5-124">Создает образ.</span><span class="sxs-lookup"><span data-stu-id="0dbf5-124">Creates a new image.</span></span>                                                                                                                                                                 |
| [<span data-ttu-id="0dbf5-125">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="0dbf5-125">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.resources/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="0dbf5-126">Создает конфигурацию подсети.</span><span class="sxs-lookup"><span data-stu-id="0dbf5-126">Creates a subnet configuration.</span></span> <span data-ttu-id="0dbf5-127">Эта конфигурация используется с hello процесс создания виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="0dbf5-127">This configuration is used with hello virtual network creation process.</span></span>                                                                                |
| [<span data-ttu-id="0dbf5-128">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="0dbf5-128">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.resources/new-azurermvirtualnetwork)                         | <span data-ttu-id="0dbf5-129">Создает виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="0dbf5-129">Creates a virtual network.</span></span>                                                                                                                                                           |
| [<span data-ttu-id="0dbf5-130">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="0dbf5-130">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.resources/new-azurermpublicipaddress)                       | <span data-ttu-id="0dbf5-131">Создает общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="0dbf5-131">Creates a public IP address.</span></span>                                                                                                                                                         |
| [<span data-ttu-id="0dbf5-132">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="0dbf5-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.resources/new-azurermnetworkinterface)                     | <span data-ttu-id="0dbf5-133">Создает сетевой интерфейс.</span><span class="sxs-lookup"><span data-stu-id="0dbf5-133">Creates a network interface.</span></span>                                                                                                                                                         |
| [<span data-ttu-id="0dbf5-134">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="0dbf5-134">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.resources/new-azurermnetworksecurityruleconfig)   | <span data-ttu-id="0dbf5-135">Создает конфигурацию правил группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="0dbf5-135">Creates a network security group rule configuration.</span></span> <span data-ttu-id="0dbf5-136">Такая настройка является toocreate используется правило NSG при создании hello NSG.</span><span class="sxs-lookup"><span data-stu-id="0dbf5-136">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span>                                                       |
| [<span data-ttu-id="0dbf5-137">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="0dbf5-137">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.resources/new-azurermnetworksecuritygroup)             | <span data-ttu-id="0dbf5-138">Создает группу безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="0dbf5-138">Creates a network security group.</span></span>                                                                                                                                                    |
| [<span data-ttu-id="0dbf5-139">Get-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="0dbf5-139">Get-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.resources/get-azurermvirtualnetwork)                         | <span data-ttu-id="0dbf5-140">Получает виртуальную сеть в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0dbf5-140">Gets a virtual network in a resource group.</span></span>                                                                                                                                          |
| [<span data-ttu-id="0dbf5-141">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="0dbf5-141">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.resources/new-azurermvmconfig)                                     | <span data-ttu-id="0dbf5-142">Создает конфигурацию виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0dbf5-142">Creates a VM configuration.</span></span> <span data-ttu-id="0dbf5-143">Эта конфигурация включает в себя такие сведения, как имя виртуальной машины, операционную систему и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="0dbf5-143">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="0dbf5-144">Конфигурация Hello используется во время создания виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="0dbf5-144">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="0dbf5-145">Set-AzureRmVMSourceImage</span><span class="sxs-lookup"><span data-stu-id="0dbf5-145">Set-AzureRmVMSourceImage</span></span>](/powershell/module/azurerm.resources/set-azurermvmsourceimage)                           | <span data-ttu-id="0dbf5-146">Указывает образ для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0dbf5-146">Specifies an image for a virtual machine.</span></span>                                                                                                                                            |
| [<span data-ttu-id="0dbf5-147">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="0dbf5-147">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.resources/set-azurermvmosdisk)                                     | <span data-ttu-id="0dbf5-148">Задает свойства диска hello операционной системы на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="0dbf5-148">Sets hello operating system disk properties on a virtual machine.</span></span>                                                                                                                      |
| [<span data-ttu-id="0dbf5-149">Set-AzureRmVMOperatingSystem</span><span class="sxs-lookup"><span data-stu-id="0dbf5-149">Set-AzureRmVMOperatingSystem</span></span>](/powershell/module/azurerm.resources/set-azurermvmoperatingsystem)                   | <span data-ttu-id="0dbf5-150">Задает свойства диска hello операционной системы на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="0dbf5-150">Sets hello operating system disk properties on a virtual machine.</span></span>                                                                                                                      |
| [<span data-ttu-id="0dbf5-151">Add-AzureRmVMNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="0dbf5-151">Add-AzureRmVMNetworkInterface</span></span>](/powershell/module/azurerm.resources/add-azurermvmnetworkinterface)                 | <span data-ttu-id="0dbf5-152">Добавляет сетевой интерфейс tooa виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="0dbf5-152">Adds a network interface tooa virtual machine.</span></span>                                                                                                                                       |
| [<span data-ttu-id="0dbf5-153">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="0dbf5-153">New-AzureRmVM</span></span>](/powershell/module/azurerm.resources/new-azurermvm)                                                 | <span data-ttu-id="0dbf5-154">Создайте виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="0dbf5-154">Create a virtual machine.</span></span>                                                                                                                                                            |
| [<span data-ttu-id="0dbf5-155">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0dbf5-155">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup)                     | <span data-ttu-id="0dbf5-156">Удаляет группу ресурсов и все ресурсы, содержащиеся в ней.</span><span class="sxs-lookup"><span data-stu-id="0dbf5-156">Removes a resource group and all resources contained within.</span></span>                                                                                                                         |

## <a name="next-steps"></a><span data-ttu-id="0dbf5-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0dbf5-157">Next steps</span></span>

<span data-ttu-id="0dbf5-158">Дополнительные сведения о hello модуля Azure PowerShell см. в разделе [документация по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0dbf5-158">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="0dbf5-159">Примеры сценариев PowerShell дополнительную виртуальную машину можно найти в hello [документации виртуальной Машины Windows Azure](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0dbf5-159">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
