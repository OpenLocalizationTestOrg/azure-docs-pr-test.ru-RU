---
title: "aaaCreate виртуальной Машине Windows на основе специализированного VHD в Azure | Документы Microsoft"
description: "Создание новой виртуальной Машины Windows путем присоединения специализированного диска управляемых как диска ОС hello, использование в модели развертывания диспетчера ресурсов hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3b7d3cd5-e3d7-4041-a2a7-0290447458ea
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: cynthn
ms.openlocfilehash: c72c6f4fb650e2664e87cf38ec9be62f0b2209fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-vm-from-a-specialized-disk"></a><span data-ttu-id="08cce-103">Создание виртуальной машины Windows из специализированного диска</span><span class="sxs-lookup"><span data-stu-id="08cce-103">Create a Windows VM from a specialized disk</span></span>

<span data-ttu-id="08cce-104">Создание новой виртуальной Машины путем присоединения специализированного диска управляемых как диска ОС hello, с помощью Powershell.</span><span class="sxs-lookup"><span data-stu-id="08cce-104">Create a new VM by attaching a specialized managed disk as hello OS disk using Powershell.</span></span> <span data-ttu-id="08cce-105">Специализированного диска представляет собой копию виртуального жесткого диска (VHD) из существующей виртуальной Машины, который поддерживает учетные записи пользователей hello, приложений и других данных о состоянии из исходной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="08cce-105">A specialized disk is a copy of virtual hard disk (VHD) from an existing VM that maintains hello user accounts, applications, and other state data from your original VM.</span></span> 

<span data-ttu-id="08cce-106">При использовании специализированных toocreate виртуального жесткого диска новой виртуальной Машины, приветствия новой виртуальной Машины сохраняет имя компьютера hello hello исходной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="08cce-106">When you use a specialized VHD toocreate a new VM, hello new VM retains hello computer name of hello original VM.</span></span> <span data-ttu-id="08cce-107">Другие сведения о компьютере также сохраняются и в некоторых случаях эти повторяющиеся данные могут вызвать проблемы.</span><span class="sxs-lookup"><span data-stu-id="08cce-107">Other computer-specific information is also be kept and, in some cases, this duplicate information could cause issues.</span></span> <span data-ttu-id="08cce-108">Следует учитывать, какие типы сведений о компьютере используют приложения при копировании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="08cce-108">Be aware of what types of computer-specific information your applications rely on when copying a VM.</span></span>

