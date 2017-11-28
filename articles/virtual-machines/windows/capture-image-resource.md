---
title: "aaaCreate управляемый образ в Azure | Документы Microsoft"
description: "Создание управляемого образа универсальной виртуальной машины или виртуального жесткого диска в Azure. Изображения могут быть toocreate используется несколько виртуальных машин, использующих управляемый дисков."
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
ms.date: 02/27/2017
ms.author: cynthn
ms.openlocfilehash: d8cd6c2ce8c5d704de2c845abced85139944d682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-image-of-a-generalized-vm-in-azure"></a><span data-ttu-id="a6287-104">Создание управляемого образа универсальной виртуальной машины в Azure</span><span class="sxs-lookup"><span data-stu-id="a6287-104">Create a managed image of a generalized VM in Azure</span></span>

<span data-ttu-id="a6287-105">Ресурс управляемого образа можно создать из универсальной виртуальной машины, которая хранится в виде управляемого диска или неуправляемых дисков в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="a6287-105">A managed image resource can be created from a generalized VM that is stored as either a managed disk or an unmanaged disk in a storage account.</span></span> <span data-ttu-id="a6287-106">Здравствуйте, изображение может затем быть toocreate используется несколько виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="a6287-106">hello image can then be used toocreate multiple VMs.</span></span> 


## <a name="generalize-hello-windows-vm-using-sysprep"></a><span data-ttu-id="a6287-107">Обобщить hello виртуальной Машины Windows с помощью программы Sysprep</span><span class="sxs-lookup"><span data-stu-id="a6287-107">Generalize hello Windows VM using Sysprep</span></span>

