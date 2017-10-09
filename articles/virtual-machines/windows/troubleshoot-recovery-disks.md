---
title: "aaaUse a Windows, устранение неполадок виртуальной Машины с помощью Azure PowerShell | Документы Microsoft"
description: "Узнайте, как проблемы tootroubleshoot виртуальной Машины Windows в Azure путем подключения восстановление tooa диска hello ОС виртуальной Машины с помощью Azure PowerShell"
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
ms.openlocfilehash: 7a6a76f64824fe5d06dc4286cb1d87ab8bb794e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-windows-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-azure-powershell"></a><span data-ttu-id="5d8e8-103">Устранение неполадок виртуальной Машины Windows путем присоединения восстановление tooa диска hello ОС виртуальной Машины с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5d8e8-103">Troubleshoot a Windows VM by attaching hello OS disk tooa recovery VM using Azure PowerShell</span></span>
<span data-ttu-id="5d8e8-104">Если на виртуальной машине (ВМ) в Azure, возникает ошибка загрузки или диск, может потребоваться tooperform устранения неполадок на виртуальном жестком диске hello сам.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-104">If your Windows virtual machine (VM) in Azure encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="5d8e8-105">Распространенным примером будет обновление отказавшего приложения, которое предотвращает hello виртуальной Машины может tooboot успешно.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-105">A common example would be a failed application update that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="5d8e8-106">Этой статьи сведения о том, как Azure PowerShell tooconnect toouse toofix вашего виртуального жесткого диска для виртуальной Машины Windows tooanother ошибок, повторно создать исходной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-106">This article details how toouse Azure PowerShell tooconnect your virtual hard disk tooanother Windows VM toofix any errors, then re-create your original VM.</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="5d8e8-107">Обзор процесса восстановления</span><span class="sxs-lookup"><span data-stu-id="5d8e8-107">Recovery process overview</span></span>
<span data-ttu-id="5d8e8-108">Поиск и устранение неполадок Hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5d8e8-108">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="5d8e8-109">Удалите hello ВМ возникновения проблемы, поддержание hello виртуальных жестких дисков.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-109">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="5d8e8-110">Присоединение и подключить виртуальный жесткий диск hello tooanother виртуальной Машины Windows для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-110">Attach and mount hello virtual hard disk tooanother Windows VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="5d8e8-111">Подключите toohello Устранение неполадок виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-111">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="5d8e8-112">Изменение файлов или выполните любые средства toofix проблемы на hello исходный виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-112">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="5d8e8-113">Отключите образ и отсоединить виртуальный жесткий диск hello из hello, устранение неполадок виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-113">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="5d8e8-114">Создайте виртуальную Машину с помощью hello исходный виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-114">Create a VM using hello original virtual hard disk.</span></span>

<span data-ttu-id="5d8e8-115">Убедитесь, что [hello последнюю версию Azure PowerShell](/powershell/azure/overview) установлен и вход tooyour подписки:</span><span class="sxs-lookup"><span data-stu-id="5d8e8-115">Make sure that you have [hello latest Azure PowerShell](/powershell/azure/overview) installed and logged in tooyour subscription:</span></span>

```powershell
Login-AzureRMAccount
```

<span data-ttu-id="5d8e8-116">В hello следующих примерах замените имена параметров собственные значения.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-116">In hello following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="5d8e8-117">Используемые имена параметров: `myResourceGroup`, `mystorageaccount` и `myVM`.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-117">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="5d8e8-118">Выявление проблем при загрузке</span><span class="sxs-lookup"><span data-stu-id="5d8e8-118">Determine boot issues</span></span>
<span data-ttu-id="5d8e8-119">Можно просмотреть снимок экрана ВМ в Azure toohelp устранения неполадок загрузки.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-119">You can view a screenshot of your VM in Azure toohelp troubleshoot boot issues.</span></span> <span data-ttu-id="5d8e8-120">На этом снимке экрана может помочь определить, почему tooboot сбоя виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-120">This screenshot can help identify why a VM fails tooboot.</span></span> <span data-ttu-id="5d8e8-121">Hello следующий пример возвращает экрана приветствия из виртуальной Машины Windows с именем hello `myVM` в группе ресурсов hello с именем `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="5d8e8-121">hello following example gets hello screenshot from hello Windows VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup `
    -Name myVM -Windows -LocalPath C:\Users\ops\
