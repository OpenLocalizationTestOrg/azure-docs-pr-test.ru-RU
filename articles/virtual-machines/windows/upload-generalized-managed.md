---
title: "Создание управляемой виртуальной машины Azure на основе универсальных локальных дисков VHD | Документация Майкрософт"
description: "Отправка универсального диска VHD в Azure и создание виртуальных машин с его помощью в модели развертывания Resource Manager."
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
ms.openlocfilehash: d802ba16ecb4e32e2adb7be3a8e99c72a1625841
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="upload-a-generalized-vhd-and-use-it-to-create-new-vms-in-azure"></a><span data-ttu-id="0615e-103">Отправка универсального диска VHD и создание виртуальных машин с его помощью в Azure</span><span class="sxs-lookup"><span data-stu-id="0615e-103">Upload a generalized VHD and use it to create new VMs in Azure</span></span>

<span data-ttu-id="0615e-104">В этой статье описывается использование PowerShell для отправки диска VHD универсальной виртуальной машины в Azure, создание образа на основе диска VHD и создание виртуальной машины на основе этого образа.</span><span class="sxs-lookup"><span data-stu-id="0615e-104">This topic walks you through using PowerShell to upload a VHD of a generalized VM to Azure, create an image from the VHD and create a new VM from that image.</span></span> <span data-ttu-id="0615e-105">Вы можете отправить диск VHD, экспортированный из локального инструмента виртуализации или из другого облака.</span><span class="sxs-lookup"><span data-stu-id="0615e-105">You can upload a VHD exported from an on-premises virtualization tool or from another cloud.</span></span> <span data-ttu-id="0615e-106">При использовании [Управляемых дисков](managed-disks-overview.md) для новой виртуальной машины упрощается управление виртуальными машинами и обеспечивается более высокий уровень доступности виртуальной машины, размещенной в группе доступности.</span><span class="sxs-lookup"><span data-stu-id="0615e-106">Using [Managed Disks](managed-disks-overview.md) for the new VM simplifies the VM managment and provides better availability when the VM is placed in an availability set.</span></span> 

