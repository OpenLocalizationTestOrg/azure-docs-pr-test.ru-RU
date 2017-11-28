---
title: "Использование виртуальной машины Windows для устранения неполадок с помощью Azure PowerShell | Документация Майкрософт"
description: "Узнайте, как устранять неполадки с виртуальными машинами Windows в Azure, подключив диск операционной системы к виртуальной машине восстановления с помощью Azure PowerShell."
services: virtual-machines-windows
documentationCenter: 
authors: genlin
manager: timlt
editor: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 8b7821b4285e73d461af426bfdfb3fdcc4454517
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-a-windows-vm-by-attaching-the-os-disk-to-a-recovery-vm-using-azure-powershell"></a><span data-ttu-id="89f99-103">Устранение неполадок с виртуальной машиной Windows при подключении диска операционной системы к виртуальной машине восстановления с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="89f99-103">Troubleshoot a Windows VM by attaching the OS disk to a recovery VM using Azure PowerShell</span></span>
<span data-ttu-id="89f99-104">Если возникает проблема с загрузкой или диском на виртуальной машине Windows в Azure, возможно, вам нужно устранить неполадки, связанные с самим виртуальным жестким диском.</span><span class="sxs-lookup"><span data-stu-id="89f99-104">If your Windows virtual machine (VM) in Azure encounters a boot or disk error, you may need to perform troubleshooting steps on the virtual hard disk itself.</span></span> <span data-ttu-id="89f99-105">Например, такая ситуация может возникнуть из-за сбоя обновления приложения, который мешает успешно загрузить виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="89f99-105">A common example would be a failed application update that prevents the VM from being able to boot successfully.</span></span> <span data-ttu-id="89f99-106">В этой статье подробно описано, как с помощью Azure PowerShell подключить виртуальный жесткий диск к другой виртуальной машине Windows для устранения ошибок, а затем восстановить исходную виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="89f99-106">This article details how to use Azure PowerShell to connect your virtual hard disk to another Windows VM to fix any errors, then re-create your original VM.</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="89f99-107">Обзор процесса восстановления</span><span class="sxs-lookup"><span data-stu-id="89f99-107">Recovery process overview</span></span>
<span data-ttu-id="89f99-108">Процесс устранения неполадок выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="89f99-108">The troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="89f99-109">Удалите виртуальную машину, на которой возникли проблемы, сохранив ее виртуальные жесткие диски.</span><span class="sxs-lookup"><span data-stu-id="89f99-109">Delete the VM encountering issues, keeping the virtual hard disks.</span></span>
2. <span data-ttu-id="89f99-110">Присоедините и подключите виртуальный жесткий диск к другой виртуальной машине Windows для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="89f99-110">Attach and mount the virtual hard disk to another Windows VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="89f99-111">Подключитесь к этой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="89f99-111">Connect to the troubleshooting VM.</span></span> <span data-ttu-id="89f99-112">Измените файлы или запустите средства, которые нужны для устранения неполадок на исходном виртуальном жестком диске.</span><span class="sxs-lookup"><span data-stu-id="89f99-112">Edit files or run any tools to fix issues on the original virtual hard disk.</span></span>
4. <span data-ttu-id="89f99-113">Отключите и отсоедините виртуальный жесткий диск от виртуальной машины, на которой выполняется устранение неполадок.</span><span class="sxs-lookup"><span data-stu-id="89f99-113">Unmount and detach the virtual hard disk from the troubleshooting VM.</span></span>
5. <span data-ttu-id="89f99-114">Создайте другую виртуальную машину, используя исходный виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="89f99-114">Create a VM using the original virtual hard disk.</span></span>

<span data-ttu-id="89f99-115">Убедитесь, что у вас установлена и настроена [последняя версия Azure PowerShell](/powershell/azure/overview) и выполнен вход в подписку.</span><span class="sxs-lookup"><span data-stu-id="89f99-115">Make sure that you have [the latest Azure PowerShell](/powershell/azure/overview) installed and logged in to your subscription:</span></span>

```powershell
Login-AzureRMAccount
```

