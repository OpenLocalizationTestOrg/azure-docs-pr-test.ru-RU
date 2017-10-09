---
title: "aaaUse современных хранилища резервных копий с помощью Azure Backup Server v2 | Документы Microsoft"
description: "Дополнительные сведения о новых возможностях Azure Backup Server v2 hello. В этой статье описывается как tooupgrade установки сервер резервного копирования."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: masaran;markgal
ms.openlocfilehash: b2a1ed27a6a682bd611fea1d2df9ef93314404e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-storage-tooazure-backup-server-v2"></a><span data-ttu-id="83fdb-104">Добавление хранилища tooAzure v2 резервное копирование сервера</span><span class="sxs-lookup"><span data-stu-id="83fdb-104">Add storage tooAzure Backup Server v2</span></span>

<span data-ttu-id="83fdb-105">Azure Backup Server версии 2 поставляется с Modern Backup Storage System Center 2016 Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="83fdb-105">Azure Backup Server v2 comes with System Center 2016 Data Protection Manager Modern Backup Storage.</span></span> <span data-ttu-id="83fdb-106">Modern Backup Storage обеспечивает до 50 % экономии пространства хранения, архивацию, которая в три раза быстрее, и более эффективное хранилище.</span><span class="sxs-lookup"><span data-stu-id="83fdb-106">Modern Backup Storage offers storage savings of 50 percent, backups that are three times faster, and more efficient storage.</span></span> <span data-ttu-id="83fdb-107">Кроме того, предлагается хранение с учетом рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="83fdb-107">It also offers workload-aware storage.</span></span> 

> [!NOTE]
> <span data-ttu-id="83fdb-108">toouse современных хранения резервной копии, необходимо запустить v2 резервное копирование сервера в Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="83fdb-108">toouse Modern Backup Storage, you must run Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="83fdb-109">Если запустить Backup Server версии 2 на более ранней версии Windows Server, Azure Backup Server не сможет реализовать преимущества Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="83fdb-109">If you run Backup Server v2 on an earlier version of Windows Server, Azure Backup Server can't take advantage of Modern Backup Storage.</span></span> <span data-ttu-id="83fdb-110">Вместо этого он будет обеспечивать защиту рабочих нагрузок, как в случае с Backup Server версии 1.</span><span class="sxs-lookup"><span data-stu-id="83fdb-110">Instead, it protects workloads as it does with Backup Server v1.</span></span> <span data-ttu-id="83fdb-111">Дополнительные сведения см. в разделе hello резервное копирование сервера версии [защиты матрицы](backup-mabs-protection-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="83fdb-111">For more information, see hello Backup Server version [protection matrix](backup-mabs-protection-matrix.md).</span></span>

## <a name="volumes-in-backup-server-v2"></a><span data-ttu-id="83fdb-112">Тома в Backup Server версии 2</span><span class="sxs-lookup"><span data-stu-id="83fdb-112">Volumes in Backup Server v2</span></span>

<span data-ttu-id="83fdb-113">Backup Server версии 2 поддерживает тома хранилища.</span><span class="sxs-lookup"><span data-stu-id="83fdb-113">Backup Server v2 accepts storage volumes.</span></span> <span data-ttu-id="83fdb-114">При добавлении тома, резервное копирование форматирует том hello tooResilient файловая система (ReFS), требующий современных хранилища резервных копий.</span><span class="sxs-lookup"><span data-stu-id="83fdb-114">When you add a volume, Backup Server formats hello volume tooResilient File System (ReFS), which Modern Backup Storage requires.</span></span> <span data-ttu-id="83fdb-115">tooadd томом и tooexpand его позже, если вам нужно, мы рекомендуем использовать этот рабочий процесс:</span><span class="sxs-lookup"><span data-stu-id="83fdb-115">tooadd a volume, and tooexpand it later if you need to, we suggest that you use this workflow:</span></span>

1.  <span data-ttu-id="83fdb-116">Настройте Backup Server версии 2 на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="83fdb-116">Set up Backup Server v2 on a VM.</span></span>
2.  <span data-ttu-id="83fdb-117">Создайте том на виртуальном диске в пуле носителей:</span><span class="sxs-lookup"><span data-stu-id="83fdb-117">Create a volume on a virtual disk in a storage pool:</span></span>
    1.  <span data-ttu-id="83fdb-118">Добавление пула носителей tooa диск и создать виртуальный диск с простую структуру.</span><span class="sxs-lookup"><span data-stu-id="83fdb-118">Add a disk tooa storage pool and create a virtual disk with simple layout.</span></span>
    2.  <span data-ttu-id="83fdb-119">Добавьте дополнительные диски и расширить hello виртуального диска.</span><span class="sxs-lookup"><span data-stu-id="83fdb-119">Add any additional disks, and extend hello virtual disk.</span></span>
    3.  <span data-ttu-id="83fdb-120">Создание тома на виртуальном диске hello.</span><span class="sxs-lookup"><span data-stu-id="83fdb-120">Create volumes on hello virtual disk.</span></span>