```

<span data-ttu-id="5d8e8-122">Просмотрите почему hello виртуальной Машины происходит сбой tooboot toodetermine экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-122">Review hello screenshot toodetermine why hello VM is failing tooboot.</span></span> <span data-ttu-id="5d8e8-123">Обратите внимание на соответствующие сообщения об ошибках или коды ошибок.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-123">Note any specific error messages or error codes provided.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="5d8e8-124">Просмотр сведений для существующего виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="5d8e8-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="5d8e8-125">Перед тем как присоединить tooanother вашего виртуального жесткого диска виртуальной Машины, необходимо имя hello tooidentify hello виртуального жесткого диска (VHD).</span><span class="sxs-lookup"><span data-stu-id="5d8e8-125">Before you can attach your virtual hard disk tooanother VM, you need tooidentify hello name of hello virtual hard disk (VHD).</span></span>

<span data-ttu-id="5d8e8-126">Hello следующий пример получает сведения для виртуальной Машины с именем hello `myVM` в группе ресурсов hello с именем `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="5d8e8-126">hello following example gets information for hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="5d8e8-127">Найдите `Vhd URI` внутри hello `StorageProfile` части hello предшествующий команда hello в выходных данных.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-127">Look for `Vhd URI` within hello `StorageProfile` section from hello output of hello preceding command.</span></span> <span data-ttu-id="5d8e8-128">Hello примере усеченные выходных данных ниже показаны hello `Vhd URI` концу hello hello блок кода:</span><span class="sxs-lookup"><span data-stu-id="5d8e8-128">hello following truncated example output shows hello `Vhd URI` towards hello end of hello code block:</span></span>

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


## <a name="delete-existing-vm"></a><span data-ttu-id="5d8e8-129">Удаление существующей виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="5d8e8-129">Delete existing VM</span></span>
<span data-ttu-id="5d8e8-130">Виртуальные жесткие диски и виртуальные машины — это разные ресурсы в Azure.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-130">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="5d8e8-131">Виртуальный жесткий диск является местом hello операционной системы, приложения и конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-131">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="5d8e8-132">Hello самой ВМ — точно так же метаданные, которые определяет hello размер или расположение и ссылки на ресурсы, такие как виртуальный жесткий диск или виртуальный сетевой адаптер (NIC).</span><span class="sxs-lookup"><span data-stu-id="5d8e8-132">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="5d8e8-133">Каждый виртуальный жесткий диск содержит аренды, назначенный при присоединении tooa виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-133">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="5d8e8-134">Несмотря на то, что диски с данными может быть присоединенные и отсоединенные даже в том случае, когда выполняется hello виртуальной Машины, диска ОС hello отключить невозможно, пока удаляется hello ресурса виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-134">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="5d8e8-135">Аренда Hello продолжается tooassociate hello ОС диска с виртуальной Машиной даже в том случае, если этой виртуальной Машины находится в состоянии остановки и освобождается.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-135">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="5d8e8-136">Здравствуйте, первый шаг toorecover ВМ — toodelete hello ВМ сам ресурс.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-136">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="5d8e8-137">Удаление hello ВМ оставляет hello виртуальных жестких дисков в вашей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-137">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="5d8e8-138">После hello удаления виртуальной Машины присоединения hello виртуальный жесткий диск tooanother ВМ tootroubleshoot и устранение ошибок hello.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-138">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="5d8e8-139">Следующий пример удаляет Hello hello виртуальной Машины с именем `myVM` из группы ресурсов hello с именем `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="5d8e8-139">hello following example deletes hello VM named `myVM` from hello resource group named `myResourceGroup`:</span></span>

```powershell
Remove-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="5d8e8-140">Подождите, пока hello ВМ закончит удаление перед присоединением tooanother hello виртуальный жесткий диск виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-140">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="5d8e8-141">Аренда Hello hello виртуальный жесткий диск, который связывает его с hello виртуальной Машины должен toobe выпуска перед тем как присоединить tooanother hello виртуальный жесткий диск виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-141">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="5d8e8-142">Подключить существующий виртуальный жесткий диск tooanother виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="5d8e8-142">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="5d8e8-143">Для Здравствуйте рядом шагах, для устранения неполадок используется другой виртуальной Машиной.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-143">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="5d8e8-144">Подключить существующий виртуальный жесткий диск toothis hello Устранение неполадок виртуальной Машины toobrowse и изменить содержимое диска hello.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-144">You attach hello existing virtual hard disk toothis troubleshooting VM toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="5d8e8-145">Этот процесс позволяет toocorrect все ошибки конфигурации или Просмотр дополнительных приложений или файлы журналов, например системы.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-145">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="5d8e8-146">Выберите или создайте другой toouse виртуальной Машины для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-146">Choose or create another VM toouse for troubleshooting purposes.</span></span>

