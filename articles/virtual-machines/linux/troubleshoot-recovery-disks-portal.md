---
title: "Использование виртуальной машины Linux для устранения неполадок с помощью портала Azure | Документация Майкрософт"
description: "Узнайте, как устранять неполадки с виртуальными машинами Linux, подключив диск операционной системы к виртуальной машине восстановления с помощью портала Azure."
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 11/14/2016
ms.author: iainfou
ms.openlocfilehash: c96ff625c3e83f6fc9057f1163c877e8e0aed5e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-the-os-disk-to-a-recovery-vm-using-the-azure-portal"></a><span data-ttu-id="8c02f-103">Устранение неполадок с виртуальной машиной Linux при присоединении диска операционной системы к виртуальной машине восстановления с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="8c02f-103">Troubleshoot a Linux VM by attaching the OS disk to a recovery VM using the Azure portal</span></span>
<span data-ttu-id="8c02f-104">Если возникает проблема с загрузкой или диском на виртуальной машине Linux, возможно, вам нужно устранить неполадки, связанные с самим виртуальным жестким диском.</span><span class="sxs-lookup"><span data-stu-id="8c02f-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need to perform troubleshooting steps on the virtual hard disk itself.</span></span> <span data-ttu-id="8c02f-105">Например, такая ситуация возникает из-за неправильной записи в `/etc/fstab`, которая мешает успешно загрузить виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="8c02f-105">A common example would be an invalid entry in `/etc/fstab` that prevents the VM from being able to boot successfully.</span></span> <span data-ttu-id="8c02f-106">В этой статье подробно описано, как с помощью портала Azure подключить виртуальный жесткий диск к другой виртуальной машине Linux для устранения ошибок, а затем восстановить исходную виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="8c02f-106">This article details how to use the Azure portal to connect your virtual hard disk to another Linux VM to fix any errors, then re-create your original VM.</span></span>

## <a name="recovery-process-overview"></a><span data-ttu-id="8c02f-107">Обзор процесса восстановления</span><span class="sxs-lookup"><span data-stu-id="8c02f-107">Recovery process overview</span></span>
<span data-ttu-id="8c02f-108">Процесс устранения неполадок выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="8c02f-108">The troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="8c02f-109">Удалите виртуальную машину, на которой возникли проблемы, сохранив ее виртуальные жесткие диски.</span><span class="sxs-lookup"><span data-stu-id="8c02f-109">Delete the VM encountering issues, keeping the virtual hard disks.</span></span>
2. <span data-ttu-id="8c02f-110">Присоедините и подключите виртуальный жесткий диск к другой виртуальной машине Linux для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="8c02f-110">Attach and mount the virtual hard disk to another Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="8c02f-111">Подключитесь к этой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="8c02f-111">Connect to the troubleshooting VM.</span></span> <span data-ttu-id="8c02f-112">Измените файлы или запустите средства, которые нужны для устранения неполадок на исходном виртуальном жестком диске.</span><span class="sxs-lookup"><span data-stu-id="8c02f-112">Edit files or run any tools to fix issues on the original virtual hard disk.</span></span>
4. <span data-ttu-id="8c02f-113">Отключите и отсоедините виртуальный жесткий диск от виртуальной машины, на которой выполняется устранение неполадок.</span><span class="sxs-lookup"><span data-stu-id="8c02f-113">Unmount and detach the virtual hard disk from the troubleshooting VM.</span></span>
5. <span data-ttu-id="8c02f-114">Создайте другую виртуальную машину, используя исходный виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="8c02f-114">Create a VM using the original virtual hard disk.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="8c02f-115">Выявление проблем при загрузке</span><span class="sxs-lookup"><span data-stu-id="8c02f-115">Determine boot issues</span></span>
<span data-ttu-id="8c02f-116">Изучите диагностические сведения о загрузке и снимки экранов виртуальной машины, чтобы определить, почему виртуальная машина не может правильно загрузиться.</span><span class="sxs-lookup"><span data-stu-id="8c02f-116">Examine the boot diagnostics and VM screenshot to determine why your VM is not able to boot correctly.</span></span> <span data-ttu-id="8c02f-117">Например, причиной может быть неправильная запись в `/etc/fstab`, удаление или перемещение базового виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="8c02f-117">A common example would be an invalid entry in `/etc/fstab`, or an underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="8c02f-118">Выберите на портале эту виртуальную машину и прокрутите экран вниз до раздела **Поддержка и устранение неполадок**.</span><span class="sxs-lookup"><span data-stu-id="8c02f-118">Select your VM in the portal and then scroll down to the **Support + Troubleshooting** section.</span></span> <span data-ttu-id="8c02f-119">Щелкните **Диагностика загрузки**, чтобы просмотреть сообщения консоли, транслируемые с виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="8c02f-119">Click **Boot diagnostics** to view the console messages streamed from your VM.</span></span> <span data-ttu-id="8c02f-120">Изучите журналы консоли и постарайтесь определить, что вызывает проблему на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="8c02f-120">Review the console logs to see if you can determine why the VM is encountering an issue.</span></span> <span data-ttu-id="8c02f-121">В следующем примере мы видим, что виртуальная машина не может выйти из режима обслуживания и требует вмешательства оператора.</span><span class="sxs-lookup"><span data-stu-id="8c02f-121">The following example shows a VM stuck in maintenance mode that requires manual interaction:</span></span>