<span data-ttu-id="89f99-116">В следующих примерах замените имена параметров собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="89f99-116">In the following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="89f99-117">Используемые имена параметров: `myResourceGroup`, `mystorageaccount` и `myVM`.</span><span class="sxs-lookup"><span data-stu-id="89f99-117">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="89f99-118">Выявление проблем при загрузке</span><span class="sxs-lookup"><span data-stu-id="89f99-118">Determine boot issues</span></span>
<span data-ttu-id="89f99-119">Вы можете просмотреть снимок экрана виртуальной машины в Azure, чтобы устранить неполадки загрузки.</span><span class="sxs-lookup"><span data-stu-id="89f99-119">You can view a screenshot of your VM in Azure to help troubleshoot boot issues.</span></span> <span data-ttu-id="89f99-120">Этот снимок экрана может помочь определить, почему виртуальная машина не загружается.</span><span class="sxs-lookup"><span data-stu-id="89f99-120">This screenshot can help identify why a VM fails to boot.</span></span> <span data-ttu-id="89f99-121">Приведенный ниже пример получает снимок экрана виртуальной машины Windows `myVM`, расположенной в группе ресурсов `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="89f99-121">The following example gets the screenshot from the Windows VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup `
    -Name myVM -Windows -LocalPath C:\Users\ops\
```

<span data-ttu-id="89f99-122">Просмотрите его, чтобы определить причину сбоя загрузки виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="89f99-122">Review the screenshot to determine why the VM is failing to boot.</span></span> <span data-ttu-id="89f99-123">Обратите внимание на соответствующие сообщения об ошибках или коды ошибок.</span><span class="sxs-lookup"><span data-stu-id="89f99-123">Note any specific error messages or error codes provided.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="89f99-124">Просмотр сведений для существующего виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="89f99-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="89f99-125">Прежде чем присоединить виртуальный жесткий диск к другой виртуальной машине, следует определить имя этого виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="89f99-125">Before you can attach your virtual hard disk to another VM, you need to identify the name of the virtual hard disk (VHD).</span></span>

<span data-ttu-id="89f99-126">В следующем примере возвращаются сведения о виртуальной машине `myVM` в группе ресурсов `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="89f99-126">The following example gets information for the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="89f99-127">Найдите `Vhd URI` в разделе `StorageProfile` выходных данных предыдущей команды.</span><span class="sxs-lookup"><span data-stu-id="89f99-127">Look for `Vhd URI` within the `StorageProfile` section from the output of the preceding command.</span></span> <span data-ttu-id="89f99-128">Приведенный ниже усеченный пример выходных данных содержит `Vhd URI` в конце блока кода.</span><span class="sxs-lookup"><span data-stu-id="89f99-128">The following truncated example output shows the `Vhd URI` towards the end of the code block:</span></span>

```powershell
RequestId                     : 8a134642-2f01-4e08-bb12-d89b5b81a0a0
StatusCode                    : OK
ResourceGroupName             : myResourceGroup
Id                            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM
Name                          : myVM
Type                          : Microsoft.Compute/virtualMachines
...
StorageProfile                :
  ImageReference              :
    Publisher                 : MicrosoftWindowsServer
    Offer                     : WindowsServer
    Sku                       : 2016-Datacenter
    Version                   : latest
  OsDisk                      :
    OsType                    : Windows
    Name                      : myVM
    Vhd                       :
      Uri                     : https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    Caching                   : ReadWrite
    CreateOption              : FromImage
```


## <a name="delete-existing-vm"></a><span data-ttu-id="89f99-129">Удаление существующей виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="89f99-129">Delete existing VM</span></span>
<span data-ttu-id="89f99-130">Виртуальные жесткие диски и виртуальные машины — это разные ресурсы в Azure.</span><span class="sxs-lookup"><span data-stu-id="89f99-130">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="89f99-131">Виртуальный жесткий диск является местом хранения операционной системы, приложений и конфигурации.</span><span class="sxs-lookup"><span data-stu-id="89f99-131">A virtual hard disk is where the operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="89f99-132">Виртуальная машина — это просто метаданные, которые определяют размер или расположение объекта, а также ссылки на ресурсы, такие как виртуальные жесткие диски или виртуальные сетевые адаптеры.</span><span class="sxs-lookup"><span data-stu-id="89f99-132">The VM itself is just metadata that defines the size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="89f99-133">При присоединении виртуального жесткого диска к виртуальной машине для него регистрируется аренда.</span><span class="sxs-lookup"><span data-stu-id="89f99-133">Each virtual hard disk has a lease assigned when attached to a VM.</span></span> <span data-ttu-id="89f99-134">Диски данных можно присоединять и отсоединять во время работы виртуальной машины, но диск операционной системы отсоединить невозможно, пока ресурс виртуальной машины не будет удален.</span><span class="sxs-lookup"><span data-stu-id="89f99-134">Although data disks can be attached and detached even while the VM is running, the OS disk cannot be detached unless the VM resource is deleted.</span></span> <span data-ttu-id="89f99-135">Аренда сохраняет привязку диска операционной системы к виртуальной машине, даже когда эта виртуальная машина остановлена или отменено ее распределение.</span><span class="sxs-lookup"><span data-stu-id="89f99-135">The lease continues to associate the OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="89f99-136">Поэтому для восстановления виртуальной машины нужно прежде всего удалить ресурс виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="89f99-136">The first step to recover your VM is to delete the VM resource itself.</span></span> <span data-ttu-id="89f99-137">Удаление виртуальной машины не повлияет на виртуальные жесткие диски, размещенные в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="89f99-137">Deleting the VM leaves the virtual hard disks in your storage account.</span></span> <span data-ttu-id="89f99-138">После удаления виртуальной машины присоедините виртуальный жесткий диск к другой виртуальной машине, чтобы устранить неполадки.</span><span class="sxs-lookup"><span data-stu-id="89f99-138">After the VM is deleted, you attach the virtual hard disk to another VM to troubleshoot and resolve the errors.</span></span>

