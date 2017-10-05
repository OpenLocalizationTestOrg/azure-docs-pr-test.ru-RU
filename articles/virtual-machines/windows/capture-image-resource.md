---
title: "Создание управляемого образа в Azure | Документация Майкрософт"
description: "Создание управляемого образа универсальной виртуальной машины или виртуального жесткого диска в Azure. Образы можно использовать для создания нескольких виртуальных машин, использующих управляемые диски."
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
ms.openlocfilehash: f64b81489ab426b50ec89af369e1581ac71848be
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-managed-image-of-a-generalized-vm-in-azure"></a><span data-ttu-id="dd302-104">Создание управляемого образа универсальной виртуальной машины в Azure</span><span class="sxs-lookup"><span data-stu-id="dd302-104">Create a managed image of a generalized VM in Azure</span></span>

<span data-ttu-id="dd302-105">Ресурс управляемого образа можно создать из универсальной виртуальной машины, которая хранится в виде управляемого диска или неуправляемых дисков в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="dd302-105">A managed image resource can be created from a generalized VM that is stored as either a managed disk or an unmanaged disk in a storage account.</span></span> <span data-ttu-id="dd302-106">Затем образ можно использовать для создания нескольких виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="dd302-106">The image can then be used to create multiple VMs.</span></span> 


## <a name="generalize-the-windows-vm-using-sysprep"></a><span data-ttu-id="dd302-107">Подготовка виртуальной машины Windows к использованию с помощью Sysprep</span><span class="sxs-lookup"><span data-stu-id="dd302-107">Generalize the Windows VM using Sysprep</span></span>

