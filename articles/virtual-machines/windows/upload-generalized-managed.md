---
title: "aaaCreate управляемого виртуальной Машины Azure на основе VHD обобщенный локальной | Документы Microsoft"
description: "Отправка обобщенный tooAzure виртуальный жесткий ДИСК и использовать его toocreate новых виртуальных машин, в модели развертывания диспетчера ресурсов hello."
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
ms.date: 05/19/2017
ms.author: cynthn
ms.openlocfilehash: 2fd0c0eec922e6ca8af4e712c1bceb1f9466105c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-and-use-it-toocreate-new-vms-in-azure"></a><span data-ttu-id="536bd-103">Отправка обобщенный виртуальный жесткий ДИСК и использовать его toocreate новые виртуальные машины в Azure</span><span class="sxs-lookup"><span data-stu-id="536bd-103">Upload a generalized VHD and use it toocreate new VMs in Azure</span></span>

<span data-ttu-id="536bd-104">Этот раздел поможет выполнить с помощью PowerShell tooupload VHD обобщенный tooAzure виртуальной Машины, создать образ на hello виртуальный жесткий ДИСК и создать новую виртуальную Машину из этого образа.</span><span class="sxs-lookup"><span data-stu-id="536bd-104">This topic walks you through using PowerShell tooupload a VHD of a generalized VM tooAzure, create an image from hello VHD and create a new VM from that image.</span></span> <span data-ttu-id="536bd-105">Вы можете отправить диск VHD, экспортированный из локального инструмента виртуализации или из другого облака.</span><span class="sxs-lookup"><span data-stu-id="536bd-105">You can upload a VHD exported from an on-premises virtualization tool or from another cloud.</span></span> <span data-ttu-id="536bd-106">С помощью [управляемых дисков](managed-disks-overview.md) для hello новой виртуальной Машины, упрощает управление виртуальными Машинами hello и предоставляет более высокую доступность при помещении hello виртуальной Машины в группу доступности.</span><span class="sxs-lookup"><span data-stu-id="536bd-106">Using [Managed Disks](managed-disks-overview.md) for hello new VM simplifies hello VM managment and provides better availability when hello VM is placed in an availability set.</span></span> 