<span data-ttu-id="89f99-139">В следующем примере виртуальная машина `myVM` удаляется из группы ресурсов `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="89f99-139">The following example deletes the VM named `myVM` from the resource group named `myResourceGroup`:</span></span>

```powershell
Remove-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="89f99-140">Дождитесь, пока удаление завершится, прежде чем присоединять виртуальный жесткий диск к другой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="89f99-140">Wait until the VM has finished deleting before you attach the virtual hard disk to another VM.</span></span> <span data-ttu-id="89f99-141">Чтобы присоединить виртуальный жесткий диск к другой виртуальной машине, необходимо снять аренду, которая привязывает диск к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="89f99-141">The lease on the virtual hard disk that associates it with the VM needs to be released before you can attach the virtual hard disk to another VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-to-another-vm"></a><span data-ttu-id="89f99-142">Присоединение существующего виртуального жесткого диска к другой виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="89f99-142">Attach existing virtual hard disk to another VM</span></span>
<span data-ttu-id="89f99-143">В следующих нескольких шагах описывается использование другой виртуальной машины для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="89f99-143">For the next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="89f99-144">Присоедините существующий виртуальный жесткий диск к виртуальной машине для устранения неполадок, чтобы просматривать и изменять содержимое диска.</span><span class="sxs-lookup"><span data-stu-id="89f99-144">You attach the existing virtual hard disk to this troubleshooting VM to browse and edit the disk's content.</span></span> <span data-ttu-id="89f99-145">Этот процесс позволяет, например, исправить ошибки конфигурации или изучить дополнительные журналы протоколов или системы.</span><span class="sxs-lookup"><span data-stu-id="89f99-145">This process allows you to correct any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="89f99-146">Выберите или создайте другую виртуальную машину, которая будет использоваться для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="89f99-146">Choose or create another VM to use for troubleshooting purposes.</span></span>

<span data-ttu-id="89f99-147">При присоединении существующего виртуального жесткого диска укажите URL-адрес диска, полученный в предыдущей команде `Get-AzureRmVM`.</span><span class="sxs-lookup"><span data-stu-id="89f99-147">When you attach the existing virtual hard disk, specify the URL to the disk obtained in the preceding `Get-AzureRmVM` command.</span></span> <span data-ttu-id="89f99-148">В следующем примере существующий виртуальный жесткий диск присоединяется к виртуальной машине для устранения неполадок `myVMRecovery` в группе ресурсов `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="89f99-148">The following example attaches an existing virtual hard disk to the troubleshooting VM named `myVMRecovery` in the resource group named `myResourceGroup`:</span></span>

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
Add-AzureRmVMDataDisk -VM $myVM -CreateOption "Attach" -Name "DataDisk" -DiskSizeInGB $null `
    -VhdUri "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

> [!NOTE]
> <span data-ttu-id="89f99-149">Для добавления диска необходимо указать его размер.</span><span class="sxs-lookup"><span data-stu-id="89f99-149">Adding a disk requires you to specify the size of the disk.</span></span> <span data-ttu-id="89f99-150">Так как мы подключаем существующий диск, `-DiskSizeInGB` имеет значение `$null`.</span><span class="sxs-lookup"><span data-stu-id="89f99-150">As we attach an existing disk, the `-DiskSizeInGB` is specified as `$null`.</span></span> <span data-ttu-id="89f99-151">Это значение обеспечивает правильное подключение диска данных без необходимости определять его фактический размер.</span><span class="sxs-lookup"><span data-stu-id="89f99-151">This value ensures the data disk is correctly attached, and without the need to determine the true size of data disk.</span></span>


