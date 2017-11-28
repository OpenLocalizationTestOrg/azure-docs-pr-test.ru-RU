---
title: "Пример сценария PowerShell \"Отправка универсального VHD в Azure\" | Документы Майкрософт"
description: "Пример сценария PowerShell для отправки универсального виртуального жесткого диска (VHD) в Azure и создания виртуальной машины с помощью модели развертывания Azure Resource Manager и управляемых дисков."
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
ms.openlocfilehash: cd3d87bb4384971e28d3330cd5c1a3d351129036
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="sample-script-to-upload-a-vhd-to-azure-and-create-a-new-vm"></a><span data-ttu-id="6e916-103">Пример сценария для отправки VHD в Azure и создания виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="6e916-103">Sample script to upload a VHD to Azure and create a new VM</span></span>

<span data-ttu-id="6e916-104">Этот сценарий принимает локальный VHD-файл из универсальной виртуальной машины и отправляет его в Azure, создает образ управляемого диска и использует его для создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="6e916-104">This script takes a local .vhd file from a generalized VM and uploads it to Azure, creates a Managed Disk image and uses the to create a new VM.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="6e916-105">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="6e916-105">Sample script</span></span>

```powershell
# Provide values for the variables
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

# Get the username and password to be used for the administrators account on the VM. 
# This is used when connecting to the VM using RDP.

$cred = Get-Credential

# Upload the VHD
New-AzureRmResourceGroup -Name $resourceGroup -Location $location
New-AzureRmStorageAccount -ResourceGroupName $resourceGroup -Name $storageAccount -Location $location `
    -SkuName $storageType -Kind "Storage"
$urlOfUploadedImageVhd = ('https://' + $storageaccount + '.blob.core.windows.net/' + $containername + '/' + $vhdName)
Add-AzureRmVhd -ResourceGroupName $resourceGroup -Destination $urlOfUploadedImageVhd `
    -LocalFilePath $localPath

# Note: Uploading the VHD may take awhile!

# Create a managed image from the uploaded VHD 
$imageConfig = New-AzureRmImageConfig -Location $location
$imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized `
    -BlobUri $urlOfUploadedImageVhd
$image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $resourceGroup -Image $imageConfig
 
# Create the networking resources
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

# Start building the VM configuration
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

# Set the VM image as source image for the new VM
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id

# Finish the VM configuration and add the NIC.
$vm = Set-AzureRmVMOSDisk -VM $vm  -DiskSizeInGB $diskSizeGB -CreateOption FromImage -Caching ReadWrite
$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

# Create the VM
New-AzureRmVM -VM $vm -ResourceGroupName $resourceGroup -Location $location

# Verify that the VM was created
$vmList = Get-AzureRmVM -ResourceGroupName $resourceGroup
$vmList.Name


