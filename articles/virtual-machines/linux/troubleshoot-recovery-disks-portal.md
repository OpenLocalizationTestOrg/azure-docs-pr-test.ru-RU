---
title: "aaaUse a Linux, устранение неполадок виртуальной Машины в hello портал Azure | Документы Microsoft"
description: "Узнайте, как tootroubleshoot проблемы виртуальных машин Linux по связи hello ОС диска tooa восстановления виртуальной Машины с помощью hello портал Azure"
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
ms.openlocfilehash: 794daa06d7436215af84a61ab9088524254c47df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-portal"></a><span data-ttu-id="ad3f7-103">Устранение неполадок виртуальной Машины Linux путем присоединения восстановление tooa диска hello ОС виртуальной Машины с помощью hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="ad3f7-103">Troubleshoot a Linux VM by attaching hello OS disk tooa recovery VM using hello Azure portal</span></span>
<span data-ttu-id="ad3f7-104">Если Linux виртуальной машины (VM), возникает ошибка загрузки или диск, может потребоваться tooperform действия на виртуальном жестком диске hello сам по устранению неполадок.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="ad3f7-105">Распространенным примером будет недопустимую запись в `/etc/fstab` , предотвращает hello виртуальной Машины может tooboot успешно.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-105">A common example would be an invalid entry in `/etc/fstab` that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="ad3f7-106">Этой статьи описаны как toouse hello Azure портала tooconnect вашего виртуального жесткого диска tooanother toofix ВМ Linux все ошибки, а затем повторного создания исходной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-106">This article details how toouse hello Azure portal tooconnect your virtual hard disk tooanother Linux VM toofix any errors, then re-create your original VM.</span></span>

## <a name="recovery-process-overview"></a><span data-ttu-id="ad3f7-107">Обзор процесса восстановления</span><span class="sxs-lookup"><span data-stu-id="ad3f7-107">Recovery process overview</span></span>
<span data-ttu-id="ad3f7-108">Поиск и устранение неполадок Hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ad3f7-108">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="ad3f7-109">Удалите hello ВМ возникновения проблемы, поддержание hello виртуальных жестких дисков.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-109">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="ad3f7-110">Присоедините и подключите tooanother hello виртуальный жесткий диск виртуальной Машины с Linux для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-110">Attach and mount hello virtual hard disk tooanother Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="ad3f7-111">Подключите toohello Устранение неполадок виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-111">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="ad3f7-112">Изменение файлов или выполните любые средства toofix проблемы на hello исходный виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-112">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="ad3f7-113">Отключите образ и отсоединить виртуальный жесткий диск hello из hello, устранение неполадок виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-113">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="ad3f7-114">Создайте виртуальную Машину с помощью hello исходный виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-114">Create a VM using hello original virtual hard disk.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="ad3f7-115">Выявление проблем при загрузке</span><span class="sxs-lookup"><span data-stu-id="ad3f7-115">Determine boot issues</span></span>
<span data-ttu-id="ad3f7-116">Изучите Диагностика загрузки hello и почему ВМ не могут tooboot правильно toodetermine экрана виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-116">Examine hello boot diagnostics and VM screenshot toodetermine why your VM is not able tooboot correctly.</span></span> <span data-ttu-id="ad3f7-117">Например, причиной может быть неправильная запись в `/etc/fstab`, удаление или перемещение базового виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-117">A common example would be an invalid entry in `/etc/fstab`, or an underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="ad3f7-118">Выбрать ВМ на портале hello и прокрутите вниз toohello **поддержки + Устранение неполадок** раздела.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-118">Select your VM in hello portal and then scroll down toohello **Support + Troubleshooting** section.</span></span> <span data-ttu-id="ad3f7-119">Нажмите кнопку **загрузки диагностики** сообщения консоли hello tooview потоковой передачи из виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-119">Click **Boot diagnostics** tooview hello console messages streamed from your VM.</span></span> <span data-ttu-id="ad3f7-120">Журналы событий консоли hello проверки toosee Если можно определить, почему hello ВМ возникают проблемы.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-120">Review hello console logs toosee if you can determine why hello VM is encountering an issue.</span></span> <span data-ttu-id="ad3f7-121">Hello следующем примере показано, что виртуальная машина находится в режиме обслуживания, которое должно выполняться вручную.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-121">hello following example shows a VM stuck in maintenance mode that requires manual interaction:</span></span>

![Просмотр журналов консоли для диагностики загрузки виртуальной машины](./media/troubleshoot-recovery-disks-portal/boot-diagnostics-error.png)