## <a name="mount-the-attached-data-disk"></a><span data-ttu-id="89f99-152">Подключение присоединенного диска данных</span><span class="sxs-lookup"><span data-stu-id="89f99-152">Mount the attached data disk</span></span>

1. <span data-ttu-id="89f99-153">Подключитесь к виртуальной машине для устранения неполадок по протоколу RDP, используя соответствующие учетные данные.</span><span class="sxs-lookup"><span data-stu-id="89f99-153">RDP to your troubleshooting VM using the appropriate credentials.</span></span> <span data-ttu-id="89f99-154">Следующий пример скачивает RDP-файл подключения для виртуальной машины `myVMRecovery` в группе ресурсов `myResourceGroup` и сохраняет его в паку `C:\Users\ops\Documents`.</span><span class="sxs-lookup"><span data-stu-id="89f99-154">The following example downloads the RDP connection file for the VM named `myVMRecovery` in the resource group named `myResourceGroup`, and downloads it to `C:\Users\ops\Documents`"</span></span>

    ```powershell
    Get-AzureRMRemoteDesktopFile -ResourceGroupName "myResourceGroup" -Name "myVMRecovery" `
        -LocalPath "C:\Users\ops\Documents\myVMRecovery.rdp"
    ```

2. <span data-ttu-id="89f99-155">Диск данных будет автоматически обнаружен и подключен.</span><span class="sxs-lookup"><span data-stu-id="89f99-155">The data disk is automatically detected and attached.</span></span> <span data-ttu-id="89f99-156">Просмотрите список подключенных томов, чтобы определить букву диска, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="89f99-156">View the list of attached volumes to determine the drive letter as follows:</span></span>

    ```powershell
    Get-Disk
    ```

    <span data-ttu-id="89f99-157">В следующем примере выходных данных показан виртуальный жесткий диск, подключенный как диск **2**.</span><span class="sxs-lookup"><span data-stu-id="89f99-157">The following example output shows the virtual hard disk connected a disk **2**.</span></span> <span data-ttu-id="89f99-158">(Для просмотра буква диска можно также использовать `Get-Volume`).</span><span class="sxs-lookup"><span data-stu-id="89f99-158">(You can also use `Get-Volume` to view the drive letter):</span></span>

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Online       127 GB MBR
    ```

## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="89f99-159">Устранение неполадок на исходном виртуальном жестком диске</span><span class="sxs-lookup"><span data-stu-id="89f99-159">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="89f99-160">Теперь, когда существующий виртуальный жесткий диск подключен, вы можете выполнить любые необходимые действия по обслуживанию и (или) устранению неполадок.</span><span class="sxs-lookup"><span data-stu-id="89f99-160">With the existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="89f99-161">После устранения проблем выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="89f99-161">Once you have addressed the issues, continue with the following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="89f99-162">Отключение и отсоединение исходного виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="89f99-162">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="89f99-163">После устранения ошибок отключите и отсоедините существующий виртуальный жесткий диск от виртуальной машины, использованный для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="89f99-163">Once your errors are resolved, you unmount and detach the existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="89f99-164">Виртуальный жесткий диск нельзя использовать с другой виртуальной машиной, пока вы не отмените аренду, присоединяющую виртуальный жесткий диск к виртуальной машине для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="89f99-164">You cannot use your virtual hard disk with any other VM until the lease attaching the virtual hard disk to the troubleshooting VM is released.</span></span>