3.  <span data-ttu-id="83fdb-121">Добавьте tooBackup hello томов сервера.</span><span class="sxs-lookup"><span data-stu-id="83fdb-121">Add hello volumes tooBackup Server.</span></span>
4.  <span data-ttu-id="83fdb-122">Настройте хранилище с учетом рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="83fdb-122">Configure workload-aware storage.</span></span>

## <a name="create-a-volume-for-modern-backup-storage"></a><span data-ttu-id="83fdb-123">Создание тома для Modern Backup Storage</span><span class="sxs-lookup"><span data-stu-id="83fdb-123">Create a volume for Modern Backup Storage</span></span>

<span data-ttu-id="83fdb-124">Использование Backup Server версии 2 в качестве дискового накопителя поможет полностью контролировать хранилище.</span><span class="sxs-lookup"><span data-stu-id="83fdb-124">Using Backup Server v2 with volumes as disk storage can help you maintain control over storage.</span></span> <span data-ttu-id="83fdb-125">Томом может быть один диск.</span><span class="sxs-lookup"><span data-stu-id="83fdb-125">A volume can be a single disk.</span></span> <span data-ttu-id="83fdb-126">Однако следует tooextend хранилища в hello будущих создайте том из дисков, созданных с помощью дисковых пространств.</span><span class="sxs-lookup"><span data-stu-id="83fdb-126">However, if you want tooextend storage in hello future, create a volume out of a disk created by using storage spaces.</span></span> <span data-ttu-id="83fdb-127">Это может помочь, если требуется tooexpand hello тома для хранения резервных копий.</span><span class="sxs-lookup"><span data-stu-id="83fdb-127">This can help if you want tooexpand hello volume for backup storage.</span></span> <span data-ttu-id="83fdb-128">В данном разделе приведены рекомендации по созданию тома с такой конфигурацией.</span><span class="sxs-lookup"><span data-stu-id="83fdb-128">This section offers best practices for creating a volume with this setup.</span></span>

1. <span data-ttu-id="83fdb-129">В диспетчере сервера выберите **Файловые службы и службы хранилища** > **Тома** > **Пулы носителей**.</span><span class="sxs-lookup"><span data-stu-id="83fdb-129">In Server Manager, select **File and Storage Services** > **Volumes** > **Storage Pools**.</span></span> <span data-ttu-id="83fdb-130">В разделе **ФИЗИЧЕСКИЕ ДИСКИ** выберите **Новый пул носителей**.</span><span class="sxs-lookup"><span data-stu-id="83fdb-130">Under **PHYSICAL DISKS**, select **New Storage Pool**.</span></span> 

    ![Создание учетной записи хранения](./media/backup-mabs-add-storage/mabs-add-storage-1.png)

2. <span data-ttu-id="83fdb-132">В hello **ЗАДАЧИ** раскрывающегося списка выберите **новый виртуальный диск**.</span><span class="sxs-lookup"><span data-stu-id="83fdb-132">In hello **TASKS** drop-down box, select **New Virtual Disk**.</span></span>

    ![Добавление виртуального диска](./media/backup-mabs-add-storage/mabs-add-storage-2.png)

3. <span data-ttu-id="83fdb-134">Выберите пул носителей hello, а затем выберите **Добавление физического диска**.</span><span class="sxs-lookup"><span data-stu-id="83fdb-134">Select hello storage pool, and then select **Add Physical Disk**.</span></span>

    ![Добавление физического диска](./media/backup-mabs-add-storage/mabs-add-storage-3.png)

4. <span data-ttu-id="83fdb-136">Выберите физический диск hello, а затем выберите **расширить виртуальный диск**.</span><span class="sxs-lookup"><span data-stu-id="83fdb-136">Select hello physical disk, and then select **Extend Virtual Disk**.</span></span>

    ![Расширение виртуального диска hello](./media/backup-mabs-add-storage/mabs-add-storage-4.png)

5. <span data-ttu-id="83fdb-138">Выберите виртуальный диск hello, а затем выберите **новый том**.</span><span class="sxs-lookup"><span data-stu-id="83fdb-138">Select hello virtual disk, and then select **New Volume**.</span></span>

    ![Создание нового тома](./media/backup-mabs-add-storage/mabs-add-storage-5.png)

6. <span data-ttu-id="83fdb-140">В hello **выберите hello сервер и диск** диалоговое окно, выберите hello server и hello новый диск.</span><span class="sxs-lookup"><span data-stu-id="83fdb-140">In hello **Select hello server and disk** dialog, select hello server and hello new disk.</span></span> <span data-ttu-id="83fdb-141">Затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="83fdb-141">Then, select **Next**.</span></span>

    ![Выберите сервер hello и диск](./media/backup-mabs-add-storage/mabs-add-storage-6.png)

## <a name="add-volumes-toobackup-server-disk-storage"></a><span data-ttu-id="83fdb-143">Добавление дискового пространства тома tooBackup сервера</span><span class="sxs-lookup"><span data-stu-id="83fdb-143">Add volumes tooBackup Server disk storage</span></span>