<span data-ttu-id="5d8e8-147">При присоединении hello существующий виртуальный жесткий диск, укажите диск toohello hello URL-адрес, полученный на предыдущем hello `Get-AzureRmVM` команды.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-147">When you attach hello existing virtual hard disk, specify hello URL toohello disk obtained in hello preceding `Get-AzureRmVM` command.</span></span> <span data-ttu-id="5d8e8-148">Hello примере присоединяет существующий виртуальный жесткий диск toohello Устранение неполадок виртуальной Машины с именем `myVMRecovery` в группе ресурсов hello с именем `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="5d8e8-148">hello following example attaches an existing virtual hard disk toohello troubleshooting VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
Add-AzureRmVMDataDisk -VM $myVM -CreateOption "Attach" -Name "DataDisk" -DiskSizeInGB $null `
    -VhdUri "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

> [!NOTE]
> <span data-ttu-id="5d8e8-149">Добавление диска требует toospecify hello размер диска hello.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-149">Adding a disk requires you toospecify hello size of hello disk.</span></span> <span data-ttu-id="5d8e8-150">Здравствуйте, как мы подключить существующий диск, `-DiskSizeInGB` указывается как `$null`.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-150">As we attach an existing disk, hello `-DiskSizeInGB` is specified as `$null`.</span></span> <span data-ttu-id="5d8e8-151">Это значение обеспечивает hello данных диск подключен правильно и без hello требуется toodetermine hello значение true, размер диска данных.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-151">This value ensures hello data disk is correctly attached, and without hello need toodetermine hello true size of data disk.</span></span>


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="5d8e8-152">Подключить hello подключенный диск данных</span><span class="sxs-lookup"><span data-stu-id="5d8e8-152">Mount hello attached data disk</span></span>

1. <span data-ttu-id="5d8e8-153">Устранение неполадок виртуальной Машины, используя соответствующие учетные данные hello tooyour протокола удаленного рабочего СТОЛА.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-153">RDP tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="5d8e8-154">Hello следующем примере загружаются RDP-файл подключения hello для виртуальной Машины с именем hello `myVMRecovery` в группе ресурсов hello с именем `myResourceGroup`и загружает его слишком`C:\Users\ops\Documents`»</span><span class="sxs-lookup"><span data-stu-id="5d8e8-154">hello following example downloads hello RDP connection file for hello VM named `myVMRecovery` in hello resource group named `myResourceGroup`, and downloads it too`C:\Users\ops\Documents`"</span></span>

    ```powershell
    Get-AzureRMRemoteDesktopFile -ResourceGroupName "myResourceGroup" -Name "myVMRecovery" `
        -LocalPath "C:\Users\ops\Documents\myVMRecovery.rdp"
    ```

2. <span data-ttu-id="5d8e8-155">диск данных Hello автоматически обнаружены и подсоединен.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-155">hello data disk is automatically detected and attached.</span></span> <span data-ttu-id="5d8e8-156">Просмотрите список hello букву диска hello присоединенных томах toodetermine следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5d8e8-156">View hello list of attached volumes toodetermine hello drive letter as follows:</span></span>

    ```powershell
    Get-Disk
    ```

    <span data-ttu-id="5d8e8-157">Следующий пример выходных данных Hello показывает hello виртуального жесткого диска, подключенного диска **2**.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-157">hello following example output shows hello virtual hard disk connected a disk **2**.</span></span> <span data-ttu-id="5d8e8-158">(Можно также использовать `Get-Volume` букву диска hello tooview):</span><span class="sxs-lookup"><span data-stu-id="5d8e8-158">(You can also use `Get-Volume` tooview hello drive letter):</span></span>

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Online       127 GB MBR
    ```

## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="5d8e8-159">Устранение неполадок на исходном виртуальном жестком диске</span><span class="sxs-lookup"><span data-stu-id="5d8e8-159">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="5d8e8-160">С hello существующий виртуальный жесткий диск подключен теперь можно выполнять обслуживание и действия по устранению неполадок при необходимости.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-160">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="5d8e8-161">После разрешения проблемы hello продолжите hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-161">Once you have addressed hello issues, continue with hello following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="5d8e8-162">Отключение и отсоединение исходного виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="5d8e8-162">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="5d8e8-163">После разрешения ошибки, можно отключить и отсоединение hello существующий виртуальный жесткий диск от виртуальной Машины по устранению неполадок.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-163">Once your errors are resolved, you unmount and detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="5d8e8-164">Расположение виртуального жесткого диска нельзя использовать с любой другой ВМ до освобождения аренды hello присоединение toohello hello виртуального жесткого диска, устранение неполадок виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-164">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="5d8e8-165">Из в рамках вашего сеанса RDP отсоединить диск данных hello на виртуальной Машине восстановления.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-165">From within your RDP session, unmount hello data disk on your recovery VM.</span></span> <span data-ttu-id="5d8e8-166">Требуется номер диска hello из hello предыдущих `Get-Disk` командлета.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-166">You need hello disk number from hello previous `Get-Disk` cmdlet.</span></span> <span data-ttu-id="5d8e8-167">Затем с помощью `Set-Disk` tooset hello диск как:</span><span class="sxs-lookup"><span data-stu-id="5d8e8-167">Then, use `Set-Disk` tooset hello disk as offline:</span></span>

    ```powershell
    Set-Disk -Number 2 -IsOffline $True
    ```

    <span data-ttu-id="5d8e8-168">Подтвердите hello диск теперь задан как вне сети с помощью `Get-Disk` еще раз.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-168">Confirm hello disk is now set as offline using `Get-Disk` again.</span></span> <span data-ttu-id="5d8e8-169">Hello в выводе следующего примера показаны hello диск теперь задан как вне сети:</span><span class="sxs-lookup"><span data-stu-id="5d8e8-169">hello following example output shows hello disk is now set as offline:</span></span>

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Offline      127 GB MBR
    ```