1. <span data-ttu-id="89f99-165">Из сеанса RDP отключите диск данных на виртуальной машине восстановления.</span><span class="sxs-lookup"><span data-stu-id="89f99-165">From within your RDP session, unmount the data disk on your recovery VM.</span></span> <span data-ttu-id="89f99-166">Для этого нужен номер диска из предыдущего командлета `Get-Disk`.</span><span class="sxs-lookup"><span data-stu-id="89f99-166">You need the disk number from the previous `Get-Disk` cmdlet.</span></span> <span data-ttu-id="89f99-167">Используйте `Set-Disk`, чтобы отключить диск.</span><span class="sxs-lookup"><span data-stu-id="89f99-167">Then, use `Set-Disk` to set the disk as offline:</span></span>

    ```powershell
    Set-Disk -Number 2 -IsOffline $True
    ```

    <span data-ttu-id="89f99-168">Убедитесь, что диск отключен, еще раз выполнив `Get-Disk`.</span><span class="sxs-lookup"><span data-stu-id="89f99-168">Confirm the disk is now set as offline using `Get-Disk` again.</span></span> <span data-ttu-id="89f99-169">В следующем примере выходных данных показано, что теперь диск отключен.</span><span class="sxs-lookup"><span data-stu-id="89f99-169">The following example output shows the disk is now set as offline:</span></span>

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Offline      127 GB MBR
    ```

2. <span data-ttu-id="89f99-170">Выйдите из сеанса RDP.</span><span class="sxs-lookup"><span data-stu-id="89f99-170">Exit your RDP session.</span></span> <span data-ttu-id="89f99-171">Из сеанса Azure PowerShell удалите виртуальный жесткий диск с виртуальной машины для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="89f99-171">From your Azure PowerShell session, remove the virtual hard disk from the troubleshooting VM.</span></span>

    ```powershell
    $myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
    Remove-AzureRmVMDataDisk -VM $myVM -Name "DataDisk"
    Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="89f99-172">Создание виртуальной машины из исходного жесткого диска</span><span class="sxs-lookup"><span data-stu-id="89f99-172">Create VM from original hard disk</span></span>
<span data-ttu-id="89f99-173">Чтобы создать виртуальную машину из исходного виртуального жесткого диска, используйте [этот шаблон Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="89f99-173">To create a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="89f99-174">Фактический шаблон JSON доступен по следующей ссылке:</span><span class="sxs-lookup"><span data-stu-id="89f99-174">The actual JSON template is at the following link:</span></span>

- <span data-ttu-id="89f99-175">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="89f99-175">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json</span></span>

<span data-ttu-id="89f99-176">Этот шаблон развертывает виртуальную машину в существующую виртуальную сеть, используя URL-адрес виртуального жесткого диска из использованной выше команды.</span><span class="sxs-lookup"><span data-stu-id="89f99-176">The template deploys a VM into an existing virtual network, using the VHD URL from the earlier command.</span></span> <span data-ttu-id="89f99-177">В следующем примере шаблон развертывается в группе ресурсов `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="89f99-177">The following example deploys the template to the resource group named `myResourceGroup`:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name myDeployment -ResourceGroupName myResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json
```

<span data-ttu-id="89f99-178">Укажите сведения в ответ на запросы шаблона, такие как имя виртуальной машины, тип операционной системы и размер виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="89f99-178">Answer the prompts for the template such as VM name, OS type, and VM size.</span></span> <span data-ttu-id="89f99-179">Используется то же значение `osDiskVhdUri`, что и при присоединении существующего виртуального жесткого диска к виртуальной машине для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="89f99-179">The `osDiskVhdUri` is the same as previously used when attaching the existing virtual hard disk to the troubleshooting VM.</span></span>


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="89f99-180">Восстановление диагностики загрузки</span><span class="sxs-lookup"><span data-stu-id="89f99-180">Re-enable boot diagnostics</span></span>

<span data-ttu-id="89f99-181">При создании виртуальной машины на основе существующего виртуального жесткого диска диагностика загрузки не всегда автоматически включена.</span><span class="sxs-lookup"><span data-stu-id="89f99-181">When you create your VM from the existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="89f99-182">В следующем примере на виртуальной машине `myVMDeployed` в группе ресурсов `myResourceGroup` включается расширение диагностики:</span><span class="sxs-lookup"><span data-stu-id="89f99-182">The following example enables the diagnostic extension on the VM named `myVMDeployed` in the resource group named `myResourceGroup`:</span></span>

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMDeployed"
Set-AzureRmVMBootDiagnostics -ResourceGroupName myResourceGroup -VM $myVM -enable
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

## <a name="next-steps"></a><span data-ttu-id="89f99-183">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="89f99-183">Next steps</span></span>
<span data-ttu-id="89f99-184">При возникновении проблем с подключением к виртуальной машине ознакомьтесь со статьей [Устранение неполадок с подключением к удаленному рабочему столу на виртуальной машине Azure под управлением Windows](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="89f99-184">If you are having issues connecting to your VM, see [Troubleshoot RDP connections to an Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="89f99-185">Для устранения проблем с доступом к приложениям, выполняющимся на виртуальной машине, прочитайте статью [Устранение неполадок доступа к приложению, выполняющемуся в виртуальной машине Azure](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="89f99-185">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Windows VM](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="89f99-186">Дополнительные сведения об использовании Resource Manager вы найдете в статье [Общие сведения об Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="89f99-186">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