![Просмотр журналов консоли для диагностики загрузки виртуальной машины](./media/troubleshoot-recovery-disks-portal/boot-diagnostics-error.png)

<span data-ttu-id="8c02f-123">Можно также щелкнуть **Снимок экрана** в верхней части журнала диагностики загрузки, чтобы загрузить снимок экрана виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="8c02f-123">You can also click **Screenshot** across the top of the boot diagnostics log to download a capture of the VM screenshot.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="8c02f-124">Просмотр сведений для существующего виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="8c02f-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="8c02f-125">Прежде чем присоединить виртуальный жесткий диск к другой виртуальной машине, следует определить имя этого виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="8c02f-125">Before you can attach your virtual hard disk to another VM, you need to identify the name of the virtual hard disk (VHD).</span></span> 

<span data-ttu-id="8c02f-126">Выберите на портале группу ресурсов и учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="8c02f-126">Select your resource group from the portal, then select your storage account.</span></span> <span data-ttu-id="8c02f-127">Щелкните **Большие двоичные объекты**, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="8c02f-127">Click **Blobs**, as in the following example:</span></span>

![Выбор больших двоичных объектов для хранения](./media/troubleshoot-recovery-disks-portal/storage-account-overview.png)

<span data-ttu-id="8c02f-129">Обычно виртуальные жесткие диски хранятся в отдельном контейнере с именем **vhds**.</span><span class="sxs-lookup"><span data-stu-id="8c02f-129">Typically you have a container named **vhds** that stores your virtual hard disks.</span></span> <span data-ttu-id="8c02f-130">Выберите этот контейнер, чтобы просмотреть список виртуальных жестких дисков.</span><span class="sxs-lookup"><span data-stu-id="8c02f-130">Select the container to view a list of virtual hard disks.</span></span> <span data-ttu-id="8c02f-131">Запишите имя нужного виртуального жесткого диска (обычно используется префикс, совпадающий с именем виртуальной машины).</span><span class="sxs-lookup"><span data-stu-id="8c02f-131">Note the name of your VHD (the prefix is usually the name of your VM):</span></span>

![Поиск виртуального жесткого диска в контейнере хранилища](./media/troubleshoot-recovery-disks-portal/storage-container.png)

<span data-ttu-id="8c02f-133">Выберите из списка существующий виртуальный жесткий диск и скопируйте его URL-адрес для использования на следующих этапах.</span><span class="sxs-lookup"><span data-stu-id="8c02f-133">Select your existing virtual hard disk from the list and copy the URL for use in the following steps:</span></span>

![Копирование URL-адреса существующего виртуального жесткого диска](./media/troubleshoot-recovery-disks-portal/copy-vhd-url.png)


