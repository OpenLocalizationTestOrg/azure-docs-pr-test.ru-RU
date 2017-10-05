---
title: "Создание виртуальной машины на основе специализированного диска в Azure | Документация Майкрософт"
description: "Создание виртуальной машины на основе подключенного специализированного неуправляемого диска в модели развертывания диспетчера ресурсов."
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
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: 974d89aa96cba94fedfd1acbaf4f1d30ac8e6257
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-vm-from-a-specialized-vhd-in-a-storage-account"></a><span data-ttu-id="66d45-103">Создание виртуальной машины на основе специализированного VHD в учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="66d45-103">Create a VM from a specialized VHD in a storage account</span></span>

<span data-ttu-id="66d45-104">Создайте виртуальную машину, подключив специализированный неуправляемый диск в качестве диска ОС с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="66d45-104">Create a new VM by attaching a specialized unmanaged disk as the OS disk using Powershell.</span></span> <span data-ttu-id="66d45-105">Специализированный диск — это копия виртуального жесткого диска виртуальной машины, в которой сохраняются учетные записи пользователей, приложения и другие данные о состоянии исходной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="66d45-105">A specialized disk is a copy of VHD from an existing VM that maintains the user accounts, applications and other state data from your original VM.</span></span> 

<span data-ttu-id="66d45-106">Существует два варианта.</span><span class="sxs-lookup"><span data-stu-id="66d45-106">You have two options:</span></span>
* [<span data-ttu-id="66d45-107">Передача VHD</span><span class="sxs-lookup"><span data-stu-id="66d45-107">Upload a VHD</span></span>](create-vm-specialized.md#option-1-upload-a-specialized-vhd)
* <span data-ttu-id="66d45-108">[Копирование VHD, имеющейся виртуальной машины Azure](create-vm-specialized.md#option-2-copy-an-existing-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="66d45-108">[Copy the VHD of an existing Azure VM](create-vm-specialized.md#option-2-copy-an-existing-azure-vm)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="66d45-109">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="66d45-109">Before you begin</span></span>
<span data-ttu-id="66d45-110">Если вы используете PowerShell, убедитесь, что у вас установлена последняя версия модуля PowerShell AzureRM.Compute.</span><span class="sxs-lookup"><span data-stu-id="66d45-110">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="66d45-111">Выполните следующую команду, чтобы установить ее.</span><span class="sxs-lookup"><span data-stu-id="66d45-111">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute 
```
<span data-ttu-id="66d45-112">Дополнительные сведения см. в разделе [об управлении версиями Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="66d45-112">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="option-1-upload-a-specialized-vhd"></a><span data-ttu-id="66d45-113">Вариант 1. Передача специализированного VHD</span><span class="sxs-lookup"><span data-stu-id="66d45-113">Option 1: Upload a specialized VHD</span></span>

<span data-ttu-id="66d45-114">Вы можете передать VHD из специализированной виртуальной машины, созданной с помощью локального средства виртуализации, например, Hyper-V или виртуальная машина, экспортированная из другого облака.</span><span class="sxs-lookup"><span data-stu-id="66d45-114">You can upload the VHD from a specialized VM created with an on-premises virtualization tool, like Hyper-V, or a VM exported from another cloud.</span></span>

### <a name="prepare-the-vm"></a><span data-ttu-id="66d45-115">Подготовка виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="66d45-115">Prepare the VM</span></span>
<span data-ttu-id="66d45-116">Вы можете передать специализированный VHD, созданный с помощью локальной виртуальной машины, или VHD, экспортированный из другого облака.</span><span class="sxs-lookup"><span data-stu-id="66d45-116">You can upload a specialized VHD that was created using an on-premises VM or a VHD exported from another cloud.</span></span> <span data-ttu-id="66d45-117">На специализированном VHD сохраняются учетные записи пользователей, приложения и другие данные о состоянии исходной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="66d45-117">A specialized VHD maintains the user accounts, applications and other state data from your original VM.</span></span> <span data-ttu-id="66d45-118">Если вы планируете использовать виртуальный жесткий диск "как есть" для создания виртуальной машины, то необходимо выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="66d45-118">If you intend to use the VHD as-is to create a new VM, ensure the following steps are completed.</span></span> 
  
  * <span data-ttu-id="66d45-119">[Подготовьте виртуальный жесткий диск Windows к передаче в Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="66d45-119">[Prepare a Windows VHD to upload to Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="66d45-120">**Не выполняйте** подготовку виртуальной машины к использованию с помощью Sysprep.</span><span class="sxs-lookup"><span data-stu-id="66d45-120">**Do not** generalize the VM using Sysprep.</span></span>
  * <span data-ttu-id="66d45-121">Удалите все гостевые инструменты и агенты виртуализации, которые установлены на виртуальной машине (т. е. инструменты VMware).</span><span class="sxs-lookup"><span data-stu-id="66d45-121">Remove any guest virtualization tools and agents that are installed on the VM (i.e. VMware tools).</span></span>
  * <span data-ttu-id="66d45-122">Убедитесь, что виртуальная машина настроена на получение IP-адреса и параметров DNS через DHCP.</span><span class="sxs-lookup"><span data-stu-id="66d45-122">Ensure the VM is configured to pull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="66d45-123">Таким образом, сервер будет получать IP-адрес в виртуальной сети при запуске.</span><span class="sxs-lookup"><span data-stu-id="66d45-123">This ensures that the server obtains an IP address within the VNet when it starts up.</span></span> 


### <a name="get-the-storage-account"></a><span data-ttu-id="66d45-124">Получение учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="66d45-124">Get the storage account</span></span>
<span data-ttu-id="66d45-125">Вам необходима учетная запись хранения Azure для хранения переданного образа виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="66d45-125">You need a storage account in Azure to store the uploaded VM image.</span></span> <span data-ttu-id="66d45-126">Можно использовать существующую учетную запись хранения или создать новую.</span><span class="sxs-lookup"><span data-stu-id="66d45-126">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="66d45-127">Чтобы отобразить список доступных учетных записей хранения, введите:</span><span class="sxs-lookup"><span data-stu-id="66d45-127">To show the available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="66d45-128">Если вы хотите использовать существующую учетную запись хранения, то перейдите к разделу [Отправка образа виртуальной машины](#upload-the-vm-vhd-to-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="66d45-128">If you want to use an existing storage account, proceed to the [Upload the VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="66d45-129">Если требуется создать учетную запись хранения, то выполните описанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="66d45-129">If you need to create a storage account, follow these steps:</span></span>

1. <span data-ttu-id="66d45-130">Необходимо указать имя группы ресурсов, в которой будет создана учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="66d45-130">You need the name of the resource group where the storage account should be created.</span></span> <span data-ttu-id="66d45-131">Чтобы найти все группы ресурсов, существующие в вашей подписке, введите:</span><span class="sxs-lookup"><span data-stu-id="66d45-131">To find out all the resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="66d45-132">Чтобы создать группу ресурсов с именем **myResourceGroup** в регионе **Западная часть США**, введите:</span><span class="sxs-lookup"><span data-stu-id="66d45-132">To create a resource group named **myResourceGroup** in the **West US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="66d45-133">С помощью командлета [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) создайте в этой группе ресурсов учетную запись хранения с именем **mystorageaccount**:</span><span class="sxs-lookup"><span data-stu-id="66d45-133">Create a storage account named **mystorageaccount** in this resource group by using the [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
### <a name="upload-the-vhd-to-your-storage-account"></a><span data-ttu-id="66d45-134">Передача виртуального жесткого диска в учетную запись хранения</span><span class="sxs-lookup"><span data-stu-id="66d45-134">Upload the VHD to your storage account</span></span>
<span data-ttu-id="66d45-135">Используйте командлет [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd), чтобы передать образ в контейнер в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="66d45-135">Use the [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet to upload the image to a container in your storage account.</span></span> <span data-ttu-id="66d45-136">В этом примере файл **myVHD.vhd** передается из расположения `"C:\Users\Public\Documents\Virtual hard disks\"` в учетную запись хранения **mystorageaccount**, входящую в группу ресурсов **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="66d45-136">This example uploads the file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` to a storage account named **mystorageaccount** in the **myResourceGroup** resource group.</span></span> <span data-ttu-id="66d45-137">Файл будет помещен в контейнер с именем **mycontainer**; новое имя файла — **myUploadedVHD.vhd**.</span><span class="sxs-lookup"><span data-stu-id="66d45-137">The file will be placed into the container named **mycontainer** and the new file name will be **myUploadedVHD.vhd**.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="66d45-138">В случае успешного выполнения отобразится ответ, который выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="66d45-138">If successful, you get a response that looks similar to this:</span></span>

```powershell
MD5 hash is being calculated for the file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for the operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

<span data-ttu-id="66d45-139">В зависимости от сетевого подключения и размера VHD-файла выполнение этой команды может занять некоторое время.</span><span class="sxs-lookup"><span data-stu-id="66d45-139">Depending on your network connection and the size of your VHD file, this command may take a while to complete.</span></span>


## <a name="option-2-copy-the-vhd-from-an-existing-azure-vm"></a><span data-ttu-id="66d45-140">Вариант 2. Копирование VHD из имеющейся виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="66d45-140">Option 2: Copy the VHD from an existing Azure VM</span></span>

<span data-ttu-id="66d45-141">Вы можете скопировать VHD в другую учетную запись хранения, чтобы использовать его при создании дублируемых виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="66d45-141">You can copy a VHD to another storage account to use when creating a new, duplicate VM.</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="66d45-142">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="66d45-142">Before you begin</span></span>
<span data-ttu-id="66d45-143">Убедитесь, что выполнены следующие условия.</span><span class="sxs-lookup"><span data-stu-id="66d45-143">Make sure that you:</span></span>

* <span data-ttu-id="66d45-144">У вас есть сведения об **исходной и целевой учетных записях хранения**.</span><span class="sxs-lookup"><span data-stu-id="66d45-144">Have information about the **source and destination storage accounts**.</span></span> <span data-ttu-id="66d45-145">Для исходной виртуальной машины необходимы имена учетной записи хранения и контейнера.</span><span class="sxs-lookup"><span data-stu-id="66d45-145">For the source VM, you need to have the storage account and container names.</span></span> <span data-ttu-id="66d45-146">Как правило, имя контейнера — **vhds**.</span><span class="sxs-lookup"><span data-stu-id="66d45-146">Usually, the container name will be **vhds**.</span></span> <span data-ttu-id="66d45-147">Необходимо также иметь целевую учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="66d45-147">You also need to have a destination storage account.</span></span> <span data-ttu-id="66d45-148">Если вы ее еще не создали, то это можно сделать через портал (**Больше служб** > Учетные записи хранения > Добавить) или с помощью командлета [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount).</span><span class="sxs-lookup"><span data-stu-id="66d45-148">If you don't already have one, you can create one using either the portal (**More Services** > Storage accounts > Add) or using the [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet.</span></span> 
* <span data-ttu-id="66d45-149">Вы скачали и установили [инструмент AzCopy](../../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="66d45-149">Have downloaded and installed the [AzCopy tool](../../storage/common/storage-use-azcopy.md).</span></span> 

### <a name="deallocate-the-vm"></a><span data-ttu-id="66d45-150">Освобождение виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="66d45-150">Deallocate the VM</span></span>
<span data-ttu-id="66d45-151">Освободите виртуальную машину, что позволит скопировать VHD.</span><span class="sxs-lookup"><span data-stu-id="66d45-151">Deallocate the VM, which frees up the VHD to be copied.</span></span> 

* <span data-ttu-id="66d45-152">**Портал**: щелкните **Виртуальные машины** > **myVM** > Остановить</span><span class="sxs-lookup"><span data-stu-id="66d45-152">**Portal**: Click **Virtual machines** > **myVM** > Stop</span></span>
* <span data-ttu-id="66d45-153">**PowerShell.** Выполните командлет [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm), чтобы остановить виртуальную машину с именем **myVM** или отменить ее подготовку в группе ресурсов **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="66d45-153">**Powershell**: Use [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) to stop (deallocate) the VM named **myVM** in resource group **myResourceGroup**.</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

<span data-ttu-id="66d45-154">**Состояние** виртуальной машины на портале Azure изменится с **Остановлено** на **Остановлено (освобождено)**.</span><span class="sxs-lookup"><span data-stu-id="66d45-154">The **Status** for the VM in the Azure portal changes from **Stopped** to **Stopped (deallocated)**.</span></span>

### <a name="get-the-storage-account-urls"></a><span data-ttu-id="66d45-155">Получение URL-адресов учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="66d45-155">Get the storage account URLs</span></span>
<span data-ttu-id="66d45-156">Необходимо получить URL-адреса исходной и целевой учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="66d45-156">You need the URLs of the source and destination storage accounts.</span></span> <span data-ttu-id="66d45-157">URL-адреса выглядят следующим образом: `https://<storageaccount>.blob.core.windows.net/<containerName>/`.</span><span class="sxs-lookup"><span data-stu-id="66d45-157">The URLs look like: `https://<storageaccount>.blob.core.windows.net/<containerName>/`.</span></span> <span data-ttu-id="66d45-158">Если вы уже знаете имена учетной записи хранения и контейнера, то можете просто подставить эти данные в скобки, чтобы создать URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="66d45-158">If you already know the storage account and container name, you can just replace the information between the brackets to create your URL.</span></span> 

<span data-ttu-id="66d45-159">Для получения URL-адреса можно использовать портал Azure или Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="66d45-159">You can use the Azure portal or Azure Powershell to get the URL:</span></span>

* <span data-ttu-id="66d45-160">**Портал.** Щелкните **>** **Больше служб** > **Учетные записи хранения** > *учетная запись хранения* > **Большие двоичные объекты**. Ваш исходный VHD-файл скорее всего будет находиться в контейнере **vhds**.</span><span class="sxs-lookup"><span data-stu-id="66d45-160">**Portal**: Click the **>** for **More services** > **Storage accounts** > *storage account* > **Blobs** and your source VHD file is probably in the **vhds** container.</span></span> <span data-ttu-id="66d45-161">Щелкните **Свойства** контейнера и скопируйте текст с пометкой **URL-адрес**.</span><span class="sxs-lookup"><span data-stu-id="66d45-161">Click **Properties** for the container, and copy the text labeled **URL**.</span></span> <span data-ttu-id="66d45-162">Вам понадобятся URL-адреса исходного и целевого контейнеров.</span><span class="sxs-lookup"><span data-stu-id="66d45-162">You'll need the URLs of both the source and destination containers.</span></span> 
* <span data-ttu-id="66d45-163">**PowerShell.** Выполните командлет [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm), чтобы получить сведения о виртуальной машине с именем **myVM** в группе ресурсов **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="66d45-163">**Powershell**: Use [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) to get the information for VM named **myVM** in the resource group **myResourceGroup**.</span></span> <span data-ttu-id="66d45-164">В результатах просмотрите раздел **Storage profile** (Профиль хранилища) и найдите в нем **URI VHD**.</span><span class="sxs-lookup"><span data-stu-id="66d45-164">In the results, look in the **Storage profile** section for the **Vhd Uri**.</span></span> <span data-ttu-id="66d45-165">Первая часть URI является URL-адресом контейнера, а последняя часть — именем VHD операционной системы для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="66d45-165">The first part of the Uri is the URL to the container and the last part is the OS VHD name for the VM.</span></span>

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
``` 

## <a name="get-the-storage-access-keys"></a><span data-ttu-id="66d45-166">Получение ключей доступа к хранилищу</span><span class="sxs-lookup"><span data-stu-id="66d45-166">Get the storage access keys</span></span>
<span data-ttu-id="66d45-167">Найдите ключи доступа для исходной и целевой учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="66d45-167">Find the access keys for the source and destination storage accounts.</span></span> <span data-ttu-id="66d45-168">Дополнительные сведения о ключах доступа см. в статье [Об учетных записях хранения Azure](../../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="66d45-168">For more information about access keys, see [About Azure storage accounts](../../storage/common/storage-create-storage-account.md).</span></span>

* <span data-ttu-id="66d45-169">**Портал.** Щелкните **Больше служб** > **Учетные записи хранения** > *учетная запись хранения* > **Ключи доступа**.</span><span class="sxs-lookup"><span data-stu-id="66d45-169">**Portal**: Click **More services** > **Storage accounts** > *storage account* > **Access keys**.</span></span> <span data-ttu-id="66d45-170">Скопируйте ключ с пометкой **key1**.</span><span class="sxs-lookup"><span data-stu-id="66d45-170">Copy the key labeled as **key1**.</span></span>
* <span data-ttu-id="66d45-171">**PowerShell.** Выполните командлет [Get-AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey), чтобы получить сведения о ключе к хранилищу данных для учетной записи хранения **mystorageaccount** в группе ресурсов **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="66d45-171">**Powershell**: Use [Get-AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) to get the storage key for the storage account **mystorageaccount** in the resource group **myResourceGroup**.</span></span> <span data-ttu-id="66d45-172">Скопируйте ключ с пометкой **key1**.</span><span class="sxs-lookup"><span data-stu-id="66d45-172">Copy the key labeled **key1**.</span></span>

```powershell
Get-AzureRmStorageAccountKey -Name mystorageaccount -ResourceGroupName myResourceGroup
```

### <a name="copy-the-vhd"></a><span data-ttu-id="66d45-173">Копирование виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="66d45-173">Copy the VHD</span></span>
<span data-ttu-id="66d45-174">С помощью AzCopy можно копировать файлы между учетными записями хранения.</span><span class="sxs-lookup"><span data-stu-id="66d45-174">You can copy files between storage accounts using AzCopy.</span></span> <span data-ttu-id="66d45-175">Если у вас нет указанного целевого контейнера, то он будет создан для вас.</span><span class="sxs-lookup"><span data-stu-id="66d45-175">For the destination container, if the specified container doesn't exist, it will be created for you.</span></span> 

<span data-ttu-id="66d45-176">Чтобы воспользоваться AzCopy, откройте окно командной строки на локальном компьютере и перейдите к папке, в которой установлен инструмент AzCopy.</span><span class="sxs-lookup"><span data-stu-id="66d45-176">To use AzCopy, open a command prompt on your local machine and navigate to the folder where AzCopy is installed.</span></span> <span data-ttu-id="66d45-177">Это будет папка вида *C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy*.</span><span class="sxs-lookup"><span data-stu-id="66d45-177">It will be similar to *C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy*.</span></span> 

<span data-ttu-id="66d45-178">Чтобы скопировать все файлы внутри контейнера, используйте параметр **/S**.</span><span class="sxs-lookup"><span data-stu-id="66d45-178">To copy all of the files within a container, you use the **/S** switch.</span></span> <span data-ttu-id="66d45-179">Это действие можно использовать для копирования VHD операционной системы и всех дисков данных, если они находятся в одном контейнере.</span><span class="sxs-lookup"><span data-stu-id="66d45-179">This can be used to copy the OS VHD and all of the data disks if they are in the same container.</span></span> <span data-ttu-id="66d45-180">В этом примере показано, как скопировать все файлы из контейнера **mysourcecontainer** в учетной записи хранения **mysourcestorageaccount** в контейнер **mydestinationcontainer** в учетной записи хранения **mydestinationstorageaccount**.</span><span class="sxs-lookup"><span data-stu-id="66d45-180">This example shows how to copy all of the files in the container **mysourcecontainer** in storage account **mysourcestorageaccount** to the container **mydestinationcontainer** in the **mydestinationstorageaccount** storage account.</span></span> <span data-ttu-id="66d45-181">Замените имена учетных записей хранения и контейнеров своими собственными.</span><span class="sxs-lookup"><span data-stu-id="66d45-181">Replace the names of the storage accounts and containers with your own.</span></span> <span data-ttu-id="66d45-182">Замените ключи `<sourceStorageAccountKey1>` и `<destinationStorageAccountKey1>` своими собственными.</span><span class="sxs-lookup"><span data-stu-id="66d45-182">Replace `<sourceStorageAccountKey1>` and `<destinationStorageAccountKey1>` with your own keys.</span></span>

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
    /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
    /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> /S
```

<span data-ttu-id="66d45-183">Если требуется скопировать только один VHD из контейнера с несколькими файлами, то можно указать имя файла с помощью параметра /Pattern.</span><span class="sxs-lookup"><span data-stu-id="66d45-183">If you only want to copy a specific VHD in a container with multiple files, you can also specify the file name using the /Pattern switch.</span></span> <span data-ttu-id="66d45-184">В данном примере будет скопирован только файл с именем **myFileName.vhd**.</span><span class="sxs-lookup"><span data-stu-id="66d45-184">In this example, only the file named **myFileName.vhd** will be copied.</span></span>

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
  /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
  /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> `
  /Pattern:myFileName.vhd
```


<span data-ttu-id="66d45-185">По завершении отобразится сообщение следующего вида:</span><span class="sxs-lookup"><span data-stu-id="66d45-185">When it is finished, you will get a message that looks something like:</span></span>

```
Finished 2 of total 2 file(s).
[2016/10/07 17:37:41] Transfer summary:
-----------------
Total files transferred: 2
Transfer successfully:   2
Transfer skipped:        0
Transfer failed:         0
Elapsed time:            00.00:13:07
```

### <a name="troubleshooting"></a><span data-ttu-id="66d45-186">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="66d45-186">Troubleshooting</span></span>
* <span data-ttu-id="66d45-187">Если при использовании AZCopy отображается сообщение об ошибке "Серверу не удалось проверить подлинность этого запроса", убедитесь, что значение заголовка авторизации составлено правильно (содержит подпись).</span><span class="sxs-lookup"><span data-stu-id="66d45-187">When you use AZCopy, if you see the error "Server failed to authenticate the request", make sure the value of the Authorization header is formed correctly including the signature.</span></span> <span data-ttu-id="66d45-188">Если используется ключ key2 или вторичный ключ к хранилищу данных, попробуйте воспользоваться первичным ключом или первым ключом к хранилищу данных.</span><span class="sxs-lookup"><span data-stu-id="66d45-188">If you are using Key 2 or the secondary storage key, try using the primary or 1st storage key.</span></span>

## <a name="create-the-new-vm"></a><span data-ttu-id="66d45-189">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="66d45-189">Create the new VM</span></span> 

<span data-ttu-id="66d45-190">Необходимо создать сетевые ресурсы и другие ресурсы виртуальной машины, которые будет использовать новая виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="66d45-190">You need to create networking and other VM resources to be used by the new VM.</span></span>

### <a name="create-the-subnet-and-vnet"></a><span data-ttu-id="66d45-191">Создание виртуальной сети и подсети</span><span class="sxs-lookup"><span data-stu-id="66d45-191">Create the subNet and vNet</span></span>

<span data-ttu-id="66d45-192">Создайте виртуальную сеть и подсеть [виртуальной сети](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="66d45-192">Create the vNet and subNet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="66d45-193">Создайте подсеть.</span><span class="sxs-lookup"><span data-stu-id="66d45-193">Create the subNet.</span></span> <span data-ttu-id="66d45-194">В этом примере создается подсеть с именем **mySubnet** в группе ресурсов **myResourceGroup** и задается префикс адреса подсети **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="66d45-194">This example creates a subnet named **mySubNet**, in the resource group **myResourceGroup**, and sets the subnet address prefix to **10.0.0.0/24**.</span></span>
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubNet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="66d45-195">Создайте виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="66d45-195">Create the vNet.</span></span> <span data-ttu-id="66d45-196">В этом примере задается имя виртуальной сети **myVnetName**, расположение **западная часть США** и префикс адреса виртуальной сети **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="66d45-196">This example sets the virtual network name to be **myVnetName**, the location to **West US**, and the address prefix for the virtual network to **10.0.0.0/16**.</span></span> 
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnetName"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-nic"></a><span data-ttu-id="66d45-197">Создание общедоступного IP-адреса и сетевой карты</span><span class="sxs-lookup"><span data-stu-id="66d45-197">Create a public IP address and NIC</span></span>
<span data-ttu-id="66d45-198">Чтобы обеспечить обмен данными с виртуальной машиной в виртуальной сети, требуются [общедоступный IP-адрес](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) и сетевой интерфейс.</span><span class="sxs-lookup"><span data-stu-id="66d45-198">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="66d45-199">Создайте общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="66d45-199">Create the public IP.</span></span> <span data-ttu-id="66d45-200">В этом примере открытому IP-адресу присвоено имя **myIP**.</span><span class="sxs-lookup"><span data-stu-id="66d45-200">In this example, the public IP address name is set to **myIP**.</span></span>
   
    ```powershell
    $ipName = "myIP"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="66d45-201">Создание сетевой карты.</span><span class="sxs-lookup"><span data-stu-id="66d45-201">Create the NIC.</span></span> <span data-ttu-id="66d45-202">В этом примере сетевой карте присвоено имя **myNicName**.</span><span class="sxs-lookup"><span data-stu-id="66d45-202">In this example, the NIC name is set to **myNicName**.</span></span>
   
    ```powershell
    $nicName = "myNicName"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="66d45-203">Создание группы безопасности сети и правила RDP</span><span class="sxs-lookup"><span data-stu-id="66d45-203">Create the network security group and an RDP rule</span></span>
<span data-ttu-id="66d45-204">Чтобы войти на виртуальную машину по протоколу удаленного рабочего стола, необходимо настроить правило безопасности, которое разрешает доступ по этому протоколу через порт 3389.</span><span class="sxs-lookup"><span data-stu-id="66d45-204">To be able to log in to your VM using RDP, you need to have an security rule that allows RDP access on port 3389.</span></span> <span data-ttu-id="66d45-205">Так как VHD для новой виртуальной машины создан на основе имеющейся специализированной виртуальной машины, то и существующую учетную запись (у которой есть разрешение на вход по протоколу удаленного рабочего стола) можно использовать для обеих этих виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="66d45-205">Because the VHD for the new VM was created from an existing specialized VM, after the VM is created you can use an existing account from the source virtual machine that had permission to log on using RDP.</span></span>
<span data-ttu-id="66d45-206">В этом примере для NSG задается имя **myNsg**, а для правила протокола удаленного рабочего стола — имя **myRdpRule**.</span><span class="sxs-lookup"><span data-stu-id="66d45-206">This example sets the NSG name to **myNsg** and the RDP rule name to **myRdpRule**.</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

<span data-ttu-id="66d45-207">Дополнительные сведения о конечных точках и правилах NSG см. в статье [Открытие портов для виртуальной машины в Azure с помощью PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="66d45-207">For more information about endpoints and NSG rules, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="set-the-vm-name-and-size"></a><span data-ttu-id="66d45-208">Задание имени и размера виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="66d45-208">Set the VM name and size</span></span>

<span data-ttu-id="66d45-209">В этом примере для имени виртуальной машины задается значение myVM, а для ее размера — Standard_A2.</span><span class="sxs-lookup"><span data-stu-id="66d45-209">This example sets the VM name to "myVM" and the VM size to "Standard_A2".</span></span>
```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-the-nic"></a><span data-ttu-id="66d45-210">Добавление сетевой карты</span><span class="sxs-lookup"><span data-stu-id="66d45-210">Add the NIC</span></span>
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    
    
### <a name="configure-the-os-disk"></a><span data-ttu-id="66d45-211">Настройка диска операционной системы</span><span class="sxs-lookup"><span data-stu-id="66d45-211">Configure the OS disk</span></span>

1. <span data-ttu-id="66d45-212">Задайте универсальный код ресурса (URI) VHD, который вы передали или скопировали.</span><span class="sxs-lookup"><span data-stu-id="66d45-212">Set the URI for the VHD that you uploaded or copied.</span></span> <span data-ttu-id="66d45-213">В этом примере VHD-файл **myOsDisk.vhd** хранится в учетной записи **myStorageAccount** в контейнере **myContainer**.</span><span class="sxs-lookup"><span data-stu-id="66d45-213">In this example, the VHD file named **myOsDisk.vhd** is kept in a storage account named **myStorageAccount** in a container named **myContainer**.</span></span>

    ```powershell
    $osDiskUri = "https://myStorageAccount.blob.core.windows.net/myContainer/myOsDisk.vhd"
    ```
2. <span data-ttu-id="66d45-214">Добавьте диск операционной системы.</span><span class="sxs-lookup"><span data-stu-id="66d45-214">Add the OS disk.</span></span> <span data-ttu-id="66d45-215">В этом примере при создании диска ОС к имени виртуальной машины добавляется термин osDisk, формируя таким образом имя диска ОС.</span><span class="sxs-lookup"><span data-stu-id="66d45-215">In this example, when the OS disk is created, the term "osDisk" is appened to the VM name to create the OS disk name.</span></span> <span data-ttu-id="66d45-216">В этом примере также указывается, что этот виртуальный жесткий диск на платформе Windows должен быть подключен к виртуальной машине в качестве диска ОС.</span><span class="sxs-lookup"><span data-stu-id="66d45-216">This example also specifies that this Windows-based VHD should be attached to the VM as the OS disk.</span></span>
    
    ```powershell
    $osDiskName = $vmName + "osDisk"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption attach -Windows
    ```

<span data-ttu-id="66d45-217">(Необязательно.) При наличии дисков данных, которые необходимо подключить к виртуальной машине, добавьте их, используя URL-адреса виртуальных жестких дисков данных и соответствующий логический номер устройства (LUN).</span><span class="sxs-lookup"><span data-stu-id="66d45-217">Optional: If you have data disks that need to be attached to the VM, add the data disks by using the URLs of data VHDs and the appropriate Logical Unit Number (Lun).</span></span>

```powershell
$dataDiskName = $vmName + "dataDisk"
$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -VhdUri $dataDiskUri -Lun 1 -CreateOption attach
```

<span data-ttu-id="66d45-218">При использовании учетной записи хранения URL-адреса дисков данных и дисков ОС выглядят так: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`.</span><span class="sxs-lookup"><span data-stu-id="66d45-218">When using a storage account, the data and operating system disk URLs look something like this: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`.</span></span> <span data-ttu-id="66d45-219">Их можно узнать на портале. Для этого найдите целевой контейнер хранилища, щелкните скопированный виртуальный жесткий диск операционной системы или данных, а затем скопируйте содержимое URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="66d45-219">You can find this on the portal by browsing to the target storage container, clicking the operating system or data VHD that was copied, and then copying the contents of the URL.</span></span>


### <a name="complete-the-vm"></a><span data-ttu-id="66d45-220">Завершение процесса подготовки виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="66d45-220">Complete the VM</span></span> 

<span data-ttu-id="66d45-221">Создайте виртуальную машину, используя созданную конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="66d45-221">Create the VM using the configurations that we just created.</span></span>

```powershell
#Create the new VM
New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

<span data-ttu-id="66d45-222">Если команда будет выполнена успешно, вы увидите примерно такой результат.</span><span class="sxs-lookup"><span data-stu-id="66d45-222">If this command was successful, you'll see output like this:</span></span>

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="66d45-223">Проверка создания виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="66d45-223">Verify that the VM was created</span></span>
<span data-ttu-id="66d45-224">Созданная виртуальная машина должна отображаться на [портале Azure](https://portal.azure.com) (выберите **Обзор** > **Виртуальные машины**). Ее можно также увидеть, выполнив следующие команды PowerShell:</span><span class="sxs-lookup"><span data-stu-id="66d45-224">You should see the newly created VM either in the [Azure portal](https://portal.azure.com), under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $rgName
$vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="66d45-225">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="66d45-225">Next steps</span></span>
<span data-ttu-id="66d45-226">Чтобы войти на новую виртуальную машину, найдите ее на [портале](https://portal.azure.com), нажмите кнопку **Подключение**и откройте RDP-файл "Удаленный рабочий стол".</span><span class="sxs-lookup"><span data-stu-id="66d45-226">To sign in to your new virtual machine, browse to the VM in the [portal](https://portal.azure.com), click **Connect**, and open the Remote Desktop RDP file.</span></span> <span data-ttu-id="66d45-227">Для входа на новую виртуальную машину используйте учетные данные для входа в новую виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="66d45-227">Use the account credentials of your original virtual machine to sign in to your new virtual machine.</span></span> <span data-ttu-id="66d45-228">Дополнительные сведения см. в статье [Как подключиться к виртуальной машине Azure под управлением Windows и войти на нее](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="66d45-228">For more information, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md).</span></span>

