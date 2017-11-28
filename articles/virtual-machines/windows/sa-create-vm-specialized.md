---
title: "aaaCreate виртуальной Машины из специализированного диска в Azure | Документы Microsoft"
description: "Создание новой виртуальной Машины путем присоединения неуправляемые специализированного диска, в модели развертывания диспетчера ресурсов hello."
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
ms.openlocfilehash: c88f213b6629a6c1d6ff5845e76c2f7719672714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-specialized-vhd-in-a-storage-account"></a><span data-ttu-id="9af76-103">Создание виртуальной машины на основе специализированного VHD в учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="9af76-103">Create a VM from a specialized VHD in a storage account</span></span>

<span data-ttu-id="9af76-104">Создание новой виртуальной Машины путем присоединения специализированный неуправляемым диск как диск ОС hello, с помощью Powershell.</span><span class="sxs-lookup"><span data-stu-id="9af76-104">Create a new VM by attaching a specialized unmanaged disk as hello OS disk using Powershell.</span></span> <span data-ttu-id="9af76-105">Специализированного диска представляет собой копию виртуального жесткого диска из существующей виртуальной Машины, который поддерживает учетные записи пользователей hello, приложений и других данных о состоянии из исходной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="9af76-105">A specialized disk is a copy of VHD from an existing VM that maintains hello user accounts, applications and other state data from your original VM.</span></span> 