## <a name="delete-existing-vm"></a><span data-ttu-id="8c02f-135">Удаление существующей виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="8c02f-135">Delete existing VM</span></span>
<span data-ttu-id="8c02f-136">Виртуальные жесткие диски и виртуальные машины — это разные ресурсы в Azure.</span><span class="sxs-lookup"><span data-stu-id="8c02f-136">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="8c02f-137">Виртуальный жесткий диск является местом хранения операционной системы, приложений и конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8c02f-137">A virtual hard disk is where the operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="8c02f-138">Виртуальная машина — это просто метаданные, которые определяют размер или расположение объекта, а также ссылки на ресурсы, такие как виртуальные жесткие диски или виртуальные сетевые адаптеры.</span><span class="sxs-lookup"><span data-stu-id="8c02f-138">The VM itself is just metadata that defines the size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="8c02f-139">При присоединении виртуального жесткого диска к виртуальной машине для него регистрируется аренда.</span><span class="sxs-lookup"><span data-stu-id="8c02f-139">Each virtual hard disk has a lease assigned when attached to a VM.</span></span> <span data-ttu-id="8c02f-140">Диски данных можно присоединять и отсоединять во время работы виртуальной машины, но диск операционной системы отсоединить невозможно, пока ресурс виртуальной машины не будет удален.</span><span class="sxs-lookup"><span data-stu-id="8c02f-140">Although data disks can be attached and detached even while the VM is running, the OS disk cannot be detached unless the VM resource is deleted.</span></span> <span data-ttu-id="8c02f-141">Аренда сохраняет привязку диска операционной системы к виртуальной машине, даже когда эта виртуальная машина остановлена или отменено ее распределение.</span><span class="sxs-lookup"><span data-stu-id="8c02f-141">The lease continues to associate the OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="8c02f-142">Поэтому для восстановления виртуальной машины нужно прежде всего удалить ресурс виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="8c02f-142">The first step to recover your VM is to delete the VM resource itself.</span></span> <span data-ttu-id="8c02f-143">Удаление виртуальной машины не повлияет на виртуальные жесткие диски, размещенные в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="8c02f-143">Deleting the VM leaves the virtual hard disks in your storage account.</span></span> <span data-ttu-id="8c02f-144">После удаления виртуальной машины присоедините виртуальный жесткий диск к другой виртуальной машине, чтобы устранить неполадки.</span><span class="sxs-lookup"><span data-stu-id="8c02f-144">After the VM is deleted, you attach the virtual hard disk to another VM to troubleshoot and resolve the errors.</span></span>

<span data-ttu-id="8c02f-145">Выберите на портале нужную виртуальную машину и щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="8c02f-145">Select your VM in the portal, then click **Delete**:</span></span>

![Снимок экрана диагностики загрузки виртуальной машины с сообщением об ошибке загрузки](./media/troubleshoot-recovery-disks-portal/stop-delete-vm.png)

<span data-ttu-id="8c02f-147">Дождитесь, пока удаление завершится, прежде чем присоединять виртуальный жесткий диск к другой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="8c02f-147">Wait until the VM has finished deleting before you attach the virtual hard disk to another VM.</span></span> <span data-ttu-id="8c02f-148">Чтобы присоединить виртуальный жесткий диск к другой виртуальной машине, необходимо снять аренду, которая привязывает диск к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="8c02f-148">The lease on the virtual hard disk that associates it with the VM needs to be released before you can attach the virtual hard disk to another VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-to-another-vm"></a><span data-ttu-id="8c02f-149">Присоединение существующего виртуального жесткого диска к другой виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="8c02f-149">Attach existing virtual hard disk to another VM</span></span>
<span data-ttu-id="8c02f-150">В следующих нескольких шагах описывается использование другой виртуальной машины для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="8c02f-150">For the next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="8c02f-151">Присоедините существующий виртуальный жесткий диск к виртуальной машине для устранения неполадок, чтобы можно было просматривать и изменять содержимое диска.</span><span class="sxs-lookup"><span data-stu-id="8c02f-151">You attach the existing virtual hard disk to this troubleshooting VM to be able to browse and edit the disk's content.</span></span> <span data-ttu-id="8c02f-152">Этот процесс позволяет, например, исправить ошибки конфигурации или изучить дополнительные журналы протоколов или системы.</span><span class="sxs-lookup"><span data-stu-id="8c02f-152">This process allows you to correct any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="8c02f-153">Выберите или создайте другую виртуальную машину, которая будет использоваться для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="8c02f-153">Choose or create another VM to use for troubleshooting purposes.</span></span>

1. <span data-ttu-id="8c02f-154">Выберите на портале группу ресурсов и виртуальную машину для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="8c02f-154">Select your resource group from the portal, then select your troubleshooting VM.</span></span> <span data-ttu-id="8c02f-155">Выберите **Диски** и нажмите кнопку **Подключить существующий**.</span><span class="sxs-lookup"><span data-stu-id="8c02f-155">Select **Disks** and then click **Attach existing**:</span></span>

    ![Присоединение существующего диска на портале](./media/troubleshoot-recovery-disks-portal/attach-existing-disk.png)