<span data-ttu-id="83fdb-144">tooadd tooBackup тома сервера, в hello **управления** области повторное сканирование хранилища hello, а затем выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="83fdb-144">tooadd a volume tooBackup Server, in hello **Management** pane, rescan hello storage, and then select **Add**.</span></span> <span data-ttu-id="83fdb-145">Появится список всех hello тома доступны toobe добавлена для хранения резервной копии сервера.</span><span class="sxs-lookup"><span data-stu-id="83fdb-145">A list of all hello volumes available toobe added for Backup Server Storage appears.</span></span> <span data-ttu-id="83fdb-146">После добавления списка toohello выбранных томов доступные тома дать им toohelp понятное имя, управлять ими.</span><span class="sxs-lookup"><span data-stu-id="83fdb-146">After available volumes are added toohello list of selected volumes, you can give them a friendly name toohelp you manage them.</span></span> <span data-ttu-id="83fdb-147">Эти tooReFS тома, резервное копирование сервера можно использовать преимущества hello современных хранилища резервной копии, выберите tooformat **ОК**.</span><span class="sxs-lookup"><span data-stu-id="83fdb-147">tooformat these volumes tooReFS so Backup Server can use hello benefits of Modern Backup Storage, select **OK**.</span></span>

![Добавление доступных томов](./media/backup-mabs-add-storage/mabs-add-storage-7.png)

## <a name="set-up-workload-aware-storage"></a><span data-ttu-id="83fdb-149">Настройка хранилища с учетом рабочих нагрузок</span><span class="sxs-lookup"><span data-stu-id="83fdb-149">Set up workload-aware storage</span></span>

<span data-ttu-id="83fdb-150">С учетом рабочей нагрузки хранилища можно выбрать hello томов, которые более хранят определенных типов рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="83fdb-150">With workload-aware storage, you can select hello volumes that preferentially store certain kinds of workloads.</span></span> <span data-ttu-id="83fdb-151">Например можно задать дорогих тома, которые поддерживают большое количество операций ввода вывода на второй (IOPS) toostore только hello рабочих нагрузок, требующих частые резервные большого объема.</span><span class="sxs-lookup"><span data-stu-id="83fdb-151">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) toostore only hello workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="83fdb-152">Примером может быть SQL Server с журналами транзакций.</span><span class="sxs-lookup"><span data-stu-id="83fdb-152">An example is SQL Server with transaction logs.</span></span> <span data-ttu-id="83fdb-153">Другие рабочие нагрузки, резервное копирование реже, таких как виртуальные машины, резервное копирование томов toolow затрат.</span><span class="sxs-lookup"><span data-stu-id="83fdb-153">Other workloads that are backed up less frequently, like VMs, can be backed up toolow-cost volumes.</span></span>

### <a name="update-dpmdiskstorage"></a><span data-ttu-id="83fdb-154">Update-DPMDiskStorage</span><span class="sxs-lookup"><span data-stu-id="83fdb-154">Update-DPMDiskStorage</span></span>

<span data-ttu-id="83fdb-155">Хранилище с поддержкой рабочей нагрузки можно настроить с помощью командлета PowerShell hello обновления DPMDiskStorage, который обновляет свойства hello тома в пуле носителей hello на сервере Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="83fdb-155">You can set up workload-aware storage by using hello PowerShell cmdlet Update-DPMDiskStorage, which updates hello properties of a volume in hello storage pool on a Data Protection Manager server.</span></span>

<span data-ttu-id="83fdb-156">Синтаксис:</span><span class="sxs-lookup"><span data-stu-id="83fdb-156">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```
<span data-ttu-id="83fdb-157">Hello следующей картинке показан командлет Update-DPMDiskStorage hello в окне PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="83fdb-157">hello following screenshot shows hello Update-DPMDiskStorage cmdlet in hello PowerShell window.</span></span>

![Команда DPMDiskStorage обновления в окне PowerShell hello Hello](./media/backup-mabs-add-storage/mabs-add-storage-8.png)

<span data-ttu-id="83fdb-159">Hello изменения, внесенные с помощью PowerShell, отражаются в hello консоли администратора сервера для резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="83fdb-159">hello changes you make by using PowerShell are reflected in hello Backup Server Administrator Console.</span></span>

![Диски и тома в консоли администрирования hello](./media/backup-mabs-add-storage/mabs-add-storage-9.png)

## <a name="next-steps"></a><span data-ttu-id="83fdb-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="83fdb-161">Next steps</span></span>
<span data-ttu-id="83fdb-162">После установки сервер резервного копирования, узнайте, как tooprepare сервере или включите защиту рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="83fdb-162">After you install Backup Server, learn how tooprepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="83fdb-163">Подготовка к резервному копированию рабочих нагрузок с использованием Azure Backup Server</span><span class="sxs-lookup"><span data-stu-id="83fdb-163">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="83fdb-164">Используйте резервное копирование сервера tooback сервер VMware</span><span class="sxs-lookup"><span data-stu-id="83fdb-164">Use Backup Server tooback up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="83fdb-165">Используйте резервное копирование сервера tooback копирование SQL Server</span><span class="sxs-lookup"><span data-stu-id="83fdb-165">Use Backup Server tooback up SQL Server</span></span>](backup-azure-sql-mabs.md)