<span data-ttu-id="9af76-106">Существует два варианта.</span><span class="sxs-lookup"><span data-stu-id="9af76-106">You have two options:</span></span>
* [<span data-ttu-id="9af76-107">Передача VHD</span><span class="sxs-lookup"><span data-stu-id="9af76-107">Upload a VHD</span></span>](create-vm-specialized.md#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="9af76-108">Скопируйте hello виртуальный жесткий ДИСК существующей виртуальной Машине Azure</span><span class="sxs-lookup"><span data-stu-id="9af76-108">Copy hello VHD of an existing Azure VM</span></span>](create-vm-specialized.md#option-2-copy-an-existing-azure-vm)

## <a name="before-you-begin"></a><span data-ttu-id="9af76-109">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="9af76-109">Before you begin</span></span>
<span data-ttu-id="9af76-110">При использовании PowerShell убедитесь, что последняя версия модуля AzureRM.Compute PowerShell hello hello.</span><span class="sxs-lookup"><span data-stu-id="9af76-110">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="9af76-111">Запустите hello следующие tooinstall команды.</span><span class="sxs-lookup"><span data-stu-id="9af76-111">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute 
```
<span data-ttu-id="9af76-112">Дополнительные сведения см. в разделе [об управлении версиями Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9af76-112">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="option-1-upload-a-specialized-vhd"></a><span data-ttu-id="9af76-113">Вариант 1. Передача специализированного VHD</span><span class="sxs-lookup"><span data-stu-id="9af76-113">Option 1: Upload a specialized VHD</span></span>

<span data-ttu-id="9af76-114">Можно передать hello создания виртуального жесткого диска от виртуальной Машины, специализированный со средством виртуализации в локальной среде, как Hyper-V или виртуальной Машины экспортирован из другого облака.</span><span class="sxs-lookup"><span data-stu-id="9af76-114">You can upload hello VHD from a specialized VM created with an on-premises virtualization tool, like Hyper-V, or a VM exported from another cloud.</span></span>

### <a name="prepare-hello-vm"></a><span data-ttu-id="9af76-115">Подготовка виртуальной Машины hello</span><span class="sxs-lookup"><span data-stu-id="9af76-115">Prepare hello VM</span></span>
<span data-ttu-id="9af76-116">Вы можете передать специализированный VHD, созданный с помощью локальной виртуальной машины, или VHD, экспортированный из другого облака.</span><span class="sxs-lookup"><span data-stu-id="9af76-116">You can upload a specialized VHD that was created using an on-premises VM or a VHD exported from another cloud.</span></span> <span data-ttu-id="9af76-117">Специализированные виртуальный жесткий ДИСК поддерживает учетные записи пользователей hello, приложений и других данных о состоянии из исходной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="9af76-117">A specialized VHD maintains hello user accounts, applications and other state data from your original VM.</span></span> <span data-ttu-id="9af76-118">Если предполагается toouse hello VHD как-является toocreate новой виртуальной Машины, убедитесь, выполняются следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="9af76-118">If you intend toouse hello VHD as-is toocreate a new VM, ensure hello following steps are completed.</span></span> 
  
  * <span data-ttu-id="9af76-119">[Подготовка виртуального жесткого диска Windows tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9af76-119">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="9af76-120">**Нет** generalize hello виртуальную Машину с помощью Sysprep.</span><span class="sxs-lookup"><span data-stu-id="9af76-120">**Do not** generalize hello VM using Sysprep.</span></span>
  * <span data-ttu-id="9af76-121">Удалите все гостевой средств виртуализации и агентов, установленных на hello виртуальной Машины (т. е. средства VMware).</span><span class="sxs-lookup"><span data-stu-id="9af76-121">Remove any guest virtualization tools and agents that are installed on hello VM (i.e. VMware tools).</span></span>
  * <span data-ttu-id="9af76-122">Обеспечить hello виртуальной Машины является настроенным toopull его IP-адрес и параметры DNS через DHCP.</span><span class="sxs-lookup"><span data-stu-id="9af76-122">Ensure hello VM is configured toopull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="9af76-123">Это гарантирует, что этот сервер hello получает IP-адрес в пределах hello виртуальной сети при запуске.</span><span class="sxs-lookup"><span data-stu-id="9af76-123">This ensures that hello server obtains an IP address within hello VNet when it starts up.</span></span> 


### <a name="get-hello-storage-account"></a><span data-ttu-id="9af76-124">Получение учетной записи хранилища hello</span><span class="sxs-lookup"><span data-stu-id="9af76-124">Get hello storage account</span></span>
<span data-ttu-id="9af76-125">Требуется учетная запись хранения в образе виртуальной Машины Azure toostore hello отправлен.</span><span class="sxs-lookup"><span data-stu-id="9af76-125">You need a storage account in Azure toostore hello uploaded VM image.</span></span> <span data-ttu-id="9af76-126">Можно использовать существующую учетную запись хранения или создать новую.</span><span class="sxs-lookup"><span data-stu-id="9af76-126">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="9af76-127">tooshow hello доступных учетных записей хранилища, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="9af76-127">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="9af76-128">Toouse существующую учетную запись хранения следует продолжить toohello [загрузку образа виртуальной Машины hello](#upload-the-vm-vhd-to-your-storage-account) раздела.</span><span class="sxs-lookup"><span data-stu-id="9af76-128">If you want toouse an existing storage account, proceed toohello [Upload hello VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="9af76-129">Если вам требуется toocreate учетной записи хранилища, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="9af76-129">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="9af76-130">Требуется имя hello hello группы ресурсов, которой должен быть создан hello учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="9af76-130">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="9af76-131">toofind out все hello группы ресурсов в вашей подписке типа:</span><span class="sxs-lookup"><span data-stu-id="9af76-131">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="9af76-132">Группа ресурсов с именем toocreate **myResourceGroup** в hello **Запад США** региона, введите:</span><span class="sxs-lookup"><span data-stu-id="9af76-132">toocreate a resource group named **myResourceGroup** in hello **West US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="9af76-133">Создать учетную запись хранилища с именем **mystorageaccount** в этой группе ресурсов с помощью hello [New AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) командлета:</span><span class="sxs-lookup"><span data-stu-id="9af76-133">Create a storage account named **mystorageaccount** in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
### <a name="upload-hello-vhd-tooyour-storage-account"></a><span data-ttu-id="9af76-134">Отправка виртуального жесткого диска для hello tooyour учетной записи хранилища</span><span class="sxs-lookup"><span data-stu-id="9af76-134">Upload hello VHD tooyour storage account</span></span>
<span data-ttu-id="9af76-135">Используйте hello [AzureRmVhd добавить](/powershell/module/azurerm.compute/add-azurermvhd) контейнера командлет tooupload hello изображения tooa вашей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="9af76-135">Use hello [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello image tooa container in your storage account.</span></span> <span data-ttu-id="9af76-136">В этом примере файл hello передачи **myVHD.vhd** из `"C:\Users\Public\Documents\Virtual hard disks\"` tooa учетной записи хранилища с именем **mystorageaccount** в hello **myResourceGroup** группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9af76-136">This example uploads hello file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` tooa storage account named **mystorageaccount** in hello **myResourceGroup** resource group.</span></span> <span data-ttu-id="9af76-137">Hello файла будут помещены в контейнер hello **mycontainer** и hello новый файл будет называться **myUploadedVHD.vhd**.</span><span class="sxs-lookup"><span data-stu-id="9af76-137">hello file will be placed into hello container named **mycontainer** and hello new file name will be **myUploadedVHD.vhd**.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="9af76-138">В случае успешного выполнения вы получаете ответ, который выглядит примерно toothis:</span><span class="sxs-lookup"><span data-stu-id="9af76-138">If successful, you get a response that looks similar toothis:</span></span>

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

<span data-ttu-id="9af76-139">В зависимости от сетевого подключения и hello размер файла виртуального жесткого диска, эта команда может занять некоторое время toocomplete.</span><span class="sxs-lookup"><span data-stu-id="9af76-139">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete.</span></span>


## <a name="option-2-copy-hello-vhd-from-an-existing-azure-vm"></a><span data-ttu-id="9af76-140">Вариант 2: Скопируйте hello виртуального жесткого диска из существующей виртуальной Машине Azure</span><span class="sxs-lookup"><span data-stu-id="9af76-140">Option 2: Copy hello VHD from an existing Azure VM</span></span>

<span data-ttu-id="9af76-141">При создании новой, повторяющиеся ВМ можно скопировать toouse учетной записи хранилища tooanother виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="9af76-141">You can copy a VHD tooanother storage account toouse when creating a new, duplicate VM.</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="9af76-142">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="9af76-142">Before you begin</span></span>
<span data-ttu-id="9af76-143">Убедитесь, что выполнены следующие условия.</span><span class="sxs-lookup"><span data-stu-id="9af76-143">Make sure that you:</span></span>

* <span data-ttu-id="9af76-144">Сведения о hello **источника и назначения учетных записей хранения**.</span><span class="sxs-lookup"><span data-stu-id="9af76-144">Have information about hello **source and destination storage accounts**.</span></span> <span data-ttu-id="9af76-145">Hello исходной виртуальной Машины необходимо toohave hello учетной записи и контейнер имена хранилища.</span><span class="sxs-lookup"><span data-stu-id="9af76-145">For hello source VM, you need toohave hello storage account and container names.</span></span> <span data-ttu-id="9af76-146">Как правило, будет имя контейнера hello **виртуальные жесткие диски**.</span><span class="sxs-lookup"><span data-stu-id="9af76-146">Usually, hello container name will be **vhds**.</span></span> <span data-ttu-id="9af76-147">Необходимо также toohave целевой учетной записью хранения.</span><span class="sxs-lookup"><span data-stu-id="9af76-147">You also need toohave a destination storage account.</span></span> <span data-ttu-id="9af76-148">Если у вас еще нет один, можно создать один с помощью портала hello (**более служб** > учетные записи хранения > Добавить) или с помощью hello [New AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) командлета.</span><span class="sxs-lookup"><span data-stu-id="9af76-148">If you don't already have one, you can create one using either hello portal (**More Services** > Storage accounts > Add) or using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet.</span></span> 
* <span data-ttu-id="9af76-149">Загружено и установлено hello [средство AzCopy](../../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="9af76-149">Have downloaded and installed hello [AzCopy tool](../../storage/common/storage-use-azcopy.md).</span></span> 

### <a name="deallocate-hello-vm"></a><span data-ttu-id="9af76-150">DEALLOCATE hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="9af76-150">Deallocate hello VM</span></span>
<span data-ttu-id="9af76-151">Неудачная попытка освобождения hello виртуальную Машину, которая освобождает toobe VHD hello копируются.</span><span class="sxs-lookup"><span data-stu-id="9af76-151">Deallocate hello VM, which frees up hello VHD toobe copied.</span></span> 

* <span data-ttu-id="9af76-152">**Портал**: щелкните **Виртуальные машины** > **myVM** > Остановить</span><span class="sxs-lookup"><span data-stu-id="9af76-152">**Portal**: Click **Virtual machines** > **myVM** > Stop</span></span>
* <span data-ttu-id="9af76-153">**PowerShell**: использование [Stop AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) toostop (освобождении) виртуальной Машины с именем hello **myVM** в группе ресурсов **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="9af76-153">**Powershell**: Use [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) toostop (deallocate) hello VM named **myVM** in resource group **myResourceGroup**.</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

<span data-ttu-id="9af76-154">Hello **состояние** для hello ВМ в hello Azure портал изменения из **остановлена** слишком**остановлена (освобождена)**.</span><span class="sxs-lookup"><span data-stu-id="9af76-154">hello **Status** for hello VM in hello Azure portal changes from **Stopped** too**Stopped (deallocated)**.</span></span>

### <a name="get-hello-storage-account-urls"></a><span data-ttu-id="9af76-155">Получение URL-адреса учетной записи хранилища hello</span><span class="sxs-lookup"><span data-stu-id="9af76-155">Get hello storage account URLs</span></span>
<span data-ttu-id="9af76-156">Требуется URL-адреса hello hello источника и назначения учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="9af76-156">You need hello URLs of hello source and destination storage accounts.</span></span> <span data-ttu-id="9af76-157">Hello URL-адреса выглядеть следующим образом: `https://<storageaccount>.blob.core.windows.net/<containerName>/`.</span><span class="sxs-lookup"><span data-stu-id="9af76-157">hello URLs look like: `https://<storageaccount>.blob.core.windows.net/<containerName>/`.</span></span> <span data-ttu-id="9af76-158">Если известно имя учетной записи и контейнера хранилища hello, можно просто замените hello информации между toocreate скобки hello URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="9af76-158">If you already know hello storage account and container name, you can just replace hello information between hello brackets toocreate your URL.</span></span> 

<span data-ttu-id="9af76-159">Можно использовать hello портал Azure или Azure Powershell tooget hello, URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="9af76-159">You can use hello Azure portal or Azure Powershell tooget hello URL:</span></span>

* <span data-ttu-id="9af76-160">**Портал**: щелкните hello  **>**  для **дополнительные службы** > **учетные записи хранения**  >   *Учетная запись хранения* > **большие двоичные объекты** и исходного файла виртуального жесткого диска, возможно, находится в hello **виртуальные жесткие диски** контейнера.</span><span class="sxs-lookup"><span data-stu-id="9af76-160">**Portal**: Click hello **>** for **More services** > **Storage accounts** > *storage account* > **Blobs** and your source VHD file is probably in hello **vhds** container.</span></span> <span data-ttu-id="9af76-161">Нажмите кнопку **свойства** для контейнера hello и копировать текст hello с меткой **URL-адрес**.</span><span class="sxs-lookup"><span data-stu-id="9af76-161">Click **Properties** for hello container, and copy hello text labeled **URL**.</span></span> <span data-ttu-id="9af76-162">Вам потребуется hello URL-адреса источника и назначения контейнеров обеих hello.</span><span class="sxs-lookup"><span data-stu-id="9af76-162">You'll need hello URLs of both hello source and destination containers.</span></span> 
* <span data-ttu-id="9af76-163">**PowerShell**: использование [Get AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) tooget hello сведения для виртуальной Машины с именем **myVM** в группе ресурсов hello **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="9af76-163">**Powershell**: Use [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) tooget hello information for VM named **myVM** in hello resource group **myResourceGroup**.</span></span> <span data-ttu-id="9af76-164">В результатах hello папка hello **профиль хранилища** раздел для hello **Uri VHD-файла**.</span><span class="sxs-lookup"><span data-stu-id="9af76-164">In hello results, look in hello **Storage profile** section for hello **Vhd Uri**.</span></span> <span data-ttu-id="9af76-165">Первая часть Hello hello Uri — контейнер toohello hello URL-адрес и hello последней части — hello имени виртуального жесткого диска операционной системы для виртуальной Машины hello.</span><span class="sxs-lookup"><span data-stu-id="9af76-165">hello first part of hello Uri is hello URL toohello container and hello last part is hello OS VHD name for hello VM.</span></span>

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
``` 

## <a name="get-hello-storage-access-keys"></a><span data-ttu-id="9af76-166">Получить ключи доступа к хранилищу hello</span><span class="sxs-lookup"><span data-stu-id="9af76-166">Get hello storage access keys</span></span>
<span data-ttu-id="9af76-167">Найти hello ключи доступа для hello источника и назначения учетные записи хранения.</span><span class="sxs-lookup"><span data-stu-id="9af76-167">Find hello access keys for hello source and destination storage accounts.</span></span> <span data-ttu-id="9af76-168">Дополнительные сведения о ключах доступа см. в статье [Об учетных записях хранения Azure](../../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="9af76-168">For more information about access keys, see [About Azure storage accounts](../../storage/common/storage-create-storage-account.md).</span></span>

* <span data-ttu-id="9af76-169">**Портал.** Щелкните **Больше служб** > **Учетные записи хранения** > *учетная запись хранения* > **Ключи доступа**.</span><span class="sxs-lookup"><span data-stu-id="9af76-169">**Portal**: Click **More services** > **Storage accounts** > *storage account* > **Access keys**.</span></span> <span data-ttu-id="9af76-170">Копировать ключ hello помечены как **key1**.</span><span class="sxs-lookup"><span data-stu-id="9af76-170">Copy hello key labeled as **key1**.</span></span>
* <span data-ttu-id="9af76-171">**PowerShell**: использование [Get AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) tooget hello хранилища ключ учетной записи хранения hello **mystorageaccount** в группе ресурсов hello  **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="9af76-171">**Powershell**: Use [Get-AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) tooget hello storage key for hello storage account **mystorageaccount** in hello resource group **myResourceGroup**.</span></span> <span data-ttu-id="9af76-172">Копировать hello ключ с меткой **key1**.</span><span class="sxs-lookup"><span data-stu-id="9af76-172">Copy hello key labeled **key1**.</span></span>

```powershell
Get-AzureRmStorageAccountKey -Name mystorageaccount -ResourceGroupName myResourceGroup
```

### <a name="copy-hello-vhd"></a><span data-ttu-id="9af76-173">Скопируйте hello виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="9af76-173">Copy hello VHD</span></span>
<span data-ttu-id="9af76-174">С помощью AzCopy можно копировать файлы между учетными записями хранения.</span><span class="sxs-lookup"><span data-stu-id="9af76-174">You can copy files between storage accounts using AzCopy.</span></span> <span data-ttu-id="9af76-175">Для hello конечный контейнер Если hello указанный контейнер не существует, он создается автоматически.</span><span class="sxs-lookup"><span data-stu-id="9af76-175">For hello destination container, if hello specified container doesn't exist, it will be created for you.</span></span> 

<span data-ttu-id="9af76-176">toouse AzCopy, откройте командную строку на локальном компьютере и перейдите в папку toohello для установки AzCopy.</span><span class="sxs-lookup"><span data-stu-id="9af76-176">toouse AzCopy, open a command prompt on your local machine and navigate toohello folder where AzCopy is installed.</span></span> <span data-ttu-id="9af76-177">Он будет выглядеть слишком*\Microsoft SDKs\Azure\AzCopy C:\Program Files (x86)*.</span><span class="sxs-lookup"><span data-stu-id="9af76-177">It will be similar too*C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy*.</span></span> 

<span data-ttu-id="9af76-178">toocopy hello все файлы в контейнере, используйте hello **/S** переключения.</span><span class="sxs-lookup"><span data-stu-id="9af76-178">toocopy all of hello files within a container, you use hello **/S** switch.</span></span> <span data-ttu-id="9af76-179">Это может быть hello используется toocopy виртуального жесткого диска операционной системы и Здравствуйте, все диски данных hello, если они находятся в одном контейнере.</span><span class="sxs-lookup"><span data-stu-id="9af76-179">This can be used toocopy hello OS VHD and all of hello data disks if they are in hello same container.</span></span> <span data-ttu-id="9af76-180">В этом примере показано, как все hello файлы в контейнере hello toocopy **mysourcecontainer** в учетной записи хранения **mysourcestorageaccount** toohello контейнера **mydestinationcontainer**  в hello **mydestinationstorageaccount** учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="9af76-180">This example shows how toocopy all of hello files in hello container **mysourcecontainer** in storage account **mysourcestorageaccount** toohello container **mydestinationcontainer** in hello **mydestinationstorageaccount** storage account.</span></span> <span data-ttu-id="9af76-181">Замените приветствия имен учетных записей хранилища hello и контейнеры свои собственные.</span><span class="sxs-lookup"><span data-stu-id="9af76-181">Replace hello names of hello storage accounts and containers with your own.</span></span> <span data-ttu-id="9af76-182">Замените ключи `<sourceStorageAccountKey1>` и `<destinationStorageAccountKey1>` своими собственными.</span><span class="sxs-lookup"><span data-stu-id="9af76-182">Replace `<sourceStorageAccountKey1>` and `<destinationStorageAccountKey1>` with your own keys.</span></span>

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
    /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
    /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> /S
```

<span data-ttu-id="9af76-183">Требуется только toocopy конкретного виртуального жесткого диска в контейнере с несколькими файлами, также можно указать имя файла hello, с помощью переключателя /Pattern hello.</span><span class="sxs-lookup"><span data-stu-id="9af76-183">If you only want toocopy a specific VHD in a container with multiple files, you can also specify hello file name using hello /Pattern switch.</span></span> <span data-ttu-id="9af76-184">В этом примере hello только файл с именем **myFileName.vhd** будут скопированы.</span><span class="sxs-lookup"><span data-stu-id="9af76-184">In this example, only hello file named **myFileName.vhd** will be copied.</span></span>

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
  /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
  /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> `
  /Pattern:myFileName.vhd
```


<span data-ttu-id="9af76-185">По завершении отобразится сообщение следующего вида:</span><span class="sxs-lookup"><span data-stu-id="9af76-185">When it is finished, you will get a message that looks something like:</span></span>

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

### <a name="troubleshooting"></a><span data-ttu-id="9af76-186">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="9af76-186">Troubleshooting</span></span>
* <span data-ttu-id="9af76-187">При использовании AZCopy, при возникновении ошибки hello «Серверу не удалось tooauthenticate hello запроса», убедитесь, что hello значение заголовка авторизации hello имеет правильный формат, включая подпись hello.</span><span class="sxs-lookup"><span data-stu-id="9af76-187">When you use AZCopy, if you see hello error "Server failed tooauthenticate hello request", make sure hello value of hello Authorization header is formed correctly including hello signature.</span></span> <span data-ttu-id="9af76-188">При использовании 2 ключ или ключ hello дополнительного хранилища, попробуйте использовать ключ хранилища первичной или 1-го hello.</span><span class="sxs-lookup"><span data-stu-id="9af76-188">If you are using Key 2 or hello secondary storage key, try using hello primary or 1st storage key.</span></span>

## <a name="create-hello-new-vm"></a><span data-ttu-id="9af76-189">Создание новой виртуальной Машины hello</span><span class="sxs-lookup"><span data-stu-id="9af76-189">Create hello new VM</span></span> 

<span data-ttu-id="9af76-190">Требуется toocreate сети и другие ресурсы toobe виртуальных Машин, используемых hello новой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="9af76-190">You need toocreate networking and other VM resources toobe used by hello new VM.</span></span>

### <a name="create-hello-subnet-and-vnet"></a><span data-ttu-id="9af76-191">Создание подсети hello и виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="9af76-191">Create hello subNet and vNet</span></span>

<span data-ttu-id="9af76-192">Создание виртуальной сети hello и подсеть hello [виртуальной сети](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9af76-192">Create hello vNet and subNet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="9af76-193">Создайте подсеть hello.</span><span class="sxs-lookup"><span data-stu-id="9af76-193">Create hello subNet.</span></span> <span data-ttu-id="9af76-194">В этом примере создается подсеть с именем **mySubNet**, в группе ресурсов hello **myResourceGroup**, и задает hello префикс адреса подсети слишком**10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="9af76-194">This example creates a subnet named **mySubNet**, in hello resource group **myResourceGroup**, and sets hello subnet address prefix too**10.0.0.0/24**.</span></span>
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubNet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="9af76-195">Создание виртуальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="9af76-195">Create hello vNet.</span></span> <span data-ttu-id="9af76-196">В этом примере задает hello toobe имя виртуальной сети **myVnetName**, hello расположение слишком**Запад США**, и hello префикс адреса для виртуальной сети hello слишком**10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="9af76-196">This example sets hello virtual network name toobe **myVnetName**, hello location too**West US**, and hello address prefix for hello virtual network too**10.0.0.0/16**.</span></span> 
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnetName"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-nic"></a><span data-ttu-id="9af76-197">Создание общедоступного IP-адреса и сетевой карты</span><span class="sxs-lookup"><span data-stu-id="9af76-197">Create a public IP address and NIC</span></span>
<span data-ttu-id="9af76-198">требуется tooenable взаимодействия с виртуальной машиной hello в виртуальной сети hello, [общедоступный IP-адрес](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) и сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="9af76-198">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="9af76-199">Создайте hello общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="9af76-199">Create hello public IP.</span></span> <span data-ttu-id="9af76-200">В этом примере имя hello открытый IP-адреса задано слишком**myIP**.</span><span class="sxs-lookup"><span data-stu-id="9af76-200">In this example, hello public IP address name is set too**myIP**.</span></span>
   
    ```powershell
    $ipName = "myIP"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="9af76-201">Создайте сетевую карту hello.</span><span class="sxs-lookup"><span data-stu-id="9af76-201">Create hello NIC.</span></span> <span data-ttu-id="9af76-202">В этом примере имя сетевого Адаптера hello задано слишком**myNicName**.</span><span class="sxs-lookup"><span data-stu-id="9af76-202">In this example, hello NIC name is set too**myNicName**.</span></span>
   
    ```powershell
    $nicName = "myNicName"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="9af76-203">Создание группы безопасности сети hello и правило протокола удаленного рабочего СТОЛА</span><span class="sxs-lookup"><span data-stu-id="9af76-203">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="9af76-204">возможности toolog toobe в tooyour виртуальную Машину с помощью протокола удаленного рабочего СТОЛА, необходимо toohave правило безопасности, которое разрешает доступ RDP через порт 3389.</span><span class="sxs-lookup"><span data-stu-id="9af76-204">toobe able toolog in tooyour VM using RDP, you need toohave an security rule that allows RDP access on port 3389.</span></span> <span data-ttu-id="9af76-205">Поскольку специальным hello виртуального жесткого диска для создания новой виртуальной Машины из существующего hello виртуальной Машины, после создания вы hello виртуальной Машины можно использовать существующую учетную запись из hello исходной виртуальной машины было toolog разрешение на использование протокола удаленного рабочего СТОЛА.</span><span class="sxs-lookup"><span data-stu-id="9af76-205">Because hello VHD for hello new VM was created from an existing specialized VM, after hello VM is created you can use an existing account from hello source virtual machine that had permission toolog on using RDP.</span></span>
<span data-ttu-id="9af76-206">В этом примере задает hello NSG имя слишком**myNsg** и hello RDP имя правила слишком**myRdpRule**.</span><span class="sxs-lookup"><span data-stu-id="9af76-206">This example sets hello NSG name too**myNsg** and hello RDP rule name too**myRdpRule**.</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

<span data-ttu-id="9af76-207">Дополнительные сведения о конечных точках и правила NSG см. в разделе [Открытие портов tooa ВМ в Azure с помощью PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9af76-207">For more information about endpoints and NSG rules, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="set-hello-vm-name-and-size"></a><span data-ttu-id="9af76-208">Задайте имя виртуальной Машины hello и размер</span><span class="sxs-lookup"><span data-stu-id="9af76-208">Set hello VM name and size</span></span>

<span data-ttu-id="9af76-209">В этом примере задает hello имя виртуальной Машины слишком «myVM» и hello ВМ размер слишком «Standard_A2».</span><span class="sxs-lookup"><span data-stu-id="9af76-209">This example sets hello VM name too"myVM" and hello VM size too"Standard_A2".</span></span>
```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a><span data-ttu-id="9af76-210">Добавить hello сетевого Адаптера</span><span class="sxs-lookup"><span data-stu-id="9af76-210">Add hello NIC</span></span>
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    
    
### <a name="configure-hello-os-disk"></a><span data-ttu-id="9af76-211">Настройка диска hello ОС</span><span class="sxs-lookup"><span data-stu-id="9af76-211">Configure hello OS disk</span></span>

1. <span data-ttu-id="9af76-212">Задайте hello URI для виртуального жесткого диска, загруженного или скопированного hello.</span><span class="sxs-lookup"><span data-stu-id="9af76-212">Set hello URI for hello VHD that you uploaded or copied.</span></span> <span data-ttu-id="9af76-213">В этом примере hello VHD-файл с именем **myOsDisk.vhd** сохраняется в учетную запись хранения с именем **myStorageAccount** в контейнер с именем **myContainer**.</span><span class="sxs-lookup"><span data-stu-id="9af76-213">In this example, hello VHD file named **myOsDisk.vhd** is kept in a storage account named **myStorageAccount** in a container named **myContainer**.</span></span>

    ```powershell
    $osDiskUri = "https://myStorageAccount.blob.core.windows.net/myContainer/myOsDisk.vhd"
    ```
2. <span data-ttu-id="9af76-214">Добавьте диск hello ОС.</span><span class="sxs-lookup"><span data-stu-id="9af76-214">Add hello OS disk.</span></span> <span data-ttu-id="9af76-215">В этом примере при создании диска ОС hello hello термин «osDisk» — appened toohello ВМ имя toocreate hello имя диска ОС.</span><span class="sxs-lookup"><span data-stu-id="9af76-215">In this example, when hello OS disk is created, hello term "osDisk" is appened toohello VM name toocreate hello OS disk name.</span></span> <span data-ttu-id="9af76-216">В этом примере также указывает, этого виртуального жесткого диска на основе Windows должно быть вложенных toohello виртуальную Машину в качестве диска ОС hello.</span><span class="sxs-lookup"><span data-stu-id="9af76-216">This example also specifies that this Windows-based VHD should be attached toohello VM as hello OS disk.</span></span>
    
    ```powershell
    $osDiskName = $vmName + "osDisk"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption attach -Windows
    ```

<span data-ttu-id="9af76-217">Необязательно: При наличии дисков с данными, toobe необходимость присоединенного toohello виртуальной Машины, добавьте hello диски с данными с помощью URL-адреса hello данных виртуальные жесткие диски и hello соответствующий логический номер устройства (Lun).</span><span class="sxs-lookup"><span data-stu-id="9af76-217">Optional: If you have data disks that need toobe attached toohello VM, add hello data disks by using hello URLs of data VHDs and hello appropriate Logical Unit Number (Lun).</span></span>

```powershell
$dataDiskName = $vmName + "dataDisk"
$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -VhdUri $dataDiskUri -Lun 1 -CreateOption attach
```

<span data-ttu-id="9af76-218">При использовании учетной записи хранилища, hello данные и URL-адреса для диска операционной системы выглядеть примерно следующим образом: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`.</span><span class="sxs-lookup"><span data-stu-id="9af76-218">When using a storage account, hello data and operating system disk URLs look something like this: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`.</span></span> <span data-ttu-id="9af76-219">Его можно найти на портале hello путем просмотра контейнера хранилища целевой toohello, щелкнув hello операционной системы или виртуального жесткого диска, который был скопирован, данные и скопировав в нее содержимое hello hello URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="9af76-219">You can find this on hello portal by browsing toohello target storage container, clicking hello operating system or data VHD that was copied, and then copying hello contents of hello URL.</span></span>


### <a name="complete-hello-vm"></a><span data-ttu-id="9af76-220">Завершить hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="9af76-220">Complete hello VM</span></span> 

<span data-ttu-id="9af76-221">Создайте виртуальную Машину с помощью hello конфигураций, которые мы только что создали hello.</span><span class="sxs-lookup"><span data-stu-id="9af76-221">Create hello VM using hello configurations that we just created.</span></span>

```powershell
#Create hello new VM
New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

<span data-ttu-id="9af76-222">Если команда будет выполнена успешно, вы увидите примерно такой результат.</span><span class="sxs-lookup"><span data-stu-id="9af76-222">If this command was successful, you'll see output like this:</span></span>

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="9af76-223">Убедитесь, что hello создания виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="9af76-223">Verify that hello VM was created</span></span>
<span data-ttu-id="9af76-224">Вы увидите hello вновь созданные ВМ в hello [портал Azure](https://portal.azure.com)в разделе **Обзор** > **виртуальные машины**, или с помощью следующих PowerShell hello команды:</span><span class="sxs-lookup"><span data-stu-id="9af76-224">You should see hello newly created VM either in hello [Azure portal](https://portal.azure.com), under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $rgName
$vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="9af76-225">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9af76-225">Next steps</span></span>
<span data-ttu-id="9af76-226">toosign в новой виртуальной машины tooyour, toohello обзор виртуальных Машин в hello [портала](https://portal.azure.com), нажмите кнопку **Connect**и откройте hello файл удаленного рабочего СТОЛА.</span><span class="sxs-lookup"><span data-stu-id="9af76-226">toosign in tooyour new virtual machine, browse toohello VM in hello [portal](https://portal.azure.com), click **Connect**, and open hello Remote Desktop RDP file.</span></span> <span data-ttu-id="9af76-227">Используйте учетные данные учетной записи hello объекта к исходной виртуальной машины toosign tooyour новой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="9af76-227">Use hello account credentials of your original virtual machine toosign in tooyour new virtual machine.</span></span> <span data-ttu-id="9af76-228">Дополнительные сведения см. в разделе [как tooconnect и вход в систему tooan Azure виртуальные машины под управлением Windows](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="9af76-228">For more information, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md).</span></span>