2. <span data-ttu-id="8c02f-157">Чтобы выбрать существующий виртуальный жесткий диск, щелкните его **VHD-файл**.</span><span class="sxs-lookup"><span data-stu-id="8c02f-157">To select your existing virtual hard disk, click **VHD File**:</span></span>

    ![Поиск существующего виртуального жесткого диска](./media/troubleshoot-recovery-disks-portal/select-vhd-location.png)

3. <span data-ttu-id="8c02f-159">Выберите учетную запись хранения и контейнер, затем щелкните существующий виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="8c02f-159">Select your storage account and container, then click your existing VHD.</span></span> <span data-ttu-id="8c02f-160">Нажмите кнопку **Выбрать**, чтобы подтвердить выбор.</span><span class="sxs-lookup"><span data-stu-id="8c02f-160">Click the **Select** button to confirm your choice:</span></span>

    ![Выбор существующего виртуального жесткого диска](./media/troubleshoot-recovery-disks-portal/select-vhd.png)

4. <span data-ttu-id="8c02f-162">Выбрав существующий виртуальный жесткий диск, щелкните **ОК**, чтобы присоединить его.</span><span class="sxs-lookup"><span data-stu-id="8c02f-162">With your VHD now selected, click **OK** to attach the existing virtual hard disk:</span></span>

    ![Подтверждение присоединения существующего виртуального жесткого диска](./media/troubleshoot-recovery-disks-portal/attach-disk-confirm.png)

5. <span data-ttu-id="8c02f-164">Через несколько секунд на панели **Диски** для виртуальной машины отобразится подключение существующего виртуального жесткого диска в качестве диска данных.</span><span class="sxs-lookup"><span data-stu-id="8c02f-164">After a few seconds, the **Disks** pane for your VM lists your existing virtual hard disk connected as a data disk:</span></span>

    ![Существующий виртуальный жесткий диск присоединен как диск данных](./media/troubleshoot-recovery-disks-portal/attached-disk.png)


## <a name="mount-the-attached-data-disk"></a><span data-ttu-id="8c02f-166">Подключение присоединенного диска данных</span><span class="sxs-lookup"><span data-stu-id="8c02f-166">Mount the attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="8c02f-167">В следующих примерах описана процедура для виртуальной машины Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="8c02f-167">The following examples detail the steps required on an Ubuntu VM.</span></span> <span data-ttu-id="8c02f-168">Если вы используете другой дистрибутив Linux, например Red Hat Enterprise Linux или SUSE, команды `mount` и расположение файлов журнала могут немного отличаться.</span><span class="sxs-lookup"><span data-stu-id="8c02f-168">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, the log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="8c02f-169">Используйте документацию к своему дистрибутиву, чтобы скорректировать команды соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="8c02f-169">Refer to the documentation for your specific distro for the appropriate changes in commands.</span></span>

