---
title: "Подготовка к использованию виртуальный жесткий ДИСК toocreate aaaUpload несколько виртуальных машин в Azure | Документы Microsoft"
description: "Отправьте обобщенный виртуальный жесткий ДИСК tooan хранилища Azure учетная запись toocreate toouse виртуальной Машины Windows с помощью модели развертывания диспетчера ресурсов hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: cynthn
ms.openlocfilehash: aa1af2a0acf81685e62853de71afa51e819cb696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-tooazure-toocreate-a-new-vm"></a><span data-ttu-id="4a5b9-103">Отправка toocreate tooAzure новой виртуальной Машины обобщенный виртуальный жесткий ДИСК</span><span class="sxs-lookup"><span data-stu-id="4a5b9-103">Upload a generalized VHD tooAzure toocreate a new VM</span></span>

<span data-ttu-id="4a5b9-104">В этом разделе рассматриваются отправки учетную запись хранения tooa универсальный неуправляемые диск и последующего создания новой виртуальной Машины с помощью отправки hello диска.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-104">This topic covers uploading a generalized unmanaged disk tooa storage account and then creating a new VM using hello uploaded disk.</span></span> <span data-ttu-id="4a5b9-105">Из универсального образа VHD удалены все сведения вашей личной учетной записи с помощью Sysprep.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-105">A generalized VHD image has had all of your personal account information removed using Sysprep.</span></span> 

<span data-ttu-id="4a5b9-106">Toocreate виртуальной Машины на основе специализированного VHD в учетной записи хранения см [создания виртуальной Машины из специализированного VHD](sa-create-vm-specialized.md).</span><span class="sxs-lookup"><span data-stu-id="4a5b9-106">If you want toocreate a VM from a specialized VHD in a storage account, see [Create a VM from a specialized VHD](sa-create-vm-specialized.md).</span></span>

<span data-ttu-id="4a5b9-107">В этом разделе описывается использование учетных записей хранилища, но мы рекомендуем вместо toousing управляемых диски перемещаются заказчики.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-107">This topic covers using storage accounts, but we recommend customers move toousing Managed Disks instead.</span></span> <span data-ttu-id="4a5b9-108">Полный обзор операций как tooprepare, передача и создание новой виртуальной Машины с помощью управляемых дисках, см. в разделе [Создание новой виртуальной Машины из обобщенный виртуальный жесткий ДИСК отправлен tooAzure, с помощью управляемых дисков](upload-generalized-managed.md).</span><span class="sxs-lookup"><span data-stu-id="4a5b9-108">For a complete walk-through of how tooprepare, upload and create a new VM using managed disks, see [Create a new VM from a generalized VHD uploaded tooAzure using Managed Disks](upload-generalized-managed.md).</span></span>



## <a name="prepare-hello-vm"></a><span data-ttu-id="4a5b9-109">Подготовка виртуальной Машины hello</span><span class="sxs-lookup"><span data-stu-id="4a5b9-109">Prepare hello VM</span></span>

<span data-ttu-id="4a5b9-110">Из универсального VHD удалены все данные вашей личной учетной записи с помощью Sysprep.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-110">A generalized VHD has had all of your personal account information removed using Sysprep.</span></span> <span data-ttu-id="4a5b9-111">Если предполагается toouse hello VHD как toocreate изображения следует новые виртуальные машины из:</span><span class="sxs-lookup"><span data-stu-id="4a5b9-111">If you intend toouse hello VHD as an image toocreate new VMs from, you should:</span></span>
  
  * <span data-ttu-id="4a5b9-112">[Подготовка виртуального жесткого диска Windows tooupload tooAzure](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="4a5b9-112">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md).</span></span> 
  * <span data-ttu-id="4a5b9-113">Обобщить hello виртуальной машины с помощью программы Sysprep</span><span class="sxs-lookup"><span data-stu-id="4a5b9-113">Generalize hello virtual machine using Sysprep</span></span>