<span data-ttu-id="dd302-108">Помимо прочих действий Sysprep удаляет все сведения о вашей учетной записи и подготавливает машину к использованию в качестве образа.</span><span class="sxs-lookup"><span data-stu-id="dd302-108">Sysprep removes all your personal account information, among other things, and prepares the machine to be used as an image.</span></span> <span data-ttu-id="dd302-109">Сведения о Sysprep см. в статье [Использование программы Sysprep: введение](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="dd302-109">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="dd302-110">Убедитесь, что Sysprep поддерживает роли сервера, запущенные на компьютере.</span><span class="sxs-lookup"><span data-stu-id="dd302-110">Make sure the server roles running on the machine are supported by Sysprep.</span></span> <span data-ttu-id="dd302-111">Дополнительные сведения см. в статье [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles) (Поддержка серверных ролей в Sysprep).</span><span class="sxs-lookup"><span data-stu-id="dd302-111">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dd302-112">Если вы еще не отправили виртуальный жесткий диск в Azure и собираетесь запустить Sysprep первый раз, прежде чем это делать, [подготовьте виртуальную машину](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dd302-112">If you are running Sysprep before uploading your VHD to Azure for the first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="dd302-113">Выполните вход на виртуальную машину Windows.</span><span class="sxs-lookup"><span data-stu-id="dd302-113">Sign in to the Windows virtual machine.</span></span>
2. <span data-ttu-id="dd302-114">Откройте окно командной строки с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="dd302-114">Open the Command Prompt window as an administrator.</span></span> <span data-ttu-id="dd302-115">Измените каталог на **%windir%\system32\sysprep** и запустите файл `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="dd302-115">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="dd302-116">В диалоговом окне **Программа подготовки системы** выберите **Переход в окно приветствия системы (OOBE)** и убедитесь, что установлен флажок **Подготовка к использованию**.</span><span class="sxs-lookup"><span data-stu-id="dd302-116">In the **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that the **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="dd302-117">В разделе **Параметры завершения работы** выберите **Завершение работы**.</span><span class="sxs-lookup"><span data-stu-id="dd302-117">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="dd302-118">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="dd302-118">Click **OK**.</span></span>
   
    ![Запуск Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="dd302-120">После выполнения всех необходимых действий Sysprep завершает работу виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="dd302-120">When Sysprep completes, it shuts down the virtual machine.</span></span> <span data-ttu-id="dd302-121">Не перезапускайте виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="dd302-121">Do not restart the VM.</span></span>


## <a name="create-a-managed-image-in-the-portal"></a><span data-ttu-id="dd302-122">Создание управляемого образа на портале</span><span class="sxs-lookup"><span data-stu-id="dd302-122">Create a managed image in the portal</span></span> 

1. <span data-ttu-id="dd302-123">Откройте [портал](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dd302-123">Open the [portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="dd302-124">Нажмите знак "плюс" (+), чтобы создать ресурс.</span><span class="sxs-lookup"><span data-stu-id="dd302-124">Click the plus sign to create a new resource.</span></span>
3. <span data-ttu-id="dd302-125">В поле фильтрации поиска введите **Image**.</span><span class="sxs-lookup"><span data-stu-id="dd302-125">In the filter search, type **Image**.</span></span>
4. <span data-ttu-id="dd302-126">Выберите **Image** (Образ) из результатов.</span><span class="sxs-lookup"><span data-stu-id="dd302-126">Select **Image** from the results.</span></span>
5. <span data-ttu-id="dd302-127">В колонке **Image** (Образ) нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="dd302-127">In the **Image** blade, click **Create**.</span></span>
6. <span data-ttu-id="dd302-128">В поле **Имя** введите имя образа.</span><span class="sxs-lookup"><span data-stu-id="dd302-128">In **Name**, type a name for the image.</span></span>
7. <span data-ttu-id="dd302-129">При наличии нескольких подписок выберите подписку, которую вы хотите использовать, из раскрывающегося списка **Подписка**.</span><span class="sxs-lookup"><span data-stu-id="dd302-129">If you have more than one subscription, select the correct one from the **Subscription** drop-down.</span></span>
7. <span data-ttu-id="dd302-130">В поле **Группа ресурсов** выберите **Создать** и введите имя или выберите **From existing** (Из существующего) и выберите из раскрывающегося списка используемую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="dd302-130">In **Resource Group** either select **Create new** and type in a name, or select **From existing** and select a resource group to use from the drop-down list.</span></span>
8. <span data-ttu-id="dd302-131">В поле **Расположение** выберите расположение группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="dd302-131">In **Location**, choose the location of your resource group.</span></span>
9. <span data-ttu-id="dd302-132">В поле **Тип ОС** выберите тип операционной системы: Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="dd302-132">In **OS type** select the type of operating system, either Windows or Linux.</span></span>
11. <span data-ttu-id="dd302-133">В разделе **Большой двоичный объект хранилища** нажмите кнопку **Обзор**, чтобы найти виртуальный жесткий диск в службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="dd302-133">In **Storage blob**, click **Browse** to look for the VHD in your Azure storage.</span></span>
12. <span data-ttu-id="dd302-134">В поле **Тип учетной записи** выберите Standard_LRS или Premium_LRS.</span><span class="sxs-lookup"><span data-stu-id="dd302-134">In **Account type** choose Standard_LRS or Premium_LRS.</span></span> <span data-ttu-id="dd302-135">Для уровня "Стандартный" используются жесткие диски, а для уровня "Премиум" — твердотельные накопители.</span><span class="sxs-lookup"><span data-stu-id="dd302-135">Standard uses hard-disk drives and Premium uses solid-state drives.</span></span> <span data-ttu-id="dd302-136">Для обоих уровней используется локально избыточное хранилище.</span><span class="sxs-lookup"><span data-stu-id="dd302-136">Both use locally-redundant storage.</span></span>
13. <span data-ttu-id="dd302-137">Из списка **Disk caching** (Кэширование дисков) выберите соответствующий параметр кэширования дисков.</span><span class="sxs-lookup"><span data-stu-id="dd302-137">In **Disk caching** select the appropriate disk caching option.</span></span> <span data-ttu-id="dd302-138">Возможные параметры: **None** (Нет), **Read-only** (Только чтение) и **Read\write** (Чтение и запись).</span><span class="sxs-lookup"><span data-stu-id="dd302-138">The options are **None**, **Read-only** and **Read\write**.</span></span>
14. <span data-ttu-id="dd302-139">(Необязательно.) В образ можно добавить существующий диск данных, щелкнув **+ Добавить диск данных**.</span><span class="sxs-lookup"><span data-stu-id="dd302-139">Optional: You can also add an existing data disk to the image by clicking **+ Add data disk**.</span></span>  
15. <span data-ttu-id="dd302-140">Завершив настройку параметров, нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="dd302-140">When you are done making your selections, click **Create**.</span></span>
16. <span data-ttu-id="dd302-141">После создания образа вы увидите его в виде ресурса **Image** в списке ресурсов группы ресурсов, которую вы выбрали.</span><span class="sxs-lookup"><span data-stu-id="dd302-141">After the image is created, you will see it as an **Image** resource in the list of resources in the resource group you chose.</span></span>



## <a name="create-a-managed-image-of-a-vm-using-powershell"></a><span data-ttu-id="dd302-142">Создание управляемого образа виртуальной машины с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd302-142">Create a managed image of a VM using Powershell</span></span>

<span data-ttu-id="dd302-143">Создание образа непосредственно из виртуальной машины гарантирует, что он будет содержать все ее диски, включая диск ОС и диски данных.</span><span class="sxs-lookup"><span data-stu-id="dd302-143">Creating an image directly from the VM ensures that the image includes all of the disks associated with the VM, including the OS Disk and any data disks.</span></span>


<span data-ttu-id="dd302-144">Прежде чем начать, убедитесь, что у вас установлена последняя версия модуля PowerShell AzureRM.Compute.</span><span class="sxs-lookup"><span data-stu-id="dd302-144">Before you begin, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="dd302-145">Выполните следующую команду, чтобы установить ее.</span><span class="sxs-lookup"><span data-stu-id="dd302-145">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="dd302-146">Дополнительные сведения см. в разделе [об управлении версиями Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dd302-146">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


1. <span data-ttu-id="dd302-147">Создайте несколько переменных.</span><span class="sxs-lookup"><span data-stu-id="dd302-147">Create some variables.</span></span>

    ```powershell
    $vmName = "myVM"
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $imageName = "myImage"
    ```
2. <span data-ttu-id="dd302-148">Убедитесь, что виртуальная машина была освобождена.</span><span class="sxs-lookup"><span data-stu-id="dd302-148">Make sure the VM has been deallocated.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. <span data-ttu-id="dd302-149">Теперь задайте для виртуальной машины состояние **Generalized**(Универсальная).</span><span class="sxs-lookup"><span data-stu-id="dd302-149">Set the status of the virtual machine to **Generalized**.</span></span> 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized
    ```
    
4. <span data-ttu-id="dd302-150">Получите виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="dd302-150">Get the virtual machine.</span></span> 

    ```powershell
    $vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName
    ```

5. <span data-ttu-id="dd302-151">Создайте конфигурацию образа.</span><span class="sxs-lookup"><span data-stu-id="dd302-151">Create the image configuration.</span></span>

    ```powershell
    $image = New-AzureRmImageConfig -Location $location -SourceVirtualMachineId $vm.ID 
    ```
6. <span data-ttu-id="dd302-152">Создайте образ.</span><span class="sxs-lookup"><span data-stu-id="dd302-152">Create the image.</span></span>

    ```powershell
    New-AzureRmImage -Image $image -ImageName $imageName -ResourceGroupName $rgName
    ``` 



## <a name="create-a-managed-image-of-a-vhd-in-powershell"></a><span data-ttu-id="dd302-153">Создание управляемого образа виртуального жесткого диска с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd302-153">Create a managed image of a VHD in PowerShell</span></span>

<span data-ttu-id="dd302-154">Создайте управляемый образ с помощью универсального виртуального жесткого диска ОС.</span><span class="sxs-lookup"><span data-stu-id="dd302-154">Create a managed image using your generalized OS VHD.</span></span>


1.  <span data-ttu-id="dd302-155">Сначала задайте общие параметры.</span><span class="sxs-lookup"><span data-stu-id="dd302-155">First, set the common parameters:</span></span>

    ```powershell
    $rgName = "myResourceGroupName"
    $vmName = "myVM"
    $location = "West Central US" 
    $imageName = "yourImageName"
    $osVhdUri = "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd"
    ```
2. <span data-ttu-id="dd302-156">Остановите и освободите виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="dd302-156">Step\deallocate the VM.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. <span data-ttu-id="dd302-157">Пометьте виртуальную машину как универсальную.</span><span class="sxs-lookup"><span data-stu-id="dd302-157">Mark the VM as generalized.</span></span>

    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized 
    ```
4.  <span data-ttu-id="dd302-158">Создайте образ с помощью универсального виртуального жесткого диска ОС.</span><span class="sxs-lookup"><span data-stu-id="dd302-158">Create the image using your generalized OS VHD.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $osVhdUri
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```


## <a name="create-a-managed-image-from-a-snapshot-using-powershell"></a><span data-ttu-id="dd302-159">Создание управляемого образа из моментального снимка с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="dd302-159">Create a managed image from a snapshot using Powershell</span></span>

<span data-ttu-id="dd302-160">Можно создать управляемый образ из моментального снимка виртуального жесткого диска универсальной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="dd302-160">You can also create a managed image from a snapshot of the VHD from a generalized VM.</span></span>

    
1. <span data-ttu-id="dd302-161">Создайте несколько переменных.</span><span class="sxs-lookup"><span data-stu-id="dd302-161">Create some variables.</span></span> 

    ```powershell
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $snapshotName = "mySnapshot"
    $imageName = "myImage"
    ```

2. <span data-ttu-id="dd302-162">Получите моментальный снимок.</span><span class="sxs-lookup"><span data-stu-id="dd302-162">Get the snapshot.</span></span>

   ```powershell
   $snapshot = Get-AzureRmSnapshot -ResourceGroupName $rgName -SnapshotName $snapshotName
   ```
   
3. <span data-ttu-id="dd302-163">Создайте конфигурацию образа.</span><span class="sxs-lookup"><span data-stu-id="dd302-163">Create the image configuration.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsState Generalized -OsType Windows -SnapshotId $snapshot.Id
    ```
4. <span data-ttu-id="dd302-164">Создайте образ.</span><span class="sxs-lookup"><span data-stu-id="dd302-164">Create the image.</span></span>

    ```powershell
    New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ``` 
    

## <a name="next-steps"></a><span data-ttu-id="dd302-165">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dd302-165">Next steps</span></span>
- <span data-ttu-id="dd302-166">Теперь вы можете [создать виртуальную машину из универсального управляемого образа](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dd302-166">Now you can [create a VM from the generalized managed image](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>  