<span data-ttu-id="a6287-108">Sysprep удаляет все ваши личные сведения, помимо прочего и подготавливает toobe машины hello, используемое в качестве изображения.</span><span class="sxs-lookup"><span data-stu-id="a6287-108">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="a6287-109">Дополнительные сведения о программе Sysprep см. в разделе [как tooUse Sysprep: введение](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="a6287-109">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="a6287-110">Убедитесь, что на компьютере hello ролей сервера hello поддерживаются программой Sysprep.</span><span class="sxs-lookup"><span data-stu-id="a6287-110">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="a6287-111">Дополнительные сведения см. в статье [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles) (Поддержка серверных ролей в Sysprep).</span><span class="sxs-lookup"><span data-stu-id="a6287-111">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a6287-112">При запуске средства Sysprep перед отправкой tooAzure вашего виртуального жесткого диска для hello в первый раз убедитесь, что у вас есть [подготовки ВМ](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) перед запуском Sysprep.</span><span class="sxs-lookup"><span data-stu-id="a6287-112">If you are running Sysprep before uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="a6287-113">Войдите в систему toohello виртуальной машины Windows.</span><span class="sxs-lookup"><span data-stu-id="a6287-113">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="a6287-114">Привет открыть окно командной строки с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="a6287-114">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="a6287-115">Измените каталог hello слишком**%windir%\system32\sysprep**, а затем запустите `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="a6287-115">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="a6287-116">В hello **средство подготовки системы** выберите **Enter System Out-of-Box Experience (OOBE)**и убедитесь, что hello **Generalize** установлен флажок.</span><span class="sxs-lookup"><span data-stu-id="a6287-116">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="a6287-117">В разделе **Параметры завершения работы** выберите **Завершение работы**.</span><span class="sxs-lookup"><span data-stu-id="a6287-117">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="a6287-118">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a6287-118">Click **OK**.</span></span>
   
    ![Запуск Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="a6287-120">По завершении работы программы Sysprep завершает hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a6287-120">When Sysprep completes, it shuts down hello virtual machine.</span></span> <span data-ttu-id="a6287-121">Не перезагружайте hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a6287-121">Do not restart hello VM.</span></span>


## <a name="create-a-managed-image-in-hello-portal"></a><span data-ttu-id="a6287-122">Создать управляемый образ на портале hello</span><span class="sxs-lookup"><span data-stu-id="a6287-122">Create a managed image in hello portal</span></span> 

1. <span data-ttu-id="a6287-123">Откройте hello [портала](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a6287-123">Open hello [portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a6287-124">Щелкните hello плюс toocreate новый ресурс.</span><span class="sxs-lookup"><span data-stu-id="a6287-124">Click hello plus sign toocreate a new resource.</span></span>
3. <span data-ttu-id="a6287-125">В поле фильтра поиска hello введите **изображения**.</span><span class="sxs-lookup"><span data-stu-id="a6287-125">In hello filter search, type **Image**.</span></span>
4. <span data-ttu-id="a6287-126">Выберите **изображения** из результатов hello.</span><span class="sxs-lookup"><span data-stu-id="a6287-126">Select **Image** from hello results.</span></span>
5. <span data-ttu-id="a6287-127">В hello **изображения** колонка, щелкните **создать**.</span><span class="sxs-lookup"><span data-stu-id="a6287-127">In hello **Image** blade, click **Create**.</span></span>
6. <span data-ttu-id="a6287-128">В **имя**, введите имя образа hello.</span><span class="sxs-lookup"><span data-stu-id="a6287-128">In **Name**, type a name for hello image.</span></span>
7. <span data-ttu-id="a6287-129">Если имеется несколько подписок, выберите hello правильный выбор из hello **подписки** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="a6287-129">If you have more than one subscription, select hello correct one from hello **Subscription** drop-down.</span></span>
7. <span data-ttu-id="a6287-130">В **группы ресурсов** выберите **создать новый** и введите имя или выберите **из существующего** и выберите из раскрывающегося списка hello toouse группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a6287-130">In **Resource Group** either select **Create new** and type in a name, or select **From existing** and select a resource group toouse from hello drop-down list.</span></span>
8. <span data-ttu-id="a6287-131">В **расположение**, выберите расположение hello группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a6287-131">In **Location**, choose hello location of your resource group.</span></span>
9. <span data-ttu-id="a6287-132">В **тип ОС** выберите hello тип операционной системы Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="a6287-132">In **OS type** select hello type of operating system, either Windows or Linux.</span></span>
11. <span data-ttu-id="a6287-133">В **BLOB-объекта хранилища**, нажмите кнопку **Обзор** toolook для hello виртуального жесткого диска в службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="a6287-133">In **Storage blob**, click **Browse** toolook for hello VHD in your Azure storage.</span></span>
12. <span data-ttu-id="a6287-134">В поле **Тип учетной записи** выберите Standard_LRS или Premium_LRS.</span><span class="sxs-lookup"><span data-stu-id="a6287-134">In **Account type** choose Standard_LRS or Premium_LRS.</span></span> <span data-ttu-id="a6287-135">Для уровня "Стандартный" используются жесткие диски, а для уровня "Премиум" — твердотельные накопители.</span><span class="sxs-lookup"><span data-stu-id="a6287-135">Standard uses hard-disk drives and Premium uses solid-state drives.</span></span> <span data-ttu-id="a6287-136">Для обоих уровней используется локально избыточное хранилище.</span><span class="sxs-lookup"><span data-stu-id="a6287-136">Both use locally-redundant storage.</span></span>
13. <span data-ttu-id="a6287-137">В **кэширования диска** Здравствуйте, выберите соответствующий диск параметр кэширования.</span><span class="sxs-lookup"><span data-stu-id="a6287-137">In **Disk caching** select hello appropriate disk caching option.</span></span> <span data-ttu-id="a6287-138">Параметры Hello **нет**, **только для чтения** и **находится**.</span><span class="sxs-lookup"><span data-stu-id="a6287-138">hello options are **None**, **Read-only** and **Read\write**.</span></span>
14. <span data-ttu-id="a6287-139">Необязательно: Можно также добавить образ toohello диска данных, щелкнув **+ добавить диск данных**.</span><span class="sxs-lookup"><span data-stu-id="a6287-139">Optional: You can also add an existing data disk toohello image by clicking **+ Add data disk**.</span></span>  
15. <span data-ttu-id="a6287-140">Завершив настройку параметров, нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a6287-140">When you are done making your selections, click **Create**.</span></span>
16. <span data-ttu-id="a6287-141">После создания образа hello, вы увидите его как **изображения** ресурс в список hello ресурсов в группе ресурсов hello выбрано.</span><span class="sxs-lookup"><span data-stu-id="a6287-141">After hello image is created, you will see it as an **Image** resource in hello list of resources in hello resource group you chose.</span></span>



## <a name="create-a-managed-image-of-a-vm-using-powershell"></a><span data-ttu-id="a6287-142">Создание управляемого образа виртуальной машины с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="a6287-142">Create a managed image of a VM using Powershell</span></span>

<span data-ttu-id="a6287-143">Создание образа непосредственно из виртуальных Машин гарантирует, что это изображение hello приветствия включает все hello диски, связанные с hello виртуальной Машины, включая hello диска ОС и дисков данных.</span><span class="sxs-lookup"><span data-stu-id="a6287-143">Creating an image directly from hello VM ensures that hello image includes all of hello disks associated with hello VM, including hello OS Disk and any data disks.</span></span>


<span data-ttu-id="a6287-144">Прежде чем начать, убедитесь, что последняя версия модуля AzureRM.Compute PowerShell hello hello.</span><span class="sxs-lookup"><span data-stu-id="a6287-144">Before you begin, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="a6287-145">Запустите hello следующие tooinstall команды.</span><span class="sxs-lookup"><span data-stu-id="a6287-145">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="a6287-146">Дополнительные сведения см. в разделе [об управлении версиями Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a6287-146">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


1. <span data-ttu-id="a6287-147">Создайте несколько переменных.</span><span class="sxs-lookup"><span data-stu-id="a6287-147">Create some variables.</span></span>

    ```powershell
    $vmName = "myVM"
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $imageName = "myImage"
    ```
2. <span data-ttu-id="a6287-148">Убедитесь, что виртуальная машина была освобождена приветствия.</span><span class="sxs-lookup"><span data-stu-id="a6287-148">Make sure hello VM has been deallocated.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. <span data-ttu-id="a6287-149">Задать состояние hello hello виртуальной машины слишком**универсальная**.</span><span class="sxs-lookup"><span data-stu-id="a6287-149">Set hello status of hello virtual machine too**Generalized**.</span></span> 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized
    ```
    
4. <span data-ttu-id="a6287-150">Получение hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a6287-150">Get hello virtual machine.</span></span> 

    ```powershell
    $vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName
    ```

5. <span data-ttu-id="a6287-151">Создайте конфигурацию hello изображения.</span><span class="sxs-lookup"><span data-stu-id="a6287-151">Create hello image configuration.</span></span>

    ```powershell
    $image = New-AzureRmImageConfig -Location $location -SourceVirtualMachineId $vm.ID 
    ```
6. <span data-ttu-id="a6287-152">Создание образа hello.</span><span class="sxs-lookup"><span data-stu-id="a6287-152">Create hello image.</span></span>

    ```powershell
    New-AzureRmImage -Image $image -ImageName $imageName -ResourceGroupName $rgName
    ``` 



## <a name="create-a-managed-image-of-a-vhd-in-powershell"></a><span data-ttu-id="a6287-153">Создание управляемого образа виртуального жесткого диска с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="a6287-153">Create a managed image of a VHD in PowerShell</span></span>

<span data-ttu-id="a6287-154">Создайте управляемый образ с помощью универсального виртуального жесткого диска ОС.</span><span class="sxs-lookup"><span data-stu-id="a6287-154">Create a managed image using your generalized OS VHD.</span></span>


1.  <span data-ttu-id="a6287-155">Во-первых можно задать общие параметры hello:</span><span class="sxs-lookup"><span data-stu-id="a6287-155">First, set hello common parameters:</span></span>

    ```powershell
    $rgName = "myResourceGroupName"
    $vmName = "myVM"
    $location = "West Central US" 
    $imageName = "yourImageName"
    $osVhdUri = "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd"
    ```
2. <span data-ttu-id="a6287-156">Здравствуйте, Step\deallocate виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a6287-156">Step\deallocate hello VM.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. <span data-ttu-id="a6287-157">Пометьте виртуальной Машины как обобщенный hello.</span><span class="sxs-lookup"><span data-stu-id="a6287-157">Mark hello VM as generalized.</span></span>

    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized 
    ```
4.  <span data-ttu-id="a6287-158">Создайте образ hello, с помощью общего виртуального жесткого диска операционной системы.</span><span class="sxs-lookup"><span data-stu-id="a6287-158">Create hello image using your generalized OS VHD.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $osVhdUri
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```


## <a name="create-a-managed-image-from-a-snapshot-using-powershell"></a><span data-ttu-id="a6287-159">Создание управляемого образа из моментального снимка с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="a6287-159">Create a managed image from a snapshot using Powershell</span></span>

<span data-ttu-id="a6287-160">Можно также создать управляемый образ из моментального снимка hello VHD из универсальной ВМ.</span><span class="sxs-lookup"><span data-stu-id="a6287-160">You can also create a managed image from a snapshot of hello VHD from a generalized VM.</span></span>

    
1. <span data-ttu-id="a6287-161">Создайте несколько переменных.</span><span class="sxs-lookup"><span data-stu-id="a6287-161">Create some variables.</span></span> 

    ```powershell
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $snapshotName = "mySnapshot"
    $imageName = "myImage"
    ```

2. <span data-ttu-id="a6287-162">Получение моментальных снимков hello.</span><span class="sxs-lookup"><span data-stu-id="a6287-162">Get hello snapshot.</span></span>

   ```powershell
   $snapshot = Get-AzureRmSnapshot -ResourceGroupName $rgName -SnapshotName $snapshotName
   ```
   
3. <span data-ttu-id="a6287-163">Создайте конфигурацию hello изображения.</span><span class="sxs-lookup"><span data-stu-id="a6287-163">Create hello image configuration.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsState Generalized -OsType Windows -SnapshotId $snapshot.Id
    ```
4. <span data-ttu-id="a6287-164">Создание образа hello.</span><span class="sxs-lookup"><span data-stu-id="a6287-164">Create hello image.</span></span>

    ```powershell
    New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ``` 
    

## <a name="next-steps"></a><span data-ttu-id="a6287-165">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a6287-165">Next steps</span></span>
- <span data-ttu-id="a6287-166">Теперь вы можете [создания виртуальной Машины из образа управляемого hello обобщенный](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a6287-166">Now you can [create a VM from hello generalized managed image](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>    