<span data-ttu-id="0615e-107">Если необходимо использовать пример скрипта, см. статью [Sample script to upload a VHD to Azure and create a new VM](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md) (Пример скрипта для отправки VHD в Azure и создания виртуальной машины).</span><span class="sxs-lookup"><span data-stu-id="0615e-107">If you want to use a sample script, see [Sample script to upload a VHD to Azure and create a new VM](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0615e-108">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="0615e-108">Before you begin</span></span>

- <span data-ttu-id="0615e-109">Прежде чем передавать в Azure виртуальный жесткий диск любого типа, следует выполнить инструкции из статьи [Подготовка диска VHD или VHDX для Windows к отправке в Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0615e-109">Before uploading any VHD to Azure, you should follow [Prepare a Windows VHD or VHDX to upload to Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
- <span data-ttu-id="0615e-110">Прежде чем начать миграцию на [Управляемые диски](managed-disks-overview.md), внимательно изучите [этот раздел](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks).</span><span class="sxs-lookup"><span data-stu-id="0615e-110">Review [Plan for the migration to Managed Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) before starting your migration to [Managed Disks](managed-disks-overview.md).</span></span>
- <span data-ttu-id="0615e-111">Убедитесь, что у вас установлена последняя версия модуля PowerShell AzureRM.Compute.</span><span class="sxs-lookup"><span data-stu-id="0615e-111">Make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="0615e-112">Выполните следующую команду, чтобы установить ее.</span><span class="sxs-lookup"><span data-stu-id="0615e-112">Run the following command to install it.</span></span>

    ```powershell
    Install-Module AzureRM.Compute -RequiredVersion 2.6.0
    ```
    <span data-ttu-id="0615e-113">Дополнительные сведения см. в разделе [об управлении версиями Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0615e-113">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="generalize-the-windows-vm-using-sysprep"></a><span data-ttu-id="0615e-114">Подготовка виртуальной машины Windows к использованию с помощью Sysprep</span><span class="sxs-lookup"><span data-stu-id="0615e-114">Generalize the Windows VM using Sysprep</span></span>

<span data-ttu-id="0615e-115">Помимо прочих действий Sysprep удаляет все сведения о вашей учетной записи и подготавливает машину к использованию в качестве образа.</span><span class="sxs-lookup"><span data-stu-id="0615e-115">Sysprep removes all your personal account information, among other things, and prepares the machine to be used as an image.</span></span> <span data-ttu-id="0615e-116">Сведения о Sysprep см. в статье [Использование программы Sysprep: введение](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="0615e-116">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="0615e-117">Убедитесь, что Sysprep поддерживает роли сервера, запущенные на компьютере.</span><span class="sxs-lookup"><span data-stu-id="0615e-117">Make sure the server roles running on the machine are supported by Sysprep.</span></span> <span data-ttu-id="0615e-118">Дополнительные сведения см. в статье [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles) (Поддержка серверных ролей в Sysprep).</span><span class="sxs-lookup"><span data-stu-id="0615e-118">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0615e-119">Если вы еще не отправили виртуальный жесткий диск в Azure и собираетесь запустить Sysprep первый раз, прежде чем это делать, [подготовьте виртуальную машину](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0615e-119">If you are running Sysprep before uploading your VHD to Azure for the first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="0615e-120">Выполните вход на виртуальную машину Windows.</span><span class="sxs-lookup"><span data-stu-id="0615e-120">Sign in to the Windows virtual machine.</span></span>
2. <span data-ttu-id="0615e-121">Откройте окно командной строки с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="0615e-121">Open the Command Prompt window as an administrator.</span></span> <span data-ttu-id="0615e-122">Измените каталог на **%windir%\system32\sysprep** и запустите файл `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="0615e-122">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="0615e-123">В диалоговом окне **Программа подготовки системы** выберите **Переход в окно приветствия системы (OOBE)** и убедитесь, что установлен флажок **Подготовка к использованию**.</span><span class="sxs-lookup"><span data-stu-id="0615e-123">In the **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that the **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="0615e-124">В разделе **Параметры завершения работы** выберите **Завершение работы**.</span><span class="sxs-lookup"><span data-stu-id="0615e-124">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="0615e-125">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="0615e-125">Click **OK**.</span></span>
   
    ![Запуск Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="0615e-127">После выполнения всех необходимых действий Sysprep завершает работу виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0615e-127">When Sysprep completes, it shuts down the virtual machine.</span></span> <span data-ttu-id="0615e-128">Не перезапускайте виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="0615e-128">Do not restart the VM.</span></span>



## <a name="log-in-to-azure"></a><span data-ttu-id="0615e-129">Вход в Azure</span><span class="sxs-lookup"><span data-stu-id="0615e-129">Log in to Azure</span></span>
<span data-ttu-id="0615e-130">Если вы еще не установили PowerShell версии 1.4 или выше, то см. статью [How to install and configure Azure PowerShell](/powershell/azure/overview) (Установка и настройка Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="0615e-130">If you don't already have PowerShell version 1.4 or above installed, read [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

1. <span data-ttu-id="0615e-131">Откройте Azure PowerShell и войдите в свою учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="0615e-131">Open Azure PowerShell and sign in to your Azure account.</span></span> <span data-ttu-id="0615e-132">Откроется всплывающее окно для ввода данных учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="0615e-132">A pop-up window opens for you to enter your Azure account credentials.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
2. <span data-ttu-id="0615e-133">Получите идентификаторы доступных вам подписок.</span><span class="sxs-lookup"><span data-stu-id="0615e-133">Get the subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="0615e-134">Укажите соответствующую подписку с помощью идентификатора.</span><span class="sxs-lookup"><span data-stu-id="0615e-134">Set the correct subscription using the subscription ID.</span></span> <span data-ttu-id="0615e-135">Замените *<subscriptionID>* идентификатором правильной подписки.</span><span class="sxs-lookup"><span data-stu-id="0615e-135">Replace *<subscriptionID>* with the ID of the correct subscription.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="get-the-storage-account"></a><span data-ttu-id="0615e-136">Получение учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="0615e-136">Get the storage account</span></span>
<span data-ttu-id="0615e-137">Вам необходима учетная запись хранения Azure для хранения переданного образа виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0615e-137">You need a storage account in Azure to store the uploaded VM image.</span></span> <span data-ttu-id="0615e-138">Можно использовать существующую учетную запись хранения или создать новую.</span><span class="sxs-lookup"><span data-stu-id="0615e-138">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="0615e-139">Если для создания управляемого диска для виртуальной машины будет использоваться виртуальный жесткий диск, то расположение учетной записи хранения должно совпадать с расположением, в котором будет создаваться виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="0615e-139">If you will be using the VHD to create a managed disk for a VM, the storage account location must be same the location where you will be creating the VM.</span></span>

<span data-ttu-id="0615e-140">Чтобы отобразить список доступных учетных записей хранения, введите:</span><span class="sxs-lookup"><span data-stu-id="0615e-140">To show the available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="0615e-141">Если вы хотите использовать существующую учетную запись хранения, то перейдите к разделу [Отправка образа виртуальной машины](#upload-the-vm-vhd-to-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="0615e-141">If you want to use an existing storage account, proceed to the [Upload the VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="0615e-142">Если требуется создать учетную запись хранения, то выполните описанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="0615e-142">If you need to create a storage account, follow these steps:</span></span>

1. <span data-ttu-id="0615e-143">Необходимо указать имя группы ресурсов, в которой будет создана учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="0615e-143">You need the name of the resource group where the storage account should be created.</span></span> <span data-ttu-id="0615e-144">Чтобы найти все группы ресурсов, существующие в вашей подписке, введите:</span><span class="sxs-lookup"><span data-stu-id="0615e-144">To find out all the resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="0615e-145">Чтобы создать группу ресурсов с именем **myResourceGroup** в регионе **Восточная часть США**, введите следующее:</span><span class="sxs-lookup"><span data-stu-id="0615e-145">To create a resource group named **myResourceGroup** in the **East US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "East US"
    ```

2. <span data-ttu-id="0615e-146">С помощью командлета [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) создайте в этой группе ресурсов учетную запись хранения с именем **mystorageaccount**:</span><span class="sxs-lookup"><span data-stu-id="0615e-146">Create a storage account named **mystorageaccount** in this resource group by using the [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "East US"`
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
    <span data-ttu-id="0615e-147">Допустимые значения -SkuName перечислены ниже.</span><span class="sxs-lookup"><span data-stu-id="0615e-147">Valid values for -SkuName are:</span></span>
   
   * <span data-ttu-id="0615e-148">**Standard_LRS** — локально избыточное хранилище.</span><span class="sxs-lookup"><span data-stu-id="0615e-148">**Standard_LRS** - Locally redundant storage.</span></span> 
   * <span data-ttu-id="0615e-149">**Standard_ZRS** — хранилище, избыточное в пределах зоны.</span><span class="sxs-lookup"><span data-stu-id="0615e-149">**Standard_ZRS** - Zone redundant storage.</span></span>
   * <span data-ttu-id="0615e-150">**Standard_GRS** — геоизбыточное хранилище.</span><span class="sxs-lookup"><span data-stu-id="0615e-150">**Standard_GRS** - Geo redundant storage.</span></span> 
   * <span data-ttu-id="0615e-151">**Standard_RAGRS** — геоизбыточное хранилище с доступом только для чтения.</span><span class="sxs-lookup"><span data-stu-id="0615e-151">**Standard_RAGRS** - Read access geo redundant storage.</span></span> 
   * <span data-ttu-id="0615e-152">**Premium_LRS** — локально избыточное хранилище уровня "Премиум".</span><span class="sxs-lookup"><span data-stu-id="0615e-152">**Premium_LRS** - Premium locally redundant storage.</span></span> 

## <a name="upload-the-vhd-to-your-storage-account"></a><span data-ttu-id="0615e-153">Передача виртуального жесткого диска в учетную запись хранения</span><span class="sxs-lookup"><span data-stu-id="0615e-153">Upload the VHD to your storage account</span></span>

<span data-ttu-id="0615e-154">Используйте командлет [Add-AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx), чтобы передать VHD в контейнер в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="0615e-154">Use the [Add-AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) cmdlet to upload the VHD to a container in your storage account.</span></span> <span data-ttu-id="0615e-155">В этом примере файл *myVHD.vhd* передается из расположения *C:\Users\Public\Documents\Virtual hard disks\"* в учетную запись хранения *mystorageaccount*, входящую в группу ресурсов *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="0615e-155">This example uploads the file *myVHD.vhd* from *"C:\Users\Public\Documents\Virtual hard disks\"* to a storage account named *mystorageaccount* in the *myResourceGroup* resource group.</span></span> <span data-ttu-id="0615e-156">Файл будет помещен в контейнер с именем *mycontainer*; новое имя файла — *myUploadedVHD.vhd*.</span><span class="sxs-lookup"><span data-stu-id="0615e-156">The file will be placed into the container named *mycontainer* and the new file name will be *myUploadedVHD.vhd*.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="0615e-157">В случае успешного выполнения отобразится ответ, который выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="0615e-157">If successful, you get a response that looks similar to this:</span></span>

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

<span data-ttu-id="0615e-158">В зависимости от сетевого подключения и размера VHD-файла выполнение этой команды может занять некоторое время.</span><span class="sxs-lookup"><span data-stu-id="0615e-158">Depending on your network connection and the size of your VHD file, this command may take a while to complete</span></span>

<span data-ttu-id="0615e-159">Сохраните путь **URI назначения** для использования в дальнейшем, если вы собираетесь создать управляемый диск или виртуальную машину с помощью переданного виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="0615e-159">Save the **Destination URI** path to use later if you are going to create a managed disk or a new VM using the uploaded VHD.</span></span>

### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="0615e-160">Другие возможности загрузки виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="0615e-160">Other options for uploading a VHD</span></span>
 
 
<span data-ttu-id="0615e-161">Вы также можете передать виртуальный жесткий диск в учетную запись хранения с помощью одного из следующих инструментов:</span><span class="sxs-lookup"><span data-stu-id="0615e-161">You can also upload a VHD to your storage account using one of the following:</span></span>

- [<span data-ttu-id="0615e-162">AzCopy</span><span class="sxs-lookup"><span data-stu-id="0615e-162">AzCopy</span></span>](http://aka.ms/downloadazcopy)
- [<span data-ttu-id="0615e-163">API копирования BLOB-объекта хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="0615e-163">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)
- [<span data-ttu-id="0615e-164">Обозреватель хранилищ Azure для передачи больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="0615e-164">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)
- [<span data-ttu-id="0615e-165">Справочник по API REST служб хранилища импорта и экспорта</span><span class="sxs-lookup"><span data-stu-id="0615e-165">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)
-   <span data-ttu-id="0615e-166">Мы рекомендуем использовать службу импорта и экспорта, если предполагаемое время передачи больше 7 дней.</span><span class="sxs-lookup"><span data-stu-id="0615e-166">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="0615e-167">Чтобы оценить предполагаемое время передачи на основе размера данных и средства передачи, используйте компонент [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html).</span><span class="sxs-lookup"><span data-stu-id="0615e-167">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) to estimate the time from data size and transfer unit.</span></span> 
    <span data-ttu-id="0615e-168">Импорт и экспорт можно использовать для копирования в учетную запись хранения класса Standard.</span><span class="sxs-lookup"><span data-stu-id="0615e-168">Import/Export can be used to copy to a standard storage account.</span></span> <span data-ttu-id="0615e-169">Необходимо осуществить копирование из учетной записи хранения Standard в учетную запись хранения Premium с помощью схожего с AzCopy средства.</span><span class="sxs-lookup"><span data-stu-id="0615e-169">You will need to copy from standard storage to premium storage account using a tool like AzCopy.</span></span>


## <a name="create-a-managed-image-from-the-uploaded-vhd"></a><span data-ttu-id="0615e-170">Создание управляемого образа на основе переданного виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="0615e-170">Create a managed image from the uploaded VHD</span></span> 

<span data-ttu-id="0615e-171">Создайте управляемый образ с помощью универсального виртуального жесткого диска ОС.</span><span class="sxs-lookup"><span data-stu-id="0615e-171">Create a managed image using your generalized OS VHD.</span></span> <span data-ttu-id="0615e-172">Подставьте собственные значения.</span><span class="sxs-lookup"><span data-stu-id="0615e-172">Replace the values with your own information.</span></span>


1.  <span data-ttu-id="0615e-173">Сначала задайте общие параметры.</span><span class="sxs-lookup"><span data-stu-id="0615e-173">First, set the common parameters:</span></span>

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    $vmSize = "Standard_DS1_v2"
    $location = "East US" 
    $imageName = "yourImageName"
    ```

4.  <span data-ttu-id="0615e-174">Создайте образ с помощью универсального виртуального жесткого диска ОС.</span><span class="sxs-lookup"><span data-stu-id="0615e-174">Create the image using your generalized OS VHD.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $urlOfUploadedImageVhd
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```

## <a name="create-a-virtual-network"></a><span data-ttu-id="0615e-175">Создать виртуальную сеть</span><span class="sxs-lookup"><span data-stu-id="0615e-175">Create a virtual network</span></span>
<span data-ttu-id="0615e-176">Создайте виртуальную сеть и подсеть [виртуальной сети](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0615e-176">Create the vNet and subnet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="0615e-177">Создание подсети.</span><span class="sxs-lookup"><span data-stu-id="0615e-177">Create the subnet.</span></span> <span data-ttu-id="0615e-178">В этом примере создается подсеть *mySubnet* с префиксом адреса *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="0615e-178">This example creates a subnet named *mySubnet* with the address prefix of *10.0.0.0/24*.</span></span>  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="0615e-179">Создание виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="0615e-179">Create the virtual network.</span></span> <span data-ttu-id="0615e-180">В этом примере создается виртуальная сеть *myVnet* с префиксом адреса *10.0.0.0/16*.</span><span class="sxs-lookup"><span data-stu-id="0615e-180">This example creates a virtual network named *myVnet* with the address prefix of *10.0.0.0/16*.</span></span>  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="0615e-181">Создание общедоступного IP-адреса и сетевого интерфейса</span><span class="sxs-lookup"><span data-stu-id="0615e-181">Create a public IP address and network interface</span></span>

<span data-ttu-id="0615e-182">Чтобы обеспечить обмен данными с виртуальной машиной в виртуальной сети, требуются [общедоступный IP-адрес](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) и сетевой интерфейс.</span><span class="sxs-lookup"><span data-stu-id="0615e-182">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="0615e-183">Создание общедоступного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="0615e-183">Create a public IP address.</span></span> <span data-ttu-id="0615e-184">В этом примере создается общедоступный IP-адрес с именем *myPip*.</span><span class="sxs-lookup"><span data-stu-id="0615e-184">This example creates a public IP address named *myPip*.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="0615e-185">Создание сетевой карты.</span><span class="sxs-lookup"><span data-stu-id="0615e-185">Create the NIC.</span></span> <span data-ttu-id="0615e-186">В этом примере создается сетевая карта с именем **myNic**.</span><span class="sxs-lookup"><span data-stu-id="0615e-186">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="0615e-187">Создание группы безопасности сети и правила RDP</span><span class="sxs-lookup"><span data-stu-id="0615e-187">Create the network security group and an RDP rule</span></span>

<span data-ttu-id="0615e-188">Чтобы войти на виртуальную машину с помощью RDP, необходимо настроить группу безопасности сети, которая разрешает доступ по протоколу RDP через порт 3389.</span><span class="sxs-lookup"><span data-stu-id="0615e-188">To be able to log in to your VM using RDP, you need to have a network security rule (NSG) that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="0615e-189">В этом примере создается группа безопасности сети с именем *myNsg*, которая содержит правило с именем *myRdpRule*, разрешающее трафик RDP через порт 3389.</span><span class="sxs-lookup"><span data-stu-id="0615e-189">This example creates an NSG named *myNsg* that contains a rule called *myRdpRule* that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="0615e-190">Дополнительные сведения о группах безопасности сети см. в статье [Открытие портов для виртуальной машины в Azure с помощью PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0615e-190">For more information about NSGs, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

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


## <a name="create-a-variable-for-the-virtual-network"></a><span data-ttu-id="0615e-191">Создание переменной для виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="0615e-191">Create a variable for the virtual network</span></span>

<span data-ttu-id="0615e-192">Создайте переменную для готовой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="0615e-192">Create a variable for the completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-the-credentials-for-the-vm"></a><span data-ttu-id="0615e-193">Получение учетных данных для виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="0615e-193">Get the credentials for the VM</span></span>

<span data-ttu-id="0615e-194">Следующий командлет откроет окно, в котором необходимо ввести новое имя пользователя и пароль, используемые в качестве учетной записи локального администратора для удаленного доступа к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="0615e-194">The following cmdlet will open a window where you will enter a new user name and password to use as the local administrator account for remotely accessing the VM.</span></span> 

```powershell
$cred = Get-Credential
```

## <a name="add-the-vm-name-and-size-to-the-vm-configuration"></a><span data-ttu-id="0615e-195">Добавьте имя и размер виртуальной машины в конфигурацию виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0615e-195">Add the VM name and size to the VM configuration.</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-the-vm-image-as-source-image-for-the-new-vm"></a><span data-ttu-id="0615e-196">Настройка образа виртуальной машины в качестве исходного образа для новой виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="0615e-196">Set the VM image as source image for the new VM</span></span>

<span data-ttu-id="0615e-197">Настройте исходный образ, используя идентификатор управляемого образа виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0615e-197">Set the source image using the ID of the managed VM image.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-the-os-configuration-and-add-the-nic"></a><span data-ttu-id="0615e-198">Настройте конфигурацию операционной системы и добавьте сетевую карту.</span><span class="sxs-lookup"><span data-stu-id="0615e-198">Set the OS configuration and add the NIC.</span></span>

<span data-ttu-id="0615e-199">Введите тип хранилища (PremiumLRS или StandardLRS) и размер диска операционной системы.</span><span class="sxs-lookup"><span data-stu-id="0615e-199">Enter the storage type (PremiumLRS or StandardLRS) and the size of the OS disk.</span></span> <span data-ttu-id="0615e-200">В этом примере для типа учетной записи задается значение *PremiumLRS*, для размера диска — *128 ГБ*, а для кэширования диска — *ReadWrite*.</span><span class="sxs-lookup"><span data-stu-id="0615e-200">This example sets the account type to *PremiumLRS*, the disk size to *128 GB* and disk caching to *ReadWrite*.</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-the-vm"></a><span data-ttu-id="0615e-201">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="0615e-201">Create the VM</span></span>

<span data-ttu-id="0615e-202">Создайте виртуальную машину, используя конфигурацию, сохраненную в переменной **$vm**.</span><span class="sxs-lookup"><span data-stu-id="0615e-202">Create the new VM using the configuration stored in the **$vm** variable.</span></span>

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="0615e-203">Проверка создания виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="0615e-203">Verify that the VM was created</span></span>
<span data-ttu-id="0615e-204">После завершения процесса новая виртуальная машина должна отображаться на [портале Azure](https://portal.azure.com) (выберите элементы **Обзор** > **Виртуальные машины**). Ее можно также увидеть, выполнив следующие команды PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0615e-204">When complete, you should see the newly created VM in the [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="0615e-205">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0615e-205">Next steps</span></span>

<span data-ttu-id="0615e-206">Чтобы войти на новую виртуальную машину, найдите ее на [портале](https://portal.azure.com), нажмите кнопку **Подключение**и откройте RDP-файл "Удаленный рабочий стол".</span><span class="sxs-lookup"><span data-stu-id="0615e-206">To sign in to your new virtual machine, browse to the VM in the [portal](https://portal.azure.com), click **Connect**, and open the Remote Desktop RDP file.</span></span> <span data-ttu-id="0615e-207">Для входа на новую виртуальную машину используйте учетные данные для входа в новую виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="0615e-207">Use the account credentials of your original virtual machine to sign in to your new virtual machine.</span></span> <span data-ttu-id="0615e-208">Дополнительные сведения см. в статье [Как подключиться к виртуальной машине Azure под управлением Windows и войти на нее](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0615e-208">For more information, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