<span data-ttu-id="ad3f7-123">Можно также щелкнуть **экрана** сверху hello hello загрузки диагностики журнала toodownload захвата снимка экрана приветствия виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-123">You can also click **Screenshot** across hello top of hello boot diagnostics log toodownload a capture of hello VM screenshot.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="ad3f7-124">Просмотр сведений для существующего виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="ad3f7-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="ad3f7-125">Перед тем как присоединить tooanother вашего виртуального жесткого диска виртуальной Машины, необходимо имя hello tooidentify hello виртуального жесткого диска (VHD).</span><span class="sxs-lookup"><span data-stu-id="ad3f7-125">Before you can attach your virtual hard disk tooanother VM, you need tooidentify hello name of hello virtual hard disk (VHD).</span></span> 

<span data-ttu-id="ad3f7-126">Выберите группу ресурсов с портала hello, а затем выберите учетную запись хранилища.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-126">Select your resource group from hello portal, then select your storage account.</span></span> <span data-ttu-id="ad3f7-127">Нажмите кнопку **большие двоичные объекты**, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="ad3f7-127">Click **Blobs**, as in hello following example:</span></span>

![Выбор больших двоичных объектов для хранения](./media/troubleshoot-recovery-disks-portal/storage-account-overview.png)

<span data-ttu-id="ad3f7-129">Обычно виртуальные жесткие диски хранятся в отдельном контейнере с именем **vhds**.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-129">Typically you have a container named **vhds** that stores your virtual hard disks.</span></span> <span data-ttu-id="ad3f7-130">Выберите контейнер hello tooview список виртуальных жестких дисков.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-130">Select hello container tooview a list of virtual hard disks.</span></span> <span data-ttu-id="ad3f7-131">Примечание hello имя вашего виртуального жесткого диска (префикс hello обычно — имя hello ВМ):</span><span class="sxs-lookup"><span data-stu-id="ad3f7-131">Note hello name of your VHD (hello prefix is usually hello name of your VM):</span></span>

![Поиск виртуального жесткого диска в контейнере хранилища](./media/troubleshoot-recovery-disks-portal/storage-container.png)

<span data-ttu-id="ad3f7-133">Выберите существующий виртуальный жесткий диск из списка hello и скопируйте hello URL-адрес для использования в hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="ad3f7-133">Select your existing virtual hard disk from hello list and copy hello URL for use in hello following steps:</span></span>

![Копирование URL-адреса существующего виртуального жесткого диска](./media/troubleshoot-recovery-disks-portal/copy-vhd-url.png)


## <a name="delete-existing-vm"></a><span data-ttu-id="ad3f7-135">Удаление существующей виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="ad3f7-135">Delete existing VM</span></span>
<span data-ttu-id="ad3f7-136">Виртуальные жесткие диски и виртуальные машины — это разные ресурсы в Azure.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-136">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="ad3f7-137">Виртуальный жесткий диск является местом hello операционной системы, приложения и конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-137">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="ad3f7-138">Hello самой ВМ — точно так же метаданные, которые определяет hello размер или расположение и ссылки на ресурсы, такие как виртуальный жесткий диск или виртуальный сетевой адаптер (NIC).</span><span class="sxs-lookup"><span data-stu-id="ad3f7-138">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="ad3f7-139">Каждый виртуальный жесткий диск содержит аренды, назначенный при присоединении tooa виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-139">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="ad3f7-140">Несмотря на то, что диски с данными может быть присоединенные и отсоединенные даже в том случае, когда выполняется hello виртуальной Машины, диска ОС hello отключить невозможно, пока удаляется hello ресурса виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-140">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="ad3f7-141">Аренда Hello продолжается tooassociate hello ОС диска с виртуальной Машиной даже в том случае, если этой виртуальной Машины находится в состоянии остановки и освобождается.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-141">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="ad3f7-142">Здравствуйте, первый шаг toorecover ВМ — toodelete hello ВМ сам ресурс.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-142">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="ad3f7-143">Удаление hello ВМ оставляет hello виртуальных жестких дисков в вашей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-143">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="ad3f7-144">После hello удаления виртуальной Машины присоединения hello виртуальный жесткий диск tooanother ВМ tootroubleshoot и устранение ошибок hello.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-144">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="ad3f7-145">Выберите виртуальную Машину на портале hello, щелкните **удалить**:</span><span class="sxs-lookup"><span data-stu-id="ad3f7-145">Select your VM in hello portal, then click **Delete**:</span></span>

![Снимок экрана диагностики загрузки виртуальной машины с сообщением об ошибке загрузки](./media/troubleshoot-recovery-disks-portal/stop-delete-vm.png)