### <a name="generalize-a-windows-virtual-machine-using-sysprep"></a><span data-ttu-id="4a5b9-114">Обобщение виртуальной машины Windows с помощью Sysprep</span><span class="sxs-lookup"><span data-stu-id="4a5b9-114">Generalize a Windows virtual machine using Sysprep</span></span>
<span data-ttu-id="4a5b9-115">В этом разделе показано, как toogeneralize вашей виртуальной машины Windows для использования в качестве образа.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-115">This section shows you how toogeneralize your Windows virtual machine for use as an image.</span></span> <span data-ttu-id="4a5b9-116">Sysprep удаляет все ваши личные сведения, помимо прочего и подготавливает toobe машины hello, используемое в качестве изображения.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-116">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="4a5b9-117">Дополнительные сведения о программе Sysprep см. в разделе [как tooUse Sysprep: введение](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="4a5b9-117">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="4a5b9-118">Убедитесь, что на компьютере hello ролей сервера hello поддерживаются программой Sysprep.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-118">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="4a5b9-119">Дополнительные сведения см. в статье [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles) (Поддержка серверных ролей в Sysprep).</span><span class="sxs-lookup"><span data-stu-id="4a5b9-119">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4a5b9-120">При запуске средства Sysprep перед отправкой tooAzure вашего виртуального жесткого диска для hello в первый раз убедитесь, что у вас есть [подготовки ВМ](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) перед запуском Sysprep.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-120">If you are running Sysprep before uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="4a5b9-121">Войдите в систему toohello виртуальной машины Windows.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-121">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="4a5b9-122">Привет открыть окно командной строки с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-122">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="4a5b9-123">Измените каталог hello слишком**%windir%\system32\sysprep**, а затем запустите `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-123">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="4a5b9-124">В hello **средство подготовки системы** выберите **Enter System Out-of-Box Experience (OOBE)**и убедитесь, что hello **Generalize** установлен флажок.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-124">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="4a5b9-125">В разделе **Параметры завершения работы** выберите **Завершение работы**.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-125">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="4a5b9-126">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-126">Click **OK**.</span></span>
   
    ![Запуск Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="4a5b9-128">По завершении работы программы Sysprep завершает hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-128">When Sysprep completes, it shuts down hello virtual machine.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="4a5b9-129">Не перезагружайте hello виртуальной Машины, пока не выполняется отправка tooAzure hello виртуального жесткого диска или создание образа из hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-129">Do not restart hello VM until you are done uploading hello VHD tooAzure or creating an image from hello VM.</span></span> <span data-ttu-id="4a5b9-130">Hello ВМ случайно возвращает перезапуска, запустите Sysprep toogeneralize его еще раз.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-130">If hello VM accidentally gets restarted, run Sysprep toogeneralize it again.</span></span>
> 
> 


## <a name="upload-hello-vhd"></a><span data-ttu-id="4a5b9-131">Отправка hello виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="4a5b9-131">Upload hello VHD</span></span>

<span data-ttu-id="4a5b9-132">Отправка виртуального жесткого диска для hello tooan учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-132">Upload hello VHD tooan Azure storage account.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="4a5b9-133">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="4a5b9-133">Log in tooAzure</span></span>
<span data-ttu-id="4a5b9-134">Если у вас еще нет PowerShell версии 1.4 или выше установлены, чтение [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4a5b9-134">If you don't already have PowerShell version 1.4 or above installed, read [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

1. <span data-ttu-id="4a5b9-135">Откройте Azure PowerShell и войдите в tooyour учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-135">Open Azure PowerShell and sign in tooyour Azure account.</span></span> <span data-ttu-id="4a5b9-136">Откроется всплывающее окно учетные данные учетной записи Azure tooenter вы.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-136">A pop-up window opens for you tooenter your Azure account credentials.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
2. <span data-ttu-id="4a5b9-137">Получите подписку hello идентификаторы для доступных подписок.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-137">Get hello subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="4a5b9-138">Набор hello нужной подписки с идентификатором hello подписки.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-138">Set hello correct subscription using hello subscription ID.</span></span> <span data-ttu-id="4a5b9-139">Замените `<subscriptionID>` с Идентификатором hello hello исправить подписки.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-139">Replace `<subscriptionID>` with hello ID of hello correct subscription.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

### <a name="get-hello-storage-account"></a><span data-ttu-id="4a5b9-140">Получение учетной записи хранилища hello</span><span class="sxs-lookup"><span data-stu-id="4a5b9-140">Get hello storage account</span></span>
<span data-ttu-id="4a5b9-141">Требуется учетная запись хранения в образе виртуальной Машины Azure toostore hello отправлен.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-141">You need a storage account in Azure toostore hello uploaded VM image.</span></span> <span data-ttu-id="4a5b9-142">Можно использовать существующую учетную запись хранения или создать новую.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-142">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="4a5b9-143">tooshow hello доступных учетных записей хранилища, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="4a5b9-143">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="4a5b9-144">Toouse существующую учетную запись хранения следует продолжить toohello [загрузку образа виртуальной Машины hello](#upload-the-vm-vhd-to-your-storage-account) раздела.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-144">If you want toouse an existing storage account, proceed toohello [Upload hello VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="4a5b9-145">Если вам требуется toocreate учетной записи хранилища, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-145">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="4a5b9-146">Требуется имя hello hello группы ресурсов, которой должен быть создан hello учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-146">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="4a5b9-147">toofind out все hello группы ресурсов в вашей подписке типа:</span><span class="sxs-lookup"><span data-stu-id="4a5b9-147">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="4a5b9-148">Группа ресурсов с именем toocreate **myResourceGroup** в hello **Запад США** региона, введите:</span><span class="sxs-lookup"><span data-stu-id="4a5b9-148">toocreate a resource group named **myResourceGroup** in hello **West US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="4a5b9-149">Создать учетную запись хранилища с именем **mystorageaccount** в этой группе ресурсов с помощью hello [New AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) командлета:</span><span class="sxs-lookup"><span data-stu-id="4a5b9-149">Create a storage account named **mystorageaccount** in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
 
### <a name="start-hello-upload"></a><span data-ttu-id="4a5b9-150">Начать отправку hello</span><span class="sxs-lookup"><span data-stu-id="4a5b9-150">Start hello upload</span></span> 

<span data-ttu-id="4a5b9-151">Используйте hello [AzureRmVhd добавить](/powershell/module/azurerm.compute/add-azurermvhd) контейнера командлет tooupload hello изображения tooa вашей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-151">Use hello [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello image tooa container in your storage account.</span></span> <span data-ttu-id="4a5b9-152">В этом примере файл hello передачи **myVHD.vhd** из `"C:\Users\Public\Documents\Virtual hard disks\"` tooa учетной записи хранилища с именем **mystorageaccount** в hello **myResourceGroup** группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-152">This example uploads hello file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` tooa storage account named **mystorageaccount** in hello **myResourceGroup** resource group.</span></span> <span data-ttu-id="4a5b9-153">Hello файла будут помещены в контейнер hello **mycontainer** и hello новый файл будет называться **myUploadedVHD.vhd**.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-153">hello file will be placed into hello container named **mycontainer** and hello new file name will be **myUploadedVHD.vhd**.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="4a5b9-154">В случае успешного выполнения вы получаете ответ, который выглядит примерно toothis:</span><span class="sxs-lookup"><span data-stu-id="4a5b9-154">If successful, you get a response that looks similar toothis:</span></span>

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

<span data-ttu-id="4a5b9-155">В зависимости от сетевого подключения и hello размер файла виртуального жесткого диска, эта команда может занять некоторое время toocomplete.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-155">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete.</span></span>


## <a name="create-a-new-vm"></a><span data-ttu-id="4a5b9-156">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="4a5b9-156">Create a new VM</span></span> 

<span data-ttu-id="4a5b9-157">Теперь можно hello используйте отправки виртуального жесткого диска toocreate новой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-157">You can now use hello uploaded VHD toocreate a new VM.</span></span> 

### <a name="set-hello-uri-of-hello-vhd"></a><span data-ttu-id="4a5b9-158">Набор hello URI hello виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="4a5b9-158">Set hello URI of hello VHD</span></span>

<span data-ttu-id="4a5b9-159">Hello URI для hello toouse виртуальный жесткий ДИСК имеет формат hello: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-159">hello URI for hello VHD toouse is in hello format: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span></span> <span data-ttu-id="4a5b9-160">В этом примере hello виртуального жесткого диска с именем **myVHD** в учетной записи хранения hello **mystorageaccount** в контейнере hello **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-160">In this example hello VHD named **myVHD** is in hello storage account **mystorageaccount** in hello container **mycontainer**.</span></span>

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a><span data-ttu-id="4a5b9-161">Создать виртуальную сеть</span><span class="sxs-lookup"><span data-stu-id="4a5b9-161">Create a virtual network</span></span>
<span data-ttu-id="4a5b9-162">Создание виртуальной сети hello и подсеть hello [виртуальной сети](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4a5b9-162">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="4a5b9-163">Создайте подсеть hello.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-163">Create hello subnet.</span></span> <span data-ttu-id="4a5b9-164">Hello следующий пример создает подсеть с именем **mySubnet** в группе ресурсов hello **myResourceGroup** с префикс адреса hello **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-164">hello following sample creates a subnet named **mySubnet** in hello resource group **myResourceGroup** with hello address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="4a5b9-165">Создайте виртуальную сеть hello.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-165">Create hello virtual network.</span></span> <span data-ttu-id="4a5b9-166">Hello следующий пример создает виртуальную сеть с именем **myVnet** в hello **Запад США** места, где префикс адреса hello **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-166">hello following sample creates a virtual network named **myVnet** in hello **West US** location with hello address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="4a5b9-167">Создание общедоступного IP-адреса и сетевого интерфейса</span><span class="sxs-lookup"><span data-stu-id="4a5b9-167">Create a public IP address and network interface</span></span>
<span data-ttu-id="4a5b9-168">требуется tooenable взаимодействия с виртуальной машиной hello в виртуальной сети hello, [общедоступный IP-адрес](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) и сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-168">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="4a5b9-169">Создание общедоступного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-169">Create a public IP address.</span></span> <span data-ttu-id="4a5b9-170">В этом примере создается общедоступный IP-адрес с именем **myPip**.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-170">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="4a5b9-171">Создайте сетевую карту hello.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-171">Create hello NIC.</span></span> <span data-ttu-id="4a5b9-172">В этом примере создается сетевая карта с именем **myNic**.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-172">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="4a5b9-173">Создание группы безопасности сети hello и правило протокола удаленного рабочего СТОЛА</span><span class="sxs-lookup"><span data-stu-id="4a5b9-173">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="4a5b9-174">возможности toolog toobe в tooyour виртуальную Машину с помощью протокола удаленного рабочего СТОЛА, необходимо toohave правило безопасности, которое разрешает RDP-доступ через порт 3389.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-174">toobe able toolog in tooyour VM using RDP, you need toohave a security rule that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="4a5b9-175">В этом примере создается группа безопасности сети с именем **myNsg**, которая содержит правило с именем **myRdpRule**, разрешающее трафик RDP через порт 3389.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-175">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="4a5b9-176">Дополнительные сведения о Nsg см. в разделе [Открытие портов tooa ВМ в Azure с помощью PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4a5b9-176">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="4a5b9-177">Создайте переменную для hello виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="4a5b9-177">Create a variable for hello virtual network</span></span>
<span data-ttu-id="4a5b9-178">Создайте переменную для завершения hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-178">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-hello-vm"></a><span data-ttu-id="4a5b9-179">Создание виртуальной Машины hello</span><span class="sxs-lookup"><span data-stu-id="4a5b9-179">Create hello VM</span></span>
<span data-ttu-id="4a5b9-180">Hello следующий сценарий PowerShell показано, как tooset hello конфигураций виртуальных машин и используйте hello загрузить образ виртуальной Машины как hello источника для новой установки hello.</span><span class="sxs-lookup"><span data-stu-id="4a5b9-180">hello following PowerShell script shows how tooset up hello virtual machine configurations and use hello uploaded VM image as hello source for hello new installation.</span></span>



```powershell
# Enter a new user name and password toouse as hello local administrator account 
    # for remotely accessing hello VM.
    $cred = Get-Credential

    # Name of hello storage account where hello VHD is located. This example sets hello 
    # storage account name as "myStorageAccount"
    $storageAccName = "myStorageAccount"

    # Name of hello virtual machine. This example sets hello VM name as "myVM".
    $vmName = "myVM"

    # Size of hello virtual machine. This example creates "Standard_D2_v2" sized VM. 
    # See hello VM sizes documentation for more information: 
    # https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/
    $vmSize = "Standard_D2_v2"

    # Computer name for hello VM. This examples sets hello computer name as "myComputer".
    $computerName = "myComputer"

    # Name of hello disk that holds hello OS. This example sets hello 
    # OS disk name as "myOsDisk"
    $osDiskName = "myOsDisk"

    # Assign a SKU name. This example sets hello SKU name as "Standard_LRS"
    # Valid values for -SkuName are: Standard_LRS - locally redundant storage, Standard_ZRS - zone redundant
    # storage, Standard_GRS - geo redundant storage, Standard_RAGRS - read access geo redundant storage,
    # Premium_LRS - premium locally redundant storage. 
    $skuName = "Standard_LRS"

    # Get hello storage account where hello uploaded image is stored
    $storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $rgName -AccountName $storageAccName

    # Set hello VM name and size
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

    #Set hello Windows operating system configuration and add hello NIC
    $vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

    # Create hello OS disk URI
    $osDiskUri = '{0}vhds/{1}-{2}.vhd' `
        -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName

    # Configure hello OS disk toobe created from hello existing VHD image (-CreateOption fromImage).
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri `
        -CreateOption fromImage -SourceImageUri $imageURI -Windows

    # Create hello new VM
    New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

## <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="4a5b9-181">Убедитесь, что hello создания виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="4a5b9-181">Verify that hello VM was created</span></span>
<span data-ttu-id="4a5b9-182">По завершении вы увидите только что созданный виртуальной Машины в hello hello [портал Azure](https://portal.azure.com) под **Обзор** > **виртуальные машины**, или с помощью следующих hello Команды PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4a5b9-182">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="4a5b9-183">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4a5b9-183">Next steps</span></span>
<span data-ttu-id="4a5b9-184">см. на новую виртуальную машину с помощью Azure PowerShell toomanage [управление виртуальными машинами с помощью диспетчера ресурсов Azure и PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4a5b9-184">toomanage your new virtual machine with Azure PowerShell, see [Manage virtual machines using Azure Resource Manager and PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