<span data-ttu-id="08cce-109">Существует два варианта.</span><span class="sxs-lookup"><span data-stu-id="08cce-109">You have two options:</span></span>
* [<span data-ttu-id="08cce-110">Передача VHD</span><span class="sxs-lookup"><span data-stu-id="08cce-110">Upload a VHD</span></span>](#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="08cce-111">Копирование имеющейся виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="08cce-111">Copy an existing Azure VM</span></span>](#option-2-copy-an-existing-azure-vm)

<span data-ttu-id="08cce-112">В этом разделе показано, как toouse Управление дисками.</span><span class="sxs-lookup"><span data-stu-id="08cce-112">This topic shows you how toouse managed disks.</span></span> <span data-ttu-id="08cce-113">При наличии развертывания устаревших версий, для которой требуется использовать учетную запись хранения, см. статью [Создание виртуальной машины на основе специализированного VHD в учетной записи хранения](sa-create-vm-specialized.md).</span><span class="sxs-lookup"><span data-stu-id="08cce-113">If you have a legacy deployment that requires using a storage account, see [Create a VM from a specialized VHD in a storage account](sa-create-vm-specialized.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="08cce-114">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="08cce-114">Before you begin</span></span>
<span data-ttu-id="08cce-115">При использовании PowerShell убедитесь, что последняя версия модуля AzureRM.Compute PowerShell hello hello.</span><span class="sxs-lookup"><span data-stu-id="08cce-115">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> 

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="08cce-116">Дополнительные сведения см. в разделе [об управлении версиями Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="08cce-116">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="option-1-upload-a-specialized-vhd"></a><span data-ttu-id="08cce-117">Вариант 1. Передача специализированного VHD</span><span class="sxs-lookup"><span data-stu-id="08cce-117">Option 1: Upload a specialized VHD</span></span>

<span data-ttu-id="08cce-118">Можно передать hello создания виртуального жесткого диска от виртуальной Машины, специализированный со средством виртуализации в локальной среде, как Hyper-V или виртуальной Машины экспортирован из другого облака.</span><span class="sxs-lookup"><span data-stu-id="08cce-118">You can upload hello VHD from a specialized VM created with an on-premises virtualization tool, like Hyper-V, or a VM exported from another cloud.</span></span>

### <a name="prepare-hello-vm"></a><span data-ttu-id="08cce-119">Подготовка виртуальной Машины hello</span><span class="sxs-lookup"><span data-stu-id="08cce-119">Prepare hello VM</span></span>
<span data-ttu-id="08cce-120">Если предполагается toouse hello VHD как-является toocreate новой виртуальной Машины, убедитесь, выполняются следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="08cce-120">If you intend toouse hello VHD as-is toocreate a new VM, ensure hello following steps are completed.</span></span> 
  
  * <span data-ttu-id="08cce-121">[Подготовка виртуального жесткого диска Windows tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="08cce-121">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="08cce-122">**Нет** generalize hello виртуальную Машину с помощью Sysprep.</span><span class="sxs-lookup"><span data-stu-id="08cce-122">**Do not** generalize hello VM using Sysprep.</span></span>
  * <span data-ttu-id="08cce-123">Удалите все гостевой средств виртуализации и агентов, установленных на hello виртуальной Машины (например, средства VMware tools).</span><span class="sxs-lookup"><span data-stu-id="08cce-123">Remove any guest virtualization tools and agents that are installed on hello VM (like VMware tools).</span></span>
  * <span data-ttu-id="08cce-124">Обеспечить hello виртуальной Машины является настроенным toopull его IP-адрес и параметры DNS через DHCP.</span><span class="sxs-lookup"><span data-stu-id="08cce-124">Ensure hello VM is configured toopull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="08cce-125">Это гарантирует, что этот сервер hello получает IP-адрес в пределах hello виртуальной сети при запуске.</span><span class="sxs-lookup"><span data-stu-id="08cce-125">This ensures that hello server obtains an IP address within hello VNet when it starts up.</span></span> 


### <a name="get-hello-storage-account"></a><span data-ttu-id="08cce-126">Получение учетной записи хранилища hello</span><span class="sxs-lookup"><span data-stu-id="08cce-126">Get hello storage account</span></span>
<span data-ttu-id="08cce-127">Требуется хранилище учетной записи в Azure toostore hello отправки виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="08cce-127">You need a storage account in Azure toostore hello uploaded VHD.</span></span> <span data-ttu-id="08cce-128">Можно использовать существующую учетную запись хранения или создать новую.</span><span class="sxs-lookup"><span data-stu-id="08cce-128">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="08cce-129">tooshow hello доступных учетных записей хранилища, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="08cce-129">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="08cce-130">Toouse существующую учетную запись хранения следует продолжить toohello [hello передачи виртуального жесткого диска](#upload-the-vhd-to-your-storage-account) раздела.</span><span class="sxs-lookup"><span data-stu-id="08cce-130">If you want toouse an existing storage account, proceed toohello [Upload hello VHD](#upload-the-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="08cce-131">Если вам требуется toocreate учетной записи хранилища, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="08cce-131">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="08cce-132">Требуется имя hello hello группы ресурсов, которой должен быть создан hello учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="08cce-132">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="08cce-133">toofind out все hello группы ресурсов в вашей подписке типа:</span><span class="sxs-lookup"><span data-stu-id="08cce-133">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="08cce-134">Группа ресурсов с именем toocreate *myResourceGroup* в hello *Запад США* региона, введите:</span><span class="sxs-lookup"><span data-stu-id="08cce-134">toocreate a resource group named *myResourceGroup* in hello *West US* region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="08cce-135">Создать учетную запись хранилища с именем *mystorageaccount* в этой группе ресурсов с помощью hello [New AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) командлета:</span><span class="sxs-lookup"><span data-stu-id="08cce-135">Create a storage account named *mystorageaccount* in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```

### <a name="upload-hello-vhd-tooyour-storage-account"></a><span data-ttu-id="08cce-136">Отправка виртуального жесткого диска для hello tooyour учетной записи хранилища</span><span class="sxs-lookup"><span data-stu-id="08cce-136">Upload hello VHD tooyour storage account</span></span> 
<span data-ttu-id="08cce-137">Используйте hello [AzureRmVhd добавить](/powershell/module/azurerm.compute/add-azurermvhd) командлет tooupload hello VHD tooa контейнера в учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="08cce-137">Use hello [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello VHD tooa container in your storage account.</span></span> <span data-ttu-id="08cce-138">В этом примере файл hello передачи *myVHD.vhd* из `"C:\Users\Public\Documents\Virtual hard disks\"` tooa учетной записи хранилища с именем *mystorageaccount* в hello *myResourceGroup* группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="08cce-138">This example uploads hello file *myVHD.vhd* from `"C:\Users\Public\Documents\Virtual hard disks\"` tooa storage account named *mystorageaccount* in hello *myResourceGroup* resource group.</span></span> <span data-ttu-id="08cce-139">Hello файл сохраняется в контейнер hello *mycontainer* и hello новый файл будет называться *myUploadedVHD.vhd*.</span><span class="sxs-lookup"><span data-stu-id="08cce-139">hello file is stored in hello container named *mycontainer* and hello new file name will be *myUploadedVHD.vhd*.</span></span>

```powershell
$resourceGroupName = "myResourceGroup"
$urlOfUploadedVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $resourceGroupName -Destination $urlOfUploadedVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="08cce-140">В случае успешного выполнения вы получаете ответ, который выглядит примерно toothis:</span><span class="sxs-lookup"><span data-stu-id="08cce-140">If successful, you get a response that looks similar toothis:</span></span>

```powershell
MD5 hash is being calculated for hello file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for hello operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

<span data-ttu-id="08cce-141">В зависимости от сетевого подключения и hello размер файла виртуального жесткого диска, эта команда может занять некоторое время toocomplete</span><span class="sxs-lookup"><span data-stu-id="08cce-141">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete</span></span>

### <a name="create-a-managed-disk-from-hello-vhd"></a><span data-ttu-id="08cce-142">Создание управляемого диска из hello виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="08cce-142">Create a managed disk from hello VHD</span></span>

<span data-ttu-id="08cce-143">Создание управляемого диска из hello специализированные VHD в учетной записи хранилища с помощью [New AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span><span class="sxs-lookup"><span data-stu-id="08cce-143">Create a managed disk from hello specialized VHD in your storage account using [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span></span> <span data-ttu-id="08cce-144">В этом примере используется **myOSDisk1** для hello имя диска, помещает hello диск в *StandardLRS* хранилища, а также используется *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* как hello URI для hello исходного VHD.</span><span class="sxs-lookup"><span data-stu-id="08cce-144">This example uses **myOSDisk1** for hello disk name, puts hello disk in *StandardLRS* storage, and uses *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* as hello URI for hello source VHD.</span></span>

<span data-ttu-id="08cce-145">Создать новую группу ресурсов для hello новой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="08cce-145">Create a new resource group for hello new VM.</span></span>

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

<span data-ttu-id="08cce-146">Создать новый диск ОС hello из hello отправки виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="08cce-146">Create hello new OS disk from hello uploaded VHD.</span></span> 

```powershell
$sourceUri = https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd)
$osDiskName = 'myOsDisk'
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig -AccountType StandardLRS  -Location $location -CreateOption Import `
    -SourceUri $sourceUri) `
    -ResourceGroupName $destinationResourceGroup
```

## <a name="option-2-copy-an-existing-azure-vm"></a><span data-ttu-id="08cce-147">Вариант 2. Копирование существующей виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="08cce-147">Option 2: Copy an existing Azure VM</span></span>

<span data-ttu-id="08cce-148">Можно создать копию виртуальной Машины, которая использует управляемый дисков с помощью снимка виртуальной Машины hello, то с помощью этого моментального снимка toocreate нового управляемого диска и новой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="08cce-148">You can create a copy of a VM that uses managed disks by taking a snapshot of hello VM, then using that snapshot toocreate a new managed disk and a new VM.</span></span>


### <a name="take-a-snapshot-of-hello-os-disk"></a><span data-ttu-id="08cce-149">Создание снимка hello диска ОС</span><span class="sxs-lookup"><span data-stu-id="08cce-149">Take a snapshot of hello OS disk</span></span>

<span data-ttu-id="08cce-150">Вы можете сделать моментальный снимок всей виртуальной машины (включая все диски) или одного диска.</span><span class="sxs-lookup"><span data-stu-id="08cce-150">You can take a snapshot of and entire VM (including all disks) or of just a single disk.</span></span> <span data-ttu-id="08cce-151">Hello следующие шаги показывают, как моментальный снимок виртуальной Машины с помощью только что hello ОС диска tootake hello [New AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot) командлета.</span><span class="sxs-lookup"><span data-stu-id="08cce-151">hello following steps show you how tootake a snapshot of just hello OS disk of your VM using hello [New-AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot) cmdlet.</span></span> 

<span data-ttu-id="08cce-152">Задайте некоторые параметры.</span><span class="sxs-lookup"><span data-stu-id="08cce-152">Set some parameters.</span></span> 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$vmName = 'myVM'
$location = 'westus' 
$snapshotName = 'mySnapshot'  
```

<span data-ttu-id="08cce-153">Получение hello объекта виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="08cce-153">Get hello VM object.</span></span>

```powershell
$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $resourceGroupName
```
<span data-ttu-id="08cce-154">Получите имя диска ОС hello.</span><span class="sxs-lookup"><span data-stu-id="08cce-154">Get hello OS disk name.</span></span>

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $vm.StorageProfile.OsDisk.Name
```

<span data-ttu-id="08cce-155">Создайте конфигурацию hello моментальных снимков.</span><span class="sxs-lookup"><span data-stu-id="08cce-155">Create hello snapshot configuration.</span></span> 

 ```powershell
$snapshotConfig =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -OsType Windows -CreateOption Copy -Location $location 
```

<span data-ttu-id="08cce-156">Снимок "hello".</span><span class="sxs-lookup"><span data-stu-id="08cce-156">Take hello snapshot.</span></span>

```powershell
$snapShot = New-AzureRmSnapshot -Snapshot $snapshotConfig -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName
```


<span data-ttu-id="08cce-157">Если планируется toouse hello моментального снимка toocreate виртуальной Машины, которая должна toobe высокопроизводительной, используйте параметр hello `-AccountType Premium_LRS` с помощью команды New-AzureRmSnapshot hello.</span><span class="sxs-lookup"><span data-stu-id="08cce-157">If you plan toouse hello snapshot toocreate a VM that needs toobe high performing, use hello parameter `-AccountType Premium_LRS` with hello New-AzureRmSnapshot command.</span></span> <span data-ttu-id="08cce-158">параметр Hello создает hello моментальных снимков, чтобы оно хранится как диск управляемых Premium.</span><span class="sxs-lookup"><span data-stu-id="08cce-158">hello parameter creates hello snapshot so that it's stored as a Premium Managed Disk.</span></span> <span data-ttu-id="08cce-159">Управляемые диски уровня "Премиум" дороже, чем управляемые диски уровня "Стандартный".</span><span class="sxs-lookup"><span data-stu-id="08cce-159">Premium Managed Disks are more expensive than Standard.</span></span> <span data-ttu-id="08cce-160">Поэтому убедитесь, что действительно требуется Premium перед использованием параметра hello.</span><span class="sxs-lookup"><span data-stu-id="08cce-160">So be sure you really need Premium before using hello parameter.</span></span>

### <a name="create-a-new-disk-from-hello-snapshot"></a><span data-ttu-id="08cce-161">Создать новый диск из моментального снимка hello</span><span class="sxs-lookup"><span data-stu-id="08cce-161">Create a new disk from hello snapshot</span></span>

<span data-ttu-id="08cce-162">Создание управляемого диска из моментального снимка с помощью hello [New AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span><span class="sxs-lookup"><span data-stu-id="08cce-162">Create a managed disk from hello snapshot using [New-AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk).</span></span> <span data-ttu-id="08cce-163">В этом примере используется *myOSDisk* для hello имя диска.</span><span class="sxs-lookup"><span data-stu-id="08cce-163">This example uses *myOSDisk* for hello disk name.</span></span>

<span data-ttu-id="08cce-164">Создать новую группу ресурсов для hello новой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="08cce-164">Create a new resource group for hello new VM.</span></span>

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

<span data-ttu-id="08cce-165">Задайте имя диска ОС hello.</span><span class="sxs-lookup"><span data-stu-id="08cce-165">Set hello OS disk name.</span></span> 

```powershell
$osDiskName = 'myOsDisk'
```

<span data-ttu-id="08cce-166">Создание управляемого диска hello.</span><span class="sxs-lookup"><span data-stu-id="08cce-166">Create hello managed disk.</span></span>

```powershell
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig  -Location $location -CreateOption Copy `
    -SourceResourceId $snapshot.Id) `
    -ResourceGroupName $destinationResourceGroup
```


## <a name="create-hello-new-vm"></a><span data-ttu-id="08cce-167">Создание новой виртуальной Машины hello</span><span class="sxs-lookup"><span data-stu-id="08cce-167">Create hello new VM</span></span> 

<span data-ttu-id="08cce-168">Создание сети и другие ресурсы toobe виртуальных Машин, используемых hello новой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="08cce-168">Create networking and other VM resources toobe used by hello new VM.</span></span>

### <a name="create-hello-subnet-and-vnet"></a><span data-ttu-id="08cce-169">Создание подсети hello и виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="08cce-169">Create hello subNet and vNet</span></span>

<span data-ttu-id="08cce-170">Создание виртуальной сети hello и подсеть hello [виртуальной сети](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="08cce-170">Create hello vNet and subNet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="08cce-171">Создайте подсеть hello.</span><span class="sxs-lookup"><span data-stu-id="08cce-171">Create hello subNet.</span></span> <span data-ttu-id="08cce-172">В этом примере создается подсеть с именем **mySubNet**, в группе ресурсов hello **myDestinationResourceGroup**, и задает hello префикс адреса подсети слишком**10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="08cce-172">This example creates a subnet named **mySubNet**, in hello resource group **myDestinationResourceGroup**, and sets hello subnet address prefix too**10.0.0.0/24**.</span></span>
   
```powershell
$subnetName = 'mySubNet'
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="08cce-173">Создание виртуальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="08cce-173">Create hello vNet.</span></span> <span data-ttu-id="08cce-174">В этом примере задает hello toobe имя виртуальной сети **myVnetName**, hello расположение слишком**Запад США**, и hello префикс адреса для виртуальной сети hello слишком**10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="08cce-174">This example sets hello virtual network name toobe **myVnetName**, hello location too**West US**, and hello address prefix for hello virtual network too**10.0.0.0/16**.</span></span> 
   
```powershell
$vnetName = "myVnetName"
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $destinationResourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
```    


### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="08cce-175">Создание группы безопасности сети hello и правило протокола удаленного рабочего СТОЛА</span><span class="sxs-lookup"><span data-stu-id="08cce-175">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="08cce-176">возможности toolog toobe в tooyour виртуальную Машину с помощью протокола удаленного рабочего СТОЛА, необходимо toohave правило безопасности, которое разрешает RDP-доступ через порт 3389.</span><span class="sxs-lookup"><span data-stu-id="08cce-176">toobe able toolog in tooyour VM using RDP, you need toohave a security rule that allows RDP access on port 3389.</span></span> <span data-ttu-id="08cce-177">Поскольку hello виртуального жесткого диска для новой виртуальной Машине был создан из существующей виртуальной Машине специализированные hello, вы можете использовать учетную запись из hello исходной виртуальной машины для протокола удаленного рабочего СТОЛА.</span><span class="sxs-lookup"><span data-stu-id="08cce-177">Because hello VHD for hello new VM was created from an existing specialized VM, you can use an account from hello source virtual machine for RDP.</span></span>

<span data-ttu-id="08cce-178">В этом примере задает hello NSG имя слишком**myNsg** и hello RDP имя правила слишком**myRdpRule**.</span><span class="sxs-lookup"><span data-stu-id="08cce-178">This example sets hello NSG name too**myNsg** and hello RDP rule name too**myRdpRule**.</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $destinationResourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

<span data-ttu-id="08cce-179">Дополнительные сведения о конечных точках и правила NSG см. в разделе [Открытие портов tooa ВМ в Azure с помощью PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="08cce-179">For more information about endpoints and NSG rules, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="create-a-public-ip-address-and-nic"></a><span data-ttu-id="08cce-180">Создание общедоступного IP-адреса и сетевой карты</span><span class="sxs-lookup"><span data-stu-id="08cce-180">Create a public IP address and NIC</span></span>
<span data-ttu-id="08cce-181">требуется tooenable взаимодействия с виртуальной машиной hello в виртуальной сети hello, [общедоступный IP-адрес](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) и сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="08cce-181">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

<span data-ttu-id="08cce-182">Создайте hello общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="08cce-182">Create hello public IP.</span></span> <span data-ttu-id="08cce-183">В этом примере имя hello открытый IP-адреса задано слишком**myIP**.</span><span class="sxs-lookup"><span data-stu-id="08cce-183">In this example, hello public IP address name is set too**myIP**.</span></span>
   
```powershell
$ipName = "myIP"
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $destinationResourceGroup -Location $location `
   -AllocationMethod Dynamic
```       

<span data-ttu-id="08cce-184">Создайте сетевую карту hello.</span><span class="sxs-lookup"><span data-stu-id="08cce-184">Create hello NIC.</span></span> <span data-ttu-id="08cce-185">В этом примере имя сетевого Адаптера hello задано слишком**myNicName**.</span><span class="sxs-lookup"><span data-stu-id="08cce-185">In this example, hello NIC name is set too**myNicName**.</span></span>
   
```powershell
$nicName = "myNicName"
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $destinationResourceGroup `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```



### <a name="set-hello-vm-name-and-size"></a><span data-ttu-id="08cce-186">Задайте имя виртуальной Машины hello и размер</span><span class="sxs-lookup"><span data-stu-id="08cce-186">Set hello VM name and size</span></span>

<span data-ttu-id="08cce-187">В этом примере задает hello имя виртуальной Машины слишком*myVM* а hello виртуальной Машины, размер слишком*Standard_A2*.</span><span class="sxs-lookup"><span data-stu-id="08cce-187">This example sets hello VM name too*myVM* and hello VM size too*Standard_A2*.</span></span>

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a><span data-ttu-id="08cce-188">Добавить hello сетевого Адаптера</span><span class="sxs-lookup"><span data-stu-id="08cce-188">Add hello NIC</span></span>
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    

### <a name="add-hello-os-disk"></a><span data-ttu-id="08cce-189">Добавить диск hello ОС</span><span class="sxs-lookup"><span data-stu-id="08cce-189">Add hello OS disk</span></span> 

<span data-ttu-id="08cce-190">Добавить hello ОС диска toohello конфигурации с помощью [AzureRmVMOSDisk набор](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span><span class="sxs-lookup"><span data-stu-id="08cce-190">Add hello OS disk toohello configuration using [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span></span> <span data-ttu-id="08cce-191">В этом примере устанавливается размер hello hello диска слишком*128 ГБ* и присоединяет hello управляемый диск — как *Windows* диска ОС.</span><span class="sxs-lookup"><span data-stu-id="08cce-191">This example sets hello size of hello disk too*128 GB* and attaches hello managed disk as a *Windows* OS disk.</span></span>
 
```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -StorageAccountType StandardLRS `
    -DiskSizeInGB 128 -CreateOption Attach -Windows
```

### <a name="complete-hello-vm"></a><span data-ttu-id="08cce-192">Завершить hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="08cce-192">Complete hello VM</span></span> 

<span data-ttu-id="08cce-193">Создание виртуальной Машины с помощью hello [New AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm)hello конфигураций, которые мы только что создали.</span><span class="sxs-lookup"><span data-stu-id="08cce-193">Create hello VM using [New-AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm)hello configurations that we just created.</span></span>

```powershell
New-AzureRmVM -ResourceGroupName $destinationResourceGroup -Location $location -VM $vm
```

<span data-ttu-id="08cce-194">Если команда будет выполнена успешно, вы увидите примерно такой результат.</span><span class="sxs-lookup"><span data-stu-id="08cce-194">If this command was successful, you'll see output like this:</span></span>

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="08cce-195">Убедитесь, что hello создания виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="08cce-195">Verify that hello VM was created</span></span>
<span data-ttu-id="08cce-196">Вы увидите hello вновь созданные ВМ в hello [портал Azure](https://portal.azure.com)в разделе **Обзор** > **виртуальные машины**, или с помощью следующих PowerShell hello команды:</span><span class="sxs-lookup"><span data-stu-id="08cce-196">You should see hello newly created VM either in hello [Azure portal](https://portal.azure.com), under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $destinationResourceGroup
$vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="08cce-197">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="08cce-197">Next steps</span></span>
<span data-ttu-id="08cce-198">toosign в новой виртуальной машины tooyour, toohello обзор виртуальных Машин в hello [портала](https://portal.azure.com), нажмите кнопку **Connect**и откройте hello файл удаленного рабочего СТОЛА.</span><span class="sxs-lookup"><span data-stu-id="08cce-198">toosign in tooyour new virtual machine, browse toohello VM in hello [portal](https://portal.azure.com), click **Connect**, and open hello Remote Desktop RDP file.</span></span> <span data-ttu-id="08cce-199">Используйте учетные данные учетной записи hello объекта к исходной виртуальной машины toosign tooyour новой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="08cce-199">Use hello account credentials of your original virtual machine toosign in tooyour new virtual machine.</span></span> <span data-ttu-id="08cce-200">Дополнительные сведения см. в разделе [как tooconnect и вход в систему tooan Azure виртуальные машины под управлением Windows](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="08cce-200">For more information, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md).</span></span>