1. <span data-ttu-id="8c02f-170">Подключитесь к виртуальной машине для устранения неполадок по протоколу SSH, используя соответствующие учетные данные.</span><span class="sxs-lookup"><span data-stu-id="8c02f-170">SSH to your troubleshooting VM using the appropriate credentials.</span></span> <span data-ttu-id="8c02f-171">Если присоединенный вами диск является первым диском данных на этой виртуальной машине, он скорее всего подключен к `/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="8c02f-171">If this disk is the first data disk attached to your troubleshooting VM, it is likely connected to `/dev/sdc`.</span></span> <span data-ttu-id="8c02f-172">Запустите команду `dmseg`, чтобы получить список присоединенных дисков.</span><span class="sxs-lookup"><span data-stu-id="8c02f-172">Use `dmseg` to list attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```
    <span data-ttu-id="8c02f-173">Вы должны увидеть результат, аналогичный приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="8c02f-173">The output is similar to the following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="8c02f-174">В предыдущем примере диск операционной системы расположен в `/dev/sda`, а временный диск, предоставляемый для каждой виртуальной машины, расположен в `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="8c02f-174">In the preceding example, the OS disk is at `/dev/sda` and the temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="8c02f-175">Если у вас несколько дисков данных, они будут присоединены как `/dev/sdd`, `/dev/sde` и т. д.</span><span class="sxs-lookup"><span data-stu-id="8c02f-175">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="8c02f-176">Создайте каталог для подключения существующего виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="8c02f-176">Create a directory to mount your existing virtual hard disk.</span></span> <span data-ttu-id="8c02f-177">Следующая команда создает каталог с именем `troubleshootingdisk`.</span><span class="sxs-lookup"><span data-stu-id="8c02f-177">The following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="8c02f-178">Если на существующем виртуальном жестком диске есть несколько разделов, подключите нужный.</span><span class="sxs-lookup"><span data-stu-id="8c02f-178">If you have multiple partitions on your existing virtual hard disk, mount the required partition.</span></span> <span data-ttu-id="8c02f-179">Следующая команда подключает первый основной разделу к каталогу `/dev/sdc1`.</span><span class="sxs-lookup"><span data-stu-id="8c02f-179">The following example mounts the first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="8c02f-180">Мы рекомендуем подключать диски данных к виртуальным машинам Azure с использованием глобального уникального идентификатора (UUID) виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="8c02f-180">Best practice is to mount data disks on VMs in Azure using the universally unique identifier (UUID) of the virtual hard disk.</span></span> <span data-ttu-id="8c02f-181">Для нашего упрощенного примера по устранению неполадок можно и не использовать UUID для подключения диска.</span><span class="sxs-lookup"><span data-stu-id="8c02f-181">For this short troubleshooting scenario, mounting the virtual hard disk using the UUID is not necessary.</span></span> <span data-ttu-id="8c02f-182">Но в обычной ситуации, если вы измените `/etc/fstab` так, чтобы виртуальные жесткие диски подключались по имени устройства вместо UUID, у виртуальной машины могут быть проблемы с загрузкой.</span><span class="sxs-lookup"><span data-stu-id="8c02f-182">However, under normal use, editing `/etc/fstab` to mount virtual hard disks using device name rather than UUID may cause the VM to fail to boot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="8c02f-183">Устранение неполадок на исходном виртуальном жестком диске</span><span class="sxs-lookup"><span data-stu-id="8c02f-183">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="8c02f-184">Теперь, когда существующий виртуальный жесткий диск подключен, вы можете выполнить любые необходимые действия по обслуживанию и (или) устранению неполадок.</span><span class="sxs-lookup"><span data-stu-id="8c02f-184">With the existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="8c02f-185">После устранения проблем выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="8c02f-185">Once you have addressed the issues, continue with the following steps.</span></span>

## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="8c02f-186">Отключение и отсоединение исходного виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="8c02f-186">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="8c02f-187">После устранения ошибок отсоедините существующий виртуальный жесткий диск от виртуальной машины, которую использовали для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="8c02f-187">Once your errors are resolved, detach the existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="8c02f-188">Виртуальный жесткий диск нельзя использовать с другой виртуальной машиной, пока вы не отмените аренду, присоединяющую виртуальный жесткий диск к виртуальной машине для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="8c02f-188">You cannot use your virtual hard disk with any other VM until the lease attaching the virtual hard disk to the troubleshooting VM is released.</span></span>

1. <span data-ttu-id="8c02f-189">Используя открытый сеанс подключения по SSH к виртуальной машине для устранения неполадок, отключите существующий виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="8c02f-189">From the SSH session to your troubleshooting VM, unmount the existing virtual hard disk.</span></span> <span data-ttu-id="8c02f-190">Прежде всего выйдите из каталога, в котором создана точка подключения.</span><span class="sxs-lookup"><span data-stu-id="8c02f-190">Change out of the parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="8c02f-191">Теперь отключите существующий виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="8c02f-191">Now unmount the existing virtual hard disk.</span></span> <span data-ttu-id="8c02f-192">В следующем примере диск отключается от каталога `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="8c02f-192">The following example unmounts the device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="8c02f-193">Теперь отсоедините виртуальный жесткий диск от виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="8c02f-193">Now detach the virtual hard disk from the VM.</span></span> <span data-ttu-id="8c02f-194">Выберите на портале нужную виртуальную машину и щелкните **Диски**.</span><span class="sxs-lookup"><span data-stu-id="8c02f-194">Select your VM in the portal and click **Disks**.</span></span> <span data-ttu-id="8c02f-195">Выберите существующий виртуальный жесткий диск и щелкните **Отсоединить**.</span><span class="sxs-lookup"><span data-stu-id="8c02f-195">Select your existing virtual hard disk and then click **Detach**:</span></span>

    ![Отсоединение существующего виртуального жесткого диска](./media/troubleshoot-recovery-disks-portal/detach-disk.png)

    <span data-ttu-id="8c02f-197">Подождите, пока виртуальная машина успешно отсоединит диск данных, прежде чем продолжать процесс.</span><span class="sxs-lookup"><span data-stu-id="8c02f-197">Wait until the VM has successfully detached the data disk before continuing.</span></span>

## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="8c02f-198">Создание виртуальной машины из исходного жесткого диска</span><span class="sxs-lookup"><span data-stu-id="8c02f-198">Create VM from original hard disk</span></span>
<span data-ttu-id="8c02f-199">Чтобы создать виртуальную машину из исходного виртуального жесткого диска, используйте [этот шаблон Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="8c02f-199">To create a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="8c02f-200">Этот шаблон развертывает виртуальную машину в существующую виртуальную сеть, используя URL-адрес виртуального жесткого диска из использованной выше команды.</span><span class="sxs-lookup"><span data-stu-id="8c02f-200">The template deploys a VM into an existing virtual network, using the VHD URL from the earlier command.</span></span> <span data-ttu-id="8c02f-201">Нажмите кнопку **Развернуть в Azure**.</span><span class="sxs-lookup"><span data-stu-id="8c02f-201">Click the **Deploy to Azure** button as follows:</span></span>

![Развертывание виртуальной машины из шаблона GitHub](./media/troubleshoot-recovery-disks-portal/deploy-template-from-github.png)

<span data-ttu-id="8c02f-203">Шаблон загружается на портал Azure для развертывания.</span><span class="sxs-lookup"><span data-stu-id="8c02f-203">The template is loaded into the Azure portal for deployment.</span></span> <span data-ttu-id="8c02f-204">Введите имя для новой виртуальной машины и укажите существующие ресурсы Azure, а затем вставьте URL-адрес исходного виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="8c02f-204">Enter the names for your new VM and existing Azure resources, and paste the URL to your existing virtual hard disk.</span></span> <span data-ttu-id="8c02f-205">Чтобы начать развертывание, щелкните **Приобрести**.</span><span class="sxs-lookup"><span data-stu-id="8c02f-205">To begin the deployment, click **Purchase**:</span></span>

![Развертывание виртуальной машины на основе шаблона](./media/troubleshoot-recovery-disks-portal/deploy-from-image.png)


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="8c02f-207">Восстановление диагностики загрузки</span><span class="sxs-lookup"><span data-stu-id="8c02f-207">Re-enable boot diagnostics</span></span>
<span data-ttu-id="8c02f-208">При создании виртуальной машины на основе существующего виртуального жесткого диска диагностика загрузки не всегда автоматически включена.</span><span class="sxs-lookup"><span data-stu-id="8c02f-208">When you create your VM from the existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="8c02f-209">Выберите эту виртуальную машину на портале, чтобы проверить состояние диагностики загрузки и включить ее, если потребуется.</span><span class="sxs-lookup"><span data-stu-id="8c02f-209">To check the status of boot diagnostics and turn on if needed, select your VM in the portal.</span></span> <span data-ttu-id="8c02f-210">В разделе **Мониторинг** щелкните **Параметры диагностики**.</span><span class="sxs-lookup"><span data-stu-id="8c02f-210">Under **Monitoring**, click **Diagnostics settings**.</span></span> <span data-ttu-id="8c02f-211">Убедитесь, что выбрано состояние **Включено** и установлен флажок **Диагностика загрузки**.</span><span class="sxs-lookup"><span data-stu-id="8c02f-211">Ensure the status is **On**, and the check mark next to **Boot diagnostics** is selected.</span></span> <span data-ttu-id="8c02f-212">Если вы внесете здесь изменения, нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="8c02f-212">If you make any changes, click **Save**:</span></span>

![Обновление параметров диагностики загрузки](./media/troubleshoot-recovery-disks-portal/reenable-boot-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="8c02f-214">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8c02f-214">Next steps</span></span>
<span data-ttu-id="8c02f-215">При возникновении проблем с подключением к виртуальной машине см. статью [Устранение неполадок с SSH-подключением к виртуальной машине Azure Linux: сбой, ошибка или отклонение](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8c02f-215">If you are having issues connecting to your VM, see [Troubleshoot SSH connections to an Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="8c02f-216">Для решения проблем с доступом к приложениям, выполняющимся на виртуальной машине, см. статью [Устранение проблем с подключением к приложениям на виртуальных машинах Linux в Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8c02f-216">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="8c02f-217">Дополнительные сведения об использовании Resource Manager вы найдете в статье [Общие сведения об Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8c02f-217">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