<span data-ttu-id="536bd-107">Если toouse образец скрипта, см. [образца сценария tooupload tooAzure виртуального жесткого диска и создание новой виртуальной Машины](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)</span><span class="sxs-lookup"><span data-stu-id="536bd-107">If you want toouse a sample script, see [Sample script tooupload a VHD tooAzure and create a new VM](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="536bd-108">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="536bd-108">Before you begin</span></span>

- <span data-ttu-id="536bd-109">Перед отправкой tooAzure любого виртуального жесткого диска, необходимо следовать [Подготовка виртуального жесткого диска Windows или VHDX tooAzure tooupload](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="536bd-109">Before uploading any VHD tooAzure, you should follow [Prepare a Windows VHD or VHDX tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
- <span data-ttu-id="536bd-110">Просмотрите [план миграции hello дисков tooManaged](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) перед началом переноса слишком[управляемых дисков](managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="536bd-110">Review [Plan for hello migration tooManaged Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) before starting your migration too[Managed Disks](managed-disks-overview.md).</span></span>
- <span data-ttu-id="536bd-111">Убедитесь, что последняя версия модуля AzureRM.Compute PowerShell hello hello.</span><span class="sxs-lookup"><span data-stu-id="536bd-111">Make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="536bd-112">Запустите hello следующие tooinstall команды.</span><span class="sxs-lookup"><span data-stu-id="536bd-112">Run hello following command tooinstall it.</span></span>

    ```powershell
    Install-Module AzureRM.Compute -RequiredVersion 2.6.0
    ```
    <span data-ttu-id="536bd-113">Дополнительные сведения см. в разделе [об управлении версиями Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="536bd-113">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="generalize-hello-windows-vm-using-sysprep"></a><span data-ttu-id="536bd-114">Обобщить hello виртуальной Машины Windows с помощью программы Sysprep</span><span class="sxs-lookup"><span data-stu-id="536bd-114">Generalize hello Windows VM using Sysprep</span></span>

<span data-ttu-id="536bd-115">Sysprep удаляет все ваши личные сведения, помимо прочего и подготавливает toobe машины hello, используемое в качестве изображения.</span><span class="sxs-lookup"><span data-stu-id="536bd-115">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="536bd-116">Дополнительные сведения о программе Sysprep см. в разделе [как tooUse Sysprep: введение](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="536bd-116">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="536bd-117">Убедитесь, что на компьютере hello ролей сервера hello поддерживаются программой Sysprep.</span><span class="sxs-lookup"><span data-stu-id="536bd-117">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="536bd-118">Дополнительные сведения см. в статье [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles) (Поддержка серверных ролей в Sysprep).</span><span class="sxs-lookup"><span data-stu-id="536bd-118">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="536bd-119">При запуске средства Sysprep перед отправкой tooAzure вашего виртуального жесткого диска для hello в первый раз убедитесь, что у вас есть [подготовки ВМ](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) перед запуском Sysprep.</span><span class="sxs-lookup"><span data-stu-id="536bd-119">If you are running Sysprep before uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="536bd-120">Войдите в систему toohello виртуальной машины Windows.</span><span class="sxs-lookup"><span data-stu-id="536bd-120">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="536bd-121">Привет открыть окно командной строки с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="536bd-121">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="536bd-122">Измените каталог hello слишком**%windir%\system32\sysprep**, а затем запустите `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="536bd-122">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="536bd-123">В hello **средство подготовки системы** выберите **Enter System Out-of-Box Experience (OOBE)**и убедитесь, что hello **Generalize** установлен флажок.</span><span class="sxs-lookup"><span data-stu-id="536bd-123">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="536bd-124">В разделе **Параметры завершения работы** выберите **Завершение работы**.</span><span class="sxs-lookup"><span data-stu-id="536bd-124">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="536bd-125">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="536bd-125">Click **OK**.</span></span>
   
    ![Запуск Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="536bd-127">По завершении работы программы Sysprep завершает hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="536bd-127">When Sysprep completes, it shuts down hello virtual machine.</span></span> <span data-ttu-id="536bd-128">Не перезагружайте hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="536bd-128">Do not restart hello VM.</span></span>



## <a name="log-in-tooazure"></a><span data-ttu-id="536bd-129">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="536bd-129">Log in tooAzure</span></span>
<span data-ttu-id="536bd-130">Если у вас еще нет PowerShell версии 1.4 или выше установлены, чтение [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="536bd-130">If you don't already have PowerShell version 1.4 or above installed, read [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

1. <span data-ttu-id="536bd-131">Откройте Azure PowerShell и войдите в tooyour учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="536bd-131">Open Azure PowerShell and sign in tooyour Azure account.</span></span> <span data-ttu-id="536bd-132">Откроется всплывающее окно учетные данные учетной записи Azure tooenter вы.</span><span class="sxs-lookup"><span data-stu-id="536bd-132">A pop-up window opens for you tooenter your Azure account credentials.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
2. <span data-ttu-id="536bd-133">Получите подписку hello идентификаторы для доступных подписок.</span><span class="sxs-lookup"><span data-stu-id="536bd-133">Get hello subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="536bd-134">Набор hello нужной подписки с идентификатором hello подписки.</span><span class="sxs-lookup"><span data-stu-id="536bd-134">Set hello correct subscription using hello subscription ID.</span></span> <span data-ttu-id="536bd-135">Замените  *<subscriptionID>*  с Идентификатором hello hello исправить подписки.</span><span class="sxs-lookup"><span data-stu-id="536bd-135">Replace *<subscriptionID>* with hello ID of hello correct subscription.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="get-hello-storage-account"></a><span data-ttu-id="536bd-136">Получение учетной записи хранилища hello</span><span class="sxs-lookup"><span data-stu-id="536bd-136">Get hello storage account</span></span>
<span data-ttu-id="536bd-137">Требуется учетная запись хранения в образе виртуальной Машины Azure toostore hello отправлен.</span><span class="sxs-lookup"><span data-stu-id="536bd-137">You need a storage account in Azure toostore hello uploaded VM image.</span></span> <span data-ttu-id="536bd-138">Можно использовать существующую учетную запись хранения или создать новую.</span><span class="sxs-lookup"><span data-stu-id="536bd-138">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="536bd-139">Если вы будете использовать toocreate VHD hello управляемого диска для виртуальной Машины, hello расположение учетной записи хранения необходимо местоположения hello, в которых будет создаваться hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="536bd-139">If you will be using hello VHD toocreate a managed disk for a VM, hello storage account location must be same hello location where you will be creating hello VM.</span></span>

<span data-ttu-id="536bd-140">tooshow hello доступных учетных записей хранилища, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="536bd-140">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="536bd-141">Toouse существующую учетную запись хранения следует продолжить toohello [загрузку образа виртуальной Машины hello](#upload-the-vm-vhd-to-your-storage-account) раздела.</span><span class="sxs-lookup"><span data-stu-id="536bd-141">If you want toouse an existing storage account, proceed toohello [Upload hello VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="536bd-142">Если вам требуется toocreate учетной записи хранилища, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="536bd-142">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="536bd-143">Требуется имя hello hello группы ресурсов, которой должен быть создан hello учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="536bd-143">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="536bd-144">toofind out все hello группы ресурсов в вашей подписке типа:</span><span class="sxs-lookup"><span data-stu-id="536bd-144">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="536bd-145">Группа ресурсов с именем toocreate **myResourceGroup** в hello **Восток США** региона, введите:</span><span class="sxs-lookup"><span data-stu-id="536bd-145">toocreate a resource group named **myResourceGroup** in hello **East US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "East US"
    ```

2. <span data-ttu-id="536bd-146">Создать учетную запись хранилища с именем **mystorageaccount** в этой группе ресурсов с помощью hello [New AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) командлета:</span><span class="sxs-lookup"><span data-stu-id="536bd-146">Create a storage account named **mystorageaccount** in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "East US"`
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
    <span data-ttu-id="536bd-147">Допустимые значения -SkuName перечислены ниже.</span><span class="sxs-lookup"><span data-stu-id="536bd-147">Valid values for -SkuName are:</span></span>
   
   * <span data-ttu-id="536bd-148">**Standard_LRS** — локально избыточное хранилище.</span><span class="sxs-lookup"><span data-stu-id="536bd-148">**Standard_LRS** - Locally redundant storage.</span></span> 
   * <span data-ttu-id="536bd-149">**Standard_ZRS** — хранилище, избыточное в пределах зоны.</span><span class="sxs-lookup"><span data-stu-id="536bd-149">**Standard_ZRS** - Zone redundant storage.</span></span>
   * <span data-ttu-id="536bd-150">**Standard_GRS** — геоизбыточное хранилище.</span><span class="sxs-lookup"><span data-stu-id="536bd-150">**Standard_GRS** - Geo redundant storage.</span></span> 
   * <span data-ttu-id="536bd-151">**Standard_RAGRS** — геоизбыточное хранилище с доступом только для чтения.</span><span class="sxs-lookup"><span data-stu-id="536bd-151">**Standard_RAGRS** - Read access geo redundant storage.</span></span> 
   * <span data-ttu-id="536bd-152">**Premium_LRS** — локально избыточное хранилище уровня "Премиум".</span><span class="sxs-lookup"><span data-stu-id="536bd-152">**Premium_LRS** - Premium locally redundant storage.</span></span> 

## <a name="upload-hello-vhd-tooyour-storage-account"></a><span data-ttu-id="536bd-153">Отправка виртуального жесткого диска для hello tooyour учетной записи хранилища</span><span class="sxs-lookup"><span data-stu-id="536bd-153">Upload hello VHD tooyour storage account</span></span>

<span data-ttu-id="536bd-154">Используйте hello [AzureRmVhd добавить](https://msdn.microsoft.com/library/mt603554.aspx) командлет tooupload hello VHD tooa контейнера в учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="536bd-154">Use hello [Add-AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) cmdlet tooupload hello VHD tooa container in your storage account.</span></span> <span data-ttu-id="536bd-155">В этом примере файл hello передачи *myVHD.vhd* из *» C:\Users\Public\Documents\Virtual жестких дисков\"*  tooa учетной записи хранилища с именем *mystorageaccount*в hello *myResourceGroup* группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="536bd-155">This example uploads hello file *myVHD.vhd* from *"C:\Users\Public\Documents\Virtual hard disks\"* tooa storage account named *mystorageaccount* in hello *myResourceGroup* resource group.</span></span> <span data-ttu-id="536bd-156">Hello файла будут помещены в контейнер hello *mycontainer* и hello новый файл будет называться *myUploadedVHD.vhd*.</span><span class="sxs-lookup"><span data-stu-id="536bd-156">hello file will be placed into hello container named *mycontainer* and hello new file name will be *myUploadedVHD.vhd*.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="536bd-157">В случае успешного выполнения вы получаете ответ, который выглядит примерно toothis:</span><span class="sxs-lookup"><span data-stu-id="536bd-157">If successful, you get a response that looks similar toothis:</span></span>

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

<span data-ttu-id="536bd-158">В зависимости от сетевого подключения и hello размер файла виртуального жесткого диска, эта команда может занять некоторое время toocomplete</span><span class="sxs-lookup"><span data-stu-id="536bd-158">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete</span></span>

<span data-ttu-id="536bd-159">Сохранить hello **конечный URI** toouse путь к более поздней версии, если вы собираетесь toocreate управляемого диска или новой виртуальной Машины с помощью hello отправлены виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="536bd-159">Save hello **Destination URI** path toouse later if you are going toocreate a managed disk or a new VM using hello uploaded VHD.</span></span>

### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="536bd-160">Другие возможности загрузки виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="536bd-160">Other options for uploading a VHD</span></span>
 
 
<span data-ttu-id="536bd-161">Можно также передать учетную запись хранения tooyour виртуального жесткого диска с помощью одного из следующих hello:</span><span class="sxs-lookup"><span data-stu-id="536bd-161">You can also upload a VHD tooyour storage account using one of hello following:</span></span>

- [<span data-ttu-id="536bd-162">AzCopy</span><span class="sxs-lookup"><span data-stu-id="536bd-162">AzCopy</span></span>](http://aka.ms/downloadazcopy)
- [<span data-ttu-id="536bd-163">API копирования BLOB-объекта хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="536bd-163">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)
- [<span data-ttu-id="536bd-164">Обозреватель хранилищ Azure для передачи больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="536bd-164">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)
- [<span data-ttu-id="536bd-165">Справочник по API REST служб хранилища импорта и экспорта</span><span class="sxs-lookup"><span data-stu-id="536bd-165">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)
-   <span data-ttu-id="536bd-166">Мы рекомендуем использовать службу импорта и экспорта, если предполагаемое время передачи больше 7 дней.</span><span class="sxs-lookup"><span data-stu-id="536bd-166">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="536bd-167">Можно использовать [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate время hello из единицу размера и передачи данных.</span><span class="sxs-lookup"><span data-stu-id="536bd-167">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate hello time from data size and transfer unit.</span></span> 
    <span data-ttu-id="536bd-168">Импорт и экспорт можно использовать toocopy tooa Стандартная учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="536bd-168">Import/Export can be used toocopy tooa standard storage account.</span></span> <span data-ttu-id="536bd-169">Вам потребуется toocopy из учетной записи хранения toopremium стандартного хранилища с помощью таких средств, как AzCopy.</span><span class="sxs-lookup"><span data-stu-id="536bd-169">You will need toocopy from standard storage toopremium storage account using a tool like AzCopy.</span></span>


## <a name="create-a-managed-image-from-hello-uploaded-vhd"></a><span data-ttu-id="536bd-170">Создавать управляемые отправить изображение из hello виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="536bd-170">Create a managed image from hello uploaded VHD</span></span> 

<span data-ttu-id="536bd-171">Создайте управляемый образ с помощью универсального виртуального жесткого диска ОС.</span><span class="sxs-lookup"><span data-stu-id="536bd-171">Create a managed image using your generalized OS VHD.</span></span> <span data-ttu-id="536bd-172">Замените значения hello своих собственных сведений.</span><span class="sxs-lookup"><span data-stu-id="536bd-172">Replace hello values with your own information.</span></span>


1.  <span data-ttu-id="536bd-173">Во-первых можно задать общие параметры hello:</span><span class="sxs-lookup"><span data-stu-id="536bd-173">First, set hello common parameters:</span></span>

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    $vmSize = "Standard_DS1_v2"
    $location = "East US" 
    $imageName = "yourImageName"
    ```

4.  <span data-ttu-id="536bd-174">Создайте образ hello, с помощью общего виртуального жесткого диска операционной системы.</span><span class="sxs-lookup"><span data-stu-id="536bd-174">Create hello image using your generalized OS VHD.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $urlOfUploadedImageVhd
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```

## <a name="create-a-virtual-network"></a><span data-ttu-id="536bd-175">Создать виртуальную сеть</span><span class="sxs-lookup"><span data-stu-id="536bd-175">Create a virtual network</span></span>
<span data-ttu-id="536bd-176">Создание виртуальной сети hello и подсеть hello [виртуальной сети](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="536bd-176">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="536bd-177">Создайте подсеть hello.</span><span class="sxs-lookup"><span data-stu-id="536bd-177">Create hello subnet.</span></span> <span data-ttu-id="536bd-178">В этом примере создается подсеть с именем *mySubnet* с префикс адреса hello *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="536bd-178">This example creates a subnet named *mySubnet* with hello address prefix of *10.0.0.0/24*.</span></span>  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="536bd-179">Создайте виртуальную сеть hello.</span><span class="sxs-lookup"><span data-stu-id="536bd-179">Create hello virtual network.</span></span> <span data-ttu-id="536bd-180">В этом примере создается виртуальная сеть с именем *myVnet* с префикс адреса hello *10.0.0.0/16*.</span><span class="sxs-lookup"><span data-stu-id="536bd-180">This example creates a virtual network named *myVnet* with hello address prefix of *10.0.0.0/16*.</span></span>  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="536bd-181">Создание общедоступного IP-адреса и сетевого интерфейса</span><span class="sxs-lookup"><span data-stu-id="536bd-181">Create a public IP address and network interface</span></span>

<span data-ttu-id="536bd-182">требуется tooenable взаимодействия с виртуальной машиной hello в виртуальной сети hello, [общедоступный IP-адрес](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) и сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="536bd-182">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="536bd-183">Создание общедоступного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="536bd-183">Create a public IP address.</span></span> <span data-ttu-id="536bd-184">В этом примере создается общедоступный IP-адрес с именем *myPip*.</span><span class="sxs-lookup"><span data-stu-id="536bd-184">This example creates a public IP address named *myPip*.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="536bd-185">Создайте сетевую карту hello.</span><span class="sxs-lookup"><span data-stu-id="536bd-185">Create hello NIC.</span></span> <span data-ttu-id="536bd-186">В этом примере создается сетевая карта с именем **myNic**.</span><span class="sxs-lookup"><span data-stu-id="536bd-186">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="536bd-187">Создание группы безопасности сети hello и правило протокола удаленного рабочего СТОЛА</span><span class="sxs-lookup"><span data-stu-id="536bd-187">Create hello network security group and an RDP rule</span></span>

<span data-ttu-id="536bd-188">возможности toolog toobe в tooyour виртуальную Машину с помощью протокола удаленного рабочего СТОЛА, необходимо toohave правило сетевой безопасности (NSG), позволяющий RDP-доступ через порт 3389.</span><span class="sxs-lookup"><span data-stu-id="536bd-188">toobe able toolog in tooyour VM using RDP, you need toohave a network security rule (NSG) that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="536bd-189">В этом примере создается группа безопасности сети с именем *myNsg*, которая содержит правило с именем *myRdpRule*, разрешающее трафик RDP через порт 3389.</span><span class="sxs-lookup"><span data-stu-id="536bd-189">This example creates an NSG named *myNsg* that contains a rule called *myRdpRule* that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="536bd-190">Дополнительные сведения о Nsg см. в разделе [Открытие портов tooa ВМ в Azure с помощью PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="536bd-190">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

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


## <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="536bd-191">Создайте переменную для hello виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="536bd-191">Create a variable for hello virtual network</span></span>

<span data-ttu-id="536bd-192">Создайте переменную для завершения hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="536bd-192">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-hello-credentials-for-hello-vm"></a><span data-ttu-id="536bd-193">Получить учетные данные hello для hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="536bd-193">Get hello credentials for hello VM</span></span>

<span data-ttu-id="536bd-194">Hello следующий командлет будет открыто окно, можно будет ввести имя и пароль toouse пользователя новый под учетной записью локального администратора hello удаленного доступа hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="536bd-194">hello following cmdlet will open a window where you will enter a new user name and password toouse as hello local administrator account for remotely accessing hello VM.</span></span> 

```powershell
$cred = Get-Credential
```

## <a name="add-hello-vm-name-and-size-toohello-vm-configuration"></a><span data-ttu-id="536bd-195">Добавьте hello имя виртуальной Машины и конфигурация виртуальной Машины toohello размера.</span><span class="sxs-lookup"><span data-stu-id="536bd-195">Add hello VM name and size toohello VM configuration.</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a><span data-ttu-id="536bd-196">Образ виртуальной Машины hello набор как источник изображения hello новой виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="536bd-196">Set hello VM image as source image for hello new VM</span></span>

<span data-ttu-id="536bd-197">Задать hello исходного образа с помощью идентификатора hello hello управляемый образ виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="536bd-197">Set hello source image using hello ID of hello managed VM image.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a><span data-ttu-id="536bd-198">Задание конфигурации hello ОС и добавление hello сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="536bd-198">Set hello OS configuration and add hello NIC.</span></span>

<span data-ttu-id="536bd-199">Введите тип хранения hello (PremiumLRS или StandardLRS) и hello размер диска операционной системы hello.</span><span class="sxs-lookup"><span data-stu-id="536bd-199">Enter hello storage type (PremiumLRS or StandardLRS) and hello size of hello OS disk.</span></span> <span data-ttu-id="536bd-200">В следующем примере тип учетной записи hello слишком*PremiumLRS*, hello размер диска слишком*128 ГБ* и их кэширование слишком*ReadWrite*.</span><span class="sxs-lookup"><span data-stu-id="536bd-200">This example sets hello account type too*PremiumLRS*, hello disk size too*128 GB* and disk caching too*ReadWrite*.</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a><span data-ttu-id="536bd-201">Создание виртуальной Машины hello</span><span class="sxs-lookup"><span data-stu-id="536bd-201">Create hello VM</span></span>

<span data-ttu-id="536bd-202">Создание новой виртуальной Машины с помощью hello конфигурации хранятся в hello hello **$vm** переменной.</span><span class="sxs-lookup"><span data-stu-id="536bd-202">Create hello new VM using hello configuration stored in hello **$vm** variable.</span></span>

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="536bd-203">Убедитесь, что hello создания виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="536bd-203">Verify that hello VM was created</span></span>
<span data-ttu-id="536bd-204">По завершении вы увидите только что созданный виртуальной Машины в hello hello [портал Azure](https://portal.azure.com) под **Обзор** > **виртуальные машины**, или с помощью следующих hello Команды PowerShell:</span><span class="sxs-lookup"><span data-stu-id="536bd-204">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="536bd-205">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="536bd-205">Next steps</span></span>

<span data-ttu-id="536bd-206">toosign в новой виртуальной машины tooyour, toohello обзор виртуальных Машин в hello [портала](https://portal.azure.com), нажмите кнопку **Connect**и откройте hello файл удаленного рабочего СТОЛА.</span><span class="sxs-lookup"><span data-stu-id="536bd-206">toosign in tooyour new virtual machine, browse toohello VM in hello [portal](https://portal.azure.com), click **Connect**, and open hello Remote Desktop RDP file.</span></span> <span data-ttu-id="536bd-207">Используйте учетные данные учетной записи hello объекта к исходной виртуальной машины toosign tooyour новой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="536bd-207">Use hello account credentials of your original virtual machine toosign in tooyour new virtual machine.</span></span> <span data-ttu-id="536bd-208">Дополнительные сведения см. в разделе [как tooconnect и вход в систему tooan Azure виртуальные машины под управлением Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="536bd-208">For more information, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