```


<!-- 
[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-iis/create-windows-vm-iis.ps1 "Create VM IIS")] -->

## <a name="clean-up-deployment"></a><span data-ttu-id="6e916-106">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="6e916-106">Clean up deployment</span></span> 

<span data-ttu-id="6e916-107">Выполните следующую команду, чтобы удалить группу ресурсов, виртуальную машину и все связанные с ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="6e916-107">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name $resourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="6e916-108">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="6e916-108">Script explanation</span></span>

<span data-ttu-id="6e916-109">Чтобы создать развертывание, скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="6e916-109">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="6e916-110">Для каждого элемента в таблице приведены ссылки на документацию по команде.</span><span class="sxs-lookup"><span data-stu-id="6e916-110">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6e916-111">Команда</span><span class="sxs-lookup"><span data-stu-id="6e916-111">Command</span></span>                                                                                                             | <span data-ttu-id="6e916-112">Примечания</span><span class="sxs-lookup"><span data-stu-id="6e916-112">Notes</span></span>                                                                                                                                                                                |
|---------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="6e916-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6e916-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)                           | <span data-ttu-id="6e916-114">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="6e916-114">Creates a resource group in which all resources are stored.</span></span>                                                                                                                          |
| [<span data-ttu-id="6e916-115">New-AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="6e916-115">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.resources/new-azurermstorageaccount)                         | <span data-ttu-id="6e916-116">Создание учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="6e916-116">Creates a storage account.</span></span>                                                                                                                                                           |
| [<span data-ttu-id="6e916-117">Add-AzureRmVhd</span><span class="sxs-lookup"><span data-stu-id="6e916-117">Add-AzureRmVhd</span></span>](/powershell/module/azurerm.resources/add-azurermvhd)                                               | <span data-ttu-id="6e916-118">Передает виртуальный жесткий диск из локальной виртуальной машины в большой двоичный объект в облачной учетной записи хранения в Azure.</span><span class="sxs-lookup"><span data-stu-id="6e916-118">Uploads a virtual hard disk from an on-premises virtual machine to a blob in a cloud storage account in Azure.</span></span>                                                                       |
| [<span data-ttu-id="6e916-119">New-AzureRmImageConfig</span><span class="sxs-lookup"><span data-stu-id="6e916-119">New-AzureRmImageConfig</span></span>](/powershell/module/azurerm.resources/new-azurermimageconfig)                               | <span data-ttu-id="6e916-120">Создает настраиваемый объект образа.</span><span class="sxs-lookup"><span data-stu-id="6e916-120">Creates a configurable image object.</span></span>                                                                                                                                                 |
| [<span data-ttu-id="6e916-121">Set-AzureRmImageOsDisk</span><span class="sxs-lookup"><span data-stu-id="6e916-121">Set-AzureRmImageOsDisk</span></span>](/powershell/module/azurerm.resources/set-azurermimageosdisk)                               | <span data-ttu-id="6e916-122">Задает свойства диска операционной системы для объекта образа.</span><span class="sxs-lookup"><span data-stu-id="6e916-122">Sets the operating system disk properties on an image object.</span></span>                                                                                                                        |
| [<span data-ttu-id="6e916-123">New-AzureRmImage</span><span class="sxs-lookup"><span data-stu-id="6e916-123">New-AzureRmImage</span></span>](/powershell/module/azurerm.resources/new-azurermimage)                                           | <span data-ttu-id="6e916-124">Создает образ.</span><span class="sxs-lookup"><span data-stu-id="6e916-124">Creates a new image.</span></span>                                                                                                                                                                 |
| [<span data-ttu-id="6e916-125">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="6e916-125">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.resources/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="6e916-126">Создает конфигурацию подсети.</span><span class="sxs-lookup"><span data-stu-id="6e916-126">Creates a subnet configuration.</span></span> <span data-ttu-id="6e916-127">Эта конфигурация используется в процессе создания виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="6e916-127">This configuration is used with the virtual network creation process.</span></span>                                                                                |
| [<span data-ttu-id="6e916-128">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="6e916-128">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.resources/new-azurermvirtualnetwork)                         | <span data-ttu-id="6e916-129">Создает виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="6e916-129">Creates a virtual network.</span></span>                                                                                                                                                           |
| [<span data-ttu-id="6e916-130">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="6e916-130">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.resources/new-azurermpublicipaddress)                       | <span data-ttu-id="6e916-131">Создает общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="6e916-131">Creates a public IP address.</span></span>                                                                                                                                                         |
| [<span data-ttu-id="6e916-132">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="6e916-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.resources/new-azurermnetworkinterface)                     | <span data-ttu-id="6e916-133">Создает сетевой интерфейс.</span><span class="sxs-lookup"><span data-stu-id="6e916-133">Creates a network interface.</span></span>                                                                                                                                                         |
| [<span data-ttu-id="6e916-134">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="6e916-134">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.resources/new-azurermnetworksecurityruleconfig)   | <span data-ttu-id="6e916-135">Создает конфигурацию правил группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="6e916-135">Creates a network security group rule configuration.</span></span> <span data-ttu-id="6e916-136">Эта конфигурация используется для создания правила NSG при создании этой NSG.</span><span class="sxs-lookup"><span data-stu-id="6e916-136">This configuration is used to create an NSG rule when the NSG is created.</span></span>                                                       |
| [<span data-ttu-id="6e916-137">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="6e916-137">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.resources/new-azurermnetworksecuritygroup)             | <span data-ttu-id="6e916-138">Создает группу безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="6e916-138">Creates a network security group.</span></span>                                                                                                                                                    |
| [<span data-ttu-id="6e916-139">Get-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="6e916-139">Get-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.resources/get-azurermvirtualnetwork)                         | <span data-ttu-id="6e916-140">Получает виртуальную сеть в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6e916-140">Gets a virtual network in a resource group.</span></span>                                                                                                                                          |
| [<span data-ttu-id="6e916-141">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="6e916-141">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.resources/new-azurermvmconfig)                                     | <span data-ttu-id="6e916-142">Создает конфигурацию виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="6e916-142">Creates a VM configuration.</span></span> <span data-ttu-id="6e916-143">Эта конфигурация включает в себя такие сведения, как имя виртуальной машины, операционную систему и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="6e916-143">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="6e916-144">Данная конфигурации используется при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="6e916-144">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="6e916-145">Set-AzureRmVMSourceImage</span><span class="sxs-lookup"><span data-stu-id="6e916-145">Set-AzureRmVMSourceImage</span></span>](/powershell/module/azurerm.resources/set-azurermvmsourceimage)                           | <span data-ttu-id="6e916-146">Указывает образ для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="6e916-146">Specifies an image for a virtual machine.</span></span>                                                                                                                                            |
| [<span data-ttu-id="6e916-147">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="6e916-147">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.resources/set-azurermvmosdisk)                                     | <span data-ttu-id="6e916-148">Задает свойства диска операционной системы для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="6e916-148">Sets the operating system disk properties on a virtual machine.</span></span>                                                                                                                      |
| [<span data-ttu-id="6e916-149">Set-AzureRmVMOperatingSystem</span><span class="sxs-lookup"><span data-stu-id="6e916-149">Set-AzureRmVMOperatingSystem</span></span>](/powershell/module/azurerm.resources/set-azurermvmoperatingsystem)                   | <span data-ttu-id="6e916-150">Задает свойства диска операционной системы для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="6e916-150">Sets the operating system disk properties on a virtual machine.</span></span>                                                                                                                      |
| [<span data-ttu-id="6e916-151">Add-AzureRmVMNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="6e916-151">Add-AzureRmVMNetworkInterface</span></span>](/powershell/module/azurerm.resources/add-azurermvmnetworkinterface)                 | <span data-ttu-id="6e916-152">Добавляет сетевой интерфейс для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="6e916-152">Adds a network interface to a virtual machine.</span></span>                                                                                                                                       |
| [<span data-ttu-id="6e916-153">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="6e916-153">New-AzureRmVM</span></span>](/powershell/module/azurerm.resources/new-azurermvm)                                                 | <span data-ttu-id="6e916-154">Создайте виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="6e916-154">Create a virtual machine.</span></span>                                                                                                                                                            |
| [<span data-ttu-id="6e916-155">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6e916-155">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup)                     | <span data-ttu-id="6e916-156">Удаляет группу ресурсов и все ресурсы, содержащиеся в ней.</span><span class="sxs-lookup"><span data-stu-id="6e916-156">Removes a resource group and all resources contained within.</span></span>                                                                                                                         |

## <a name="next-steps"></a><span data-ttu-id="6e916-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6e916-157">Next steps</span></span>

<span data-ttu-id="6e916-158">Дополнительные сведения о модуле Azure PowerShell см. в [документации по Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6e916-158">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="6e916-159">Дополнительные примеры сценариев PowerShell для виртуальных машин представлены в [документации по виртуальным машинам Azure под управлением Windows](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6e916-159">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