2. <span data-ttu-id="5d8e8-170">Выйдите из сеанса RDP.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-170">Exit your RDP session.</span></span> <span data-ttu-id="5d8e8-171">Удалите из свой сеанс Azure PowerShell hello виртуального жесткого диска из hello, устранение неполадок виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-171">From your Azure PowerShell session, remove hello virtual hard disk from hello troubleshooting VM.</span></span>

    ```powershell
    $myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
    Remove-AzureRmVMDataDisk -VM $myVM -Name "DataDisk"
    Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="5d8e8-172">Создание виртуальной машины из исходного жесткого диска</span><span class="sxs-lookup"><span data-stu-id="5d8e8-172">Create VM from original hard disk</span></span>
<span data-ttu-id="5d8e8-173">использовать ВМ с исходного виртуального жесткого диска, toocreate [этого шаблона Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="5d8e8-173">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="5d8e8-174">шаблон фактического JSON Hello находится в hello по ссылке:</span><span class="sxs-lookup"><span data-stu-id="5d8e8-174">hello actual JSON template is at hello following link:</span></span>

- <span data-ttu-id="5d8e8-175">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="5d8e8-175">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json</span></span>

<span data-ttu-id="5d8e8-176">шаблон Hello развертывания ВМ в существующей виртуальной сети, с помощью hello URL-адрес VHD из hello ранее команд.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-176">hello template deploys a VM into an existing virtual network, using hello VHD URL from hello earlier command.</span></span> <span data-ttu-id="5d8e8-177">Hello примере развертывает hello шаблона toohello ресурсов группы с именем `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="5d8e8-177">hello following example deploys hello template toohello resource group named `myResourceGroup`:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name myDeployment -ResourceGroupName myResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json
```

<span data-ttu-id="5d8e8-178">Hello ответов запрашивает hello шаблона, такие как имя виртуальной Машины, тип операционной системы и размер виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-178">Answer hello prompts for hello template such as VM name, OS type, and VM size.</span></span> <span data-ttu-id="5d8e8-179">Hello `osDiskVhdUri` Здравствуйте, же, как уже используется при присоединении hello существующий виртуальный жесткий диск toohello Устранение неполадок виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-179">hello `osDiskVhdUri` is hello same as previously used when attaching hello existing virtual hard disk toohello troubleshooting VM.</span></span>


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="5d8e8-180">Восстановление диагностики загрузки</span><span class="sxs-lookup"><span data-stu-id="5d8e8-180">Re-enable boot diagnostics</span></span>

<span data-ttu-id="5d8e8-181">При создании ВМ из hello существующий виртуальный жесткий диск, диагностика загрузки может не быть доступной.</span><span class="sxs-lookup"><span data-stu-id="5d8e8-181">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="5d8e8-182">Hello следующий пример включает hello диагностического расширения для виртуальной Машины с именем hello `myVMDeployed` в группе ресурсов hello с именем `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="5d8e8-182">hello following example enables hello diagnostic extension on hello VM named `myVMDeployed` in hello resource group named `myResourceGroup`:</span></span>

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMDeployed"
Set-AzureRmVMBootDiagnostics -ResourceGroupName myResourceGroup -VM $myVM -enable
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

## <a name="next-steps"></a><span data-ttu-id="5d8e8-183">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5d8e8-183">Next steps</span></span>
<span data-ttu-id="5d8e8-184">Если возникают проблемы с подключением tooyour виртуальной Машины, см. раздел [tooan подключений RDP, устранение неполадок виртуальной Машины Azure](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5d8e8-184">If you are having issues connecting tooyour VM, see [Troubleshoot RDP connections tooan Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="5d8e8-185">Для устранения проблем с доступом к приложениям, выполняющимся на виртуальной машине, прочитайте статью [Устранение неполадок доступа к приложению, выполняющемуся в виртуальной машине Azure](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5d8e8-185">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Windows VM](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="5d8e8-186">Дополнительные сведения об использовании Resource Manager вы найдете в статье [Общие сведения об Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5d8e8-186">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