<span data-ttu-id="ad3f7-147">Подождите, пока hello ВМ закончит удаление перед присоединением tooanother hello виртуальный жесткий диск виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-147">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="ad3f7-148">Аренда Hello hello виртуальный жесткий диск, который связывает его с hello виртуальной Машины должен toobe выпуска перед тем как присоединить tooanother hello виртуальный жесткий диск виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-148">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="ad3f7-149">Подключить существующий виртуальный жесткий диск tooanother виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="ad3f7-149">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="ad3f7-150">Для Здравствуйте рядом шагах, для устранения неполадок используется другой виртуальной Машиной.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-150">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="ad3f7-151">Подключить существующий виртуальный жесткий диск toothis hello Устранение неполадок может toobrowse toobe ВМ и изменить содержимое диска hello.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-151">You attach hello existing virtual hard disk toothis troubleshooting VM toobe able toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="ad3f7-152">Этот процесс позволяет toocorrect все ошибки конфигурации или Просмотр дополнительных приложений или файлы журналов, например системы.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-152">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="ad3f7-153">Выберите или создайте другой toouse виртуальной Машины для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-153">Choose or create another VM toouse for troubleshooting purposes.</span></span>

1. <span data-ttu-id="ad3f7-154">Выберите группу ресурсов с портала hello, а затем выберите виртуальную Машину по устранению неполадок.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-154">Select your resource group from hello portal, then select your troubleshooting VM.</span></span> <span data-ttu-id="ad3f7-155">Выберите **Диски** и нажмите кнопку **Подключить существующий**.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-155">Select **Disks** and then click **Attach existing**:</span></span>

    ![Подключить существующий диск в портале hello](./media/troubleshoot-recovery-disks-portal/attach-existing-disk.png)

2. <span data-ttu-id="ad3f7-157">tooselect существующего виртуального жесткого диска, нажмите кнопку **VHD-файл**:</span><span class="sxs-lookup"><span data-stu-id="ad3f7-157">tooselect your existing virtual hard disk, click **VHD File**:</span></span>

    ![Поиск существующего виртуального жесткого диска](./media/troubleshoot-recovery-disks-portal/select-vhd-location.png)

3. <span data-ttu-id="ad3f7-159">Выберите учетную запись хранения и контейнер, затем щелкните существующий виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-159">Select your storage account and container, then click your existing VHD.</span></span> <span data-ttu-id="ad3f7-160">Нажмите кнопку hello **выберите** кнопку tooconfirm Выбор:</span><span class="sxs-lookup"><span data-stu-id="ad3f7-160">Click hello **Select** button tooconfirm your choice:</span></span>

    ![Выбор существующего виртуального жесткого диска](./media/troubleshoot-recovery-disks-portal/select-vhd.png)

4. <span data-ttu-id="ad3f7-162">С вашей VHD выбранное сейчас, нажмите кнопку **ОК** tooattach hello существующего виртуального жесткого диска:</span><span class="sxs-lookup"><span data-stu-id="ad3f7-162">With your VHD now selected, click **OK** tooattach hello existing virtual hard disk:</span></span>

    ![Подтверждение присоединения существующего виртуального жесткого диска](./media/troubleshoot-recovery-disks-portal/attach-disk-confirm.png)

5. <span data-ttu-id="ad3f7-164">Через несколько секунд hello **дисков** ваш существующий виртуальный жесткий диск, подключенный как диск данных перечислены области для вашей виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="ad3f7-164">After a few seconds, hello **Disks** pane for your VM lists your existing virtual hard disk connected as a data disk:</span></span>

    ![Существующий виртуальный жесткий диск присоединен как диск данных](./media/troubleshoot-recovery-disks-portal/attached-disk.png)


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="ad3f7-166">Подключить hello подключенный диск данных</span><span class="sxs-lookup"><span data-stu-id="ad3f7-166">Mount hello attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="ad3f7-167">Hello следующих примерах приведены шаги на Виртуальной машине Ubuntu hello.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-167">hello following examples detail hello steps required on an Ubuntu VM.</span></span> <span data-ttu-id="ad3f7-168">Если вы используете другой дистрибутив Linux, например Red Hat Enterprise Linux или SUSE, hello расположения файлов журнала и `mount` команд может немного отличаться.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-168">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, hello log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="ad3f7-169">См. в документации toohello для вашего конкретного дистрибутив для hello соответствующие изменения в командах.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-169">Refer toohello documentation for your specific distro for hello appropriate changes in commands.</span></span>

1. <span data-ttu-id="ad3f7-170">Устранение неполадок виртуальной Машины, используя соответствующие учетные данные hello tooyour SSH.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-170">SSH tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="ad3f7-171">Если этот диск является tooyour данных диске, подключенном hello для первого Устранение неполадок виртуальной Машины, оно скорее всего подключено слишком`/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-171">If this disk is hello first data disk attached tooyour troubleshooting VM, it is likely connected too`/dev/sdc`.</span></span> <span data-ttu-id="ad3f7-172">Используйте `dmseg` toolist присоединенных дисков:</span><span class="sxs-lookup"><span data-stu-id="ad3f7-172">Use `dmseg` toolist attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```
    <span data-ttu-id="ad3f7-173">Hello вывода будет примерно toohello следующий пример:</span><span class="sxs-lookup"><span data-stu-id="ad3f7-173">hello output is similar toohello following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="ad3f7-174">В предыдущих пример hello, диск hello ОС находится на `/dev/sda` и hello временного диска, указанное для каждой виртуальной Машины в `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-174">In hello preceding example, hello OS disk is at `/dev/sda` and hello temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="ad3f7-175">Если у вас несколько дисков данных, они будут присоединены как `/dev/sdd`, `/dev/sde` и т. д.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-175">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="ad3f7-176">Создайте directory toomount существующий виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-176">Create a directory toomount your existing virtual hard disk.</span></span> <span data-ttu-id="ad3f7-177">Hello следующий пример создает каталог с именем `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="ad3f7-177">hello following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="ad3f7-178">При наличии нескольких секций на существующий виртуальный жесткий диск, подключите hello необходимые секции.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-178">If you have multiple partitions on your existing virtual hard disk, mount hello required partition.</span></span> <span data-ttu-id="ad3f7-179">Hello следующий пример подключает первому основному разделу hello в `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="ad3f7-179">hello following example mounts hello first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="ad3f7-180">Лучший способ — что toomount диски с данными на виртуальных машинах в Azure с помощью hello универсальный уникальный идентификатор UUID hello виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-180">Best practice is toomount data disks on VMs in Azure using hello universally unique identifier (UUID) of hello virtual hard disk.</span></span> <span data-ttu-id="ad3f7-181">В этом сценарии короткий по устранению неполадок монтажного hello виртуального жесткого диска с помощью hello UUID не требуется.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-181">For this short troubleshooting scenario, mounting hello virtual hard disk using hello UUID is not necessary.</span></span> <span data-ttu-id="ad3f7-182">Тем не менее, при обычных условиях использования редактирования `/etc/fstab` toomount виртуальных жестких дисков с помощью имени, а не может вызвать UUID hello tooboot toofail виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-182">However, under normal use, editing `/etc/fstab` toomount virtual hard disks using device name rather than UUID may cause hello VM toofail tooboot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="ad3f7-183">Устранение неполадок на исходном виртуальном жестком диске</span><span class="sxs-lookup"><span data-stu-id="ad3f7-183">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="ad3f7-184">С hello существующий виртуальный жесткий диск подключен теперь можно выполнять обслуживание и действия по устранению неполадок при необходимости.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-184">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="ad3f7-185">После разрешения проблемы hello продолжите hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-185">Once you have addressed hello issues, continue with hello following steps.</span></span>

## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="ad3f7-186">Отключение и отсоединение исходного виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="ad3f7-186">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="ad3f7-187">После разрешения ошибки, отсоедините hello существующий виртуальный жесткий диск из виртуальной Машины по устранению неполадок.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-187">Once your errors are resolved, detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="ad3f7-188">Расположение виртуального жесткого диска нельзя использовать с любой другой ВМ до освобождения аренды hello присоединение toohello hello виртуального жесткого диска, устранение неполадок виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-188">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="ad3f7-189">Из сеанса SSH hello tooyour Устранение неполадок виртуальной Машины отключите hello существующий виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-189">From hello SSH session tooyour troubleshooting VM, unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="ad3f7-190">Сначала измените вне hello родительский каталог для точки подключения:</span><span class="sxs-lookup"><span data-stu-id="ad3f7-190">Change out of hello parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="ad3f7-191">Теперь отключите hello существующий виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-191">Now unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="ad3f7-192">Hello следующий пример отсоединяет диск hello устройство с `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="ad3f7-192">hello following example unmounts hello device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="ad3f7-193">Теперь отсоедините hello виртуальный жесткий диск из виртуальной Машины hello.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-193">Now detach hello virtual hard disk from hello VM.</span></span> <span data-ttu-id="ad3f7-194">Выберите виртуальную Машину на портале hello и нажмите кнопку **дисков**.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-194">Select your VM in hello portal and click **Disks**.</span></span> <span data-ttu-id="ad3f7-195">Выберите существующий виртуальный жесткий диск и щелкните **Отсоединить**.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-195">Select your existing virtual hard disk and then click **Detach**:</span></span>

    ![Отсоединение существующего виртуального жесткого диска](./media/troubleshoot-recovery-disks-portal/detach-disk.png)

    <span data-ttu-id="ad3f7-197">Подождите, пока hello виртуальной Машины успешно отсоединена hello диск данных перед продолжением.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-197">Wait until hello VM has successfully detached hello data disk before continuing.</span></span>

## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="ad3f7-198">Создание виртуальной машины из исходного жесткого диска</span><span class="sxs-lookup"><span data-stu-id="ad3f7-198">Create VM from original hard disk</span></span>
<span data-ttu-id="ad3f7-199">использовать ВМ с исходного виртуального жесткого диска, toocreate [этого шаблона Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="ad3f7-199">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="ad3f7-200">шаблон Hello развертывания ВМ в существующей виртуальной сети, с помощью hello URL-адрес VHD из hello ранее команд.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-200">hello template deploys a VM into an existing virtual network, using hello VHD URL from hello earlier command.</span></span> <span data-ttu-id="ad3f7-201">Нажмите кнопку hello **развертывание tooAzure** кнопку следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ad3f7-201">Click hello **Deploy tooAzure** button as follows:</span></span>

![Развертывание виртуальной машины из шаблона GitHub](./media/troubleshoot-recovery-disks-portal/deploy-template-from-github.png)

<span data-ttu-id="ad3f7-203">шаблон Hello загружается hello портала Azure для развертывания.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-203">hello template is loaded into hello Azure portal for deployment.</span></span> <span data-ttu-id="ad3f7-204">Введите имена hello для новой виртуальной Машины и существующие ресурсы Azure и вставьте hello URL-адрес tooyour существующий виртуальный жесткий диск.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-204">Enter hello names for your new VM and existing Azure resources, and paste hello URL tooyour existing virtual hard disk.</span></span> <span data-ttu-id="ad3f7-205">Развертывание toobegin hello, нажмите кнопку **покупки**:</span><span class="sxs-lookup"><span data-stu-id="ad3f7-205">toobegin hello deployment, click **Purchase**:</span></span>

![Развертывание виртуальной машины на основе шаблона](./media/troubleshoot-recovery-disks-portal/deploy-from-image.png)


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="ad3f7-207">Восстановление диагностики загрузки</span><span class="sxs-lookup"><span data-stu-id="ad3f7-207">Re-enable boot diagnostics</span></span>
<span data-ttu-id="ad3f7-208">При создании ВМ из hello существующий виртуальный жесткий диск, диагностика загрузки может не быть доступной.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-208">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="ad3f7-209">toocheck hello состояние Диагностика загрузки и включите при необходимости выбрать ВМ на портале hello.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-209">toocheck hello status of boot diagnostics and turn on if needed, select your VM in hello portal.</span></span> <span data-ttu-id="ad3f7-210">В разделе **Мониторинг** щелкните **Параметры диагностики**.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-210">Under **Monitoring**, click **Diagnostics settings**.</span></span> <span data-ttu-id="ad3f7-211">Убедитесь, находится в состоянии hello **на**, и hello флажок рядом слишком**загрузки диагностики** выбран.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-211">Ensure hello status is **On**, and hello check mark next too**Boot diagnostics** is selected.</span></span> <span data-ttu-id="ad3f7-212">Если вы внесете здесь изменения, нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ad3f7-212">If you make any changes, click **Save**:</span></span>

![Обновление параметров диагностики загрузки](./media/troubleshoot-recovery-disks-portal/reenable-boot-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="ad3f7-214">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ad3f7-214">Next steps</span></span>
<span data-ttu-id="ad3f7-215">Если возникают проблемы с подключением tooyour виртуальной Машины, см. раздел [Устранение SSH подключений tooan виртуальной Машины Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ad3f7-215">If you are having issues connecting tooyour VM, see [Troubleshoot SSH connections tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="ad3f7-216">Для решения проблем с доступом к приложениям, выполняющимся на виртуальной машине, см. статью [Устранение проблем с подключением к приложениям на виртуальных машинах Linux в Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ad3f7-216">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="ad3f7-217">Дополнительные сведения об использовании Resource Manager вы найдете в статье [Общие сведения об Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ad3f7-217">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
