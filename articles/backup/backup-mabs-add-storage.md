---
title: "Использование Modern Backup Storage с Azure Backup Server версии 2 | Документация Майкрософт"
description: "Сведения о новых возможностях Azure Backup Server версии 2. В этой статье описывается обновление установки Backup Server."
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
ms.openlocfilehash: 751b9b495fd368dff1f72429707f5f33a0ccb569
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="add-storage-to-azure-backup-server-v2"></a><span data-ttu-id="e12c0-104">Добавление хранилища на Azure Backup Server версии 2</span><span class="sxs-lookup"><span data-stu-id="e12c0-104">Add storage to Azure Backup Server v2</span></span>

<span data-ttu-id="e12c0-105">Azure Backup Server версии 2 поставляется с Modern Backup Storage System Center 2016 Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="e12c0-105">Azure Backup Server v2 comes with System Center 2016 Data Protection Manager Modern Backup Storage.</span></span> <span data-ttu-id="e12c0-106">Modern Backup Storage обеспечивает до 50 % экономии пространства хранения, архивацию, которая в три раза быстрее, и более эффективное хранилище.</span><span class="sxs-lookup"><span data-stu-id="e12c0-106">Modern Backup Storage offers storage savings of 50 percent, backups that are three times faster, and more efficient storage.</span></span> <span data-ttu-id="e12c0-107">Кроме того, предлагается хранение с учетом рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="e12c0-107">It also offers workload-aware storage.</span></span> 

> [!NOTE]
> <span data-ttu-id="e12c0-108">Чтобы использовать Modern Backup Storage, необходимо запустить Backup Server версии 2 в Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="e12c0-108">To use Modern Backup Storage, you must run Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="e12c0-109">Если запустить Backup Server версии 2 на более ранней версии Windows Server, Azure Backup Server не сможет реализовать преимущества Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="e12c0-109">If you run Backup Server v2 on an earlier version of Windows Server, Azure Backup Server can't take advantage of Modern Backup Storage.</span></span> <span data-ttu-id="e12c0-110">Вместо этого он будет обеспечивать защиту рабочих нагрузок, как в случае с Backup Server версии 1.</span><span class="sxs-lookup"><span data-stu-id="e12c0-110">Instead, it protects workloads as it does with Backup Server v1.</span></span> <span data-ttu-id="e12c0-111">Дополнительные сведения см. в матрице защиты версий [Backup Server](backup-mabs-protection-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="e12c0-111">For more information, see the Backup Server version [protection matrix](backup-mabs-protection-matrix.md).</span></span>

## <a name="volumes-in-backup-server-v2"></a><span data-ttu-id="e12c0-112">Тома в Backup Server версии 2</span><span class="sxs-lookup"><span data-stu-id="e12c0-112">Volumes in Backup Server v2</span></span>

<span data-ttu-id="e12c0-113">Backup Server версии 2 поддерживает тома хранилища.</span><span class="sxs-lookup"><span data-stu-id="e12c0-113">Backup Server v2 accepts storage volumes.</span></span> <span data-ttu-id="e12c0-114">При добавлении тома Backup Server форматирует его в систему Resilient File System (ReFS), требуемую для Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="e12c0-114">When you add a volume, Backup Server formats the volume to Resilient File System (ReFS), which Modern Backup Storage requires.</span></span> <span data-ttu-id="e12c0-115">Чтобы добавить том и при необходимости раскрыть его позже, рекомендуется использовать следующий рабочий процесс:</span><span class="sxs-lookup"><span data-stu-id="e12c0-115">To add a volume, and to expand it later if you need to, we suggest that you use this workflow:</span></span>

1.  <span data-ttu-id="e12c0-116">Настройте Backup Server версии 2 на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="e12c0-116">Set up Backup Server v2 on a VM.</span></span>
2.  <span data-ttu-id="e12c0-117">Создайте том на виртуальном диске в пуле носителей:</span><span class="sxs-lookup"><span data-stu-id="e12c0-117">Create a volume on a virtual disk in a storage pool:</span></span>
    1.  <span data-ttu-id="e12c0-118">Добавьте диск в пул носителей и создайте виртуальный диск с простой структурой.</span><span class="sxs-lookup"><span data-stu-id="e12c0-118">Add a disk to a storage pool and create a virtual disk with simple layout.</span></span>
    2.  <span data-ttu-id="e12c0-119">Добавьте дополнительные диски и расширьте виртуальный диск.</span><span class="sxs-lookup"><span data-stu-id="e12c0-119">Add any additional disks, and extend the virtual disk.</span></span>
    3.  <span data-ttu-id="e12c0-120">Создайте тома на виртуальном диске.</span><span class="sxs-lookup"><span data-stu-id="e12c0-120">Create volumes on the virtual disk.</span></span>
3.  <span data-ttu-id="e12c0-121">Добавьте эти тома на Backup Server.</span><span class="sxs-lookup"><span data-stu-id="e12c0-121">Add the volumes to Backup Server.</span></span>
4.  <span data-ttu-id="e12c0-122">Настройте хранилище с учетом рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="e12c0-122">Configure workload-aware storage.</span></span>

## <a name="create-a-volume-for-modern-backup-storage"></a><span data-ttu-id="e12c0-123">Создание тома для Modern Backup Storage</span><span class="sxs-lookup"><span data-stu-id="e12c0-123">Create a volume for Modern Backup Storage</span></span>

<span data-ttu-id="e12c0-124">Использование Backup Server версии 2 в качестве дискового накопителя поможет полностью контролировать хранилище.</span><span class="sxs-lookup"><span data-stu-id="e12c0-124">Using Backup Server v2 with volumes as disk storage can help you maintain control over storage.</span></span> <span data-ttu-id="e12c0-125">Томом может быть один диск.</span><span class="sxs-lookup"><span data-stu-id="e12c0-125">A volume can be a single disk.</span></span> <span data-ttu-id="e12c0-126">Тем не менее, если вы хотите расширить хранилище в будущем, создайте том из дисков с незадействованным дисковым пространством.</span><span class="sxs-lookup"><span data-stu-id="e12c0-126">However, if you want to extend storage in the future, create a volume out of a disk created by using storage spaces.</span></span> <span data-ttu-id="e12c0-127">Это поможет при необходимости увеличить размер тома для хранения резервных копий.</span><span class="sxs-lookup"><span data-stu-id="e12c0-127">This can help if you want to expand the volume for backup storage.</span></span> <span data-ttu-id="e12c0-128">В данном разделе приведены рекомендации по созданию тома с такой конфигурацией.</span><span class="sxs-lookup"><span data-stu-id="e12c0-128">This section offers best practices for creating a volume with this setup.</span></span>

1. <span data-ttu-id="e12c0-129">В диспетчере сервера выберите **Файловые службы и службы хранилища** > **Тома** > **Пулы носителей**.</span><span class="sxs-lookup"><span data-stu-id="e12c0-129">In Server Manager, select **File and Storage Services** > **Volumes** > **Storage Pools**.</span></span> <span data-ttu-id="e12c0-130">В разделе **ФИЗИЧЕСКИЕ ДИСКИ** выберите **Новый пул носителей**.</span><span class="sxs-lookup"><span data-stu-id="e12c0-130">Under **PHYSICAL DISKS**, select **New Storage Pool**.</span></span> 

    ![Создание учетной записи хранения](./media/backup-mabs-add-storage/mabs-add-storage-1.png)

2. <span data-ttu-id="e12c0-132">В раскрывающемся списке **Задачи** выберите **New Virtual Disk** (Создать виртуальный диск).</span><span class="sxs-lookup"><span data-stu-id="e12c0-132">In the **TASKS** drop-down box, select **New Virtual Disk**.</span></span>

    ![Добавление виртуального диска](./media/backup-mabs-add-storage/mabs-add-storage-2.png)

3. <span data-ttu-id="e12c0-134">Выберите пул носителей, а затем выберите **Добавление физического диска**.</span><span class="sxs-lookup"><span data-stu-id="e12c0-134">Select the storage pool, and then select **Add Physical Disk**.</span></span>

    ![Добавление физического диска](./media/backup-mabs-add-storage/mabs-add-storage-3.png)

4. <span data-ttu-id="e12c0-136">Выберите физический диск, а затем выберите **Расширение виртуального диска**.</span><span class="sxs-lookup"><span data-stu-id="e12c0-136">Select the physical disk, and then select **Extend Virtual Disk**.</span></span>

    ![Расширение виртуального диска](./media/backup-mabs-add-storage/mabs-add-storage-4.png)

5. <span data-ttu-id="e12c0-138">Выберите виртуальный диск, а затем выберите **Новый том**.</span><span class="sxs-lookup"><span data-stu-id="e12c0-138">Select the virtual disk, and then select **New Volume**.</span></span>

    ![Создание нового тома](./media/backup-mabs-add-storage/mabs-add-storage-5.png)

6. <span data-ttu-id="e12c0-140">В диалоговом окне **Выбор сервера или диска** выберите сервер и новый диск.</span><span class="sxs-lookup"><span data-stu-id="e12c0-140">In the **Select the server and disk** dialog, select the server and the new disk.</span></span> <span data-ttu-id="e12c0-141">Затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e12c0-141">Then, select **Next**.</span></span>

    ![Выбор сервера и диска](./media/backup-mabs-add-storage/mabs-add-storage-6.png)

## <a name="add-volumes-to-backup-server-disk-storage"></a><span data-ttu-id="e12c0-143">Добавление тома для хранилища дисков Backup Server</span><span class="sxs-lookup"><span data-stu-id="e12c0-143">Add volumes to Backup Server disk storage</span></span>

<span data-ttu-id="e12c0-144">Чтобы добавить том на Backup Server в области **Управление**, повторно просканируйте хранилище, а затем выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e12c0-144">To add a volume to Backup Server, in the **Management** pane, rescan the storage, and then select **Add**.</span></span> <span data-ttu-id="e12c0-145">Отобразится список всех томов, которые можно добавить в Backup Server Storage.</span><span class="sxs-lookup"><span data-stu-id="e12c0-145">A list of all the volumes available to be added for Backup Server Storage appears.</span></span> <span data-ttu-id="e12c0-146">После добавления в список выбранных томов доступных томов можно присвоить им понятные имена, чтобы упростить управление.</span><span class="sxs-lookup"><span data-stu-id="e12c0-146">After available volumes are added to the list of selected volumes, you can give them a friendly name to help you manage them.</span></span> <span data-ttu-id="e12c0-147">Чтобы отформатировать эти тома в ReFS и использовать преимущества Modern Backup Storage, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e12c0-147">To format these volumes to ReFS so Backup Server can use the benefits of Modern Backup Storage, select **OK**.</span></span>

![Добавление доступных томов](./media/backup-mabs-add-storage/mabs-add-storage-7.png)

## <a name="set-up-workload-aware-storage"></a><span data-ttu-id="e12c0-149">Настройка хранилища с учетом рабочих нагрузок</span><span class="sxs-lookup"><span data-stu-id="e12c0-149">Set up workload-aware storage</span></span>

<span data-ttu-id="e12c0-150">Используя хранилище с учетом рабочих нагрузок, можно выбрать предпочтительные тома для хранения определенных типов рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="e12c0-150">With workload-aware storage, you can select the volumes that preferentially store certain kinds of workloads.</span></span> <span data-ttu-id="e12c0-151">Например, можно указать ресурсоемкие тома, которые поддерживают большое количество операций ввода-вывода в секунду (IOPS), для хранения только рабочих нагрузок, требующих частого создания резервных копий большого объема.</span><span class="sxs-lookup"><span data-stu-id="e12c0-151">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) to store only the workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="e12c0-152">Примером может быть SQL Server с журналами транзакций.</span><span class="sxs-lookup"><span data-stu-id="e12c0-152">An example is SQL Server with transaction logs.</span></span> <span data-ttu-id="e12c0-153">Рабочие нагрузки, архивация которых выполняется реже, например виртуальные машины, можно архивировать на недорогие тома.</span><span class="sxs-lookup"><span data-stu-id="e12c0-153">Other workloads that are backed up less frequently, like VMs, can be backed up to low-cost volumes.</span></span>

### <a name="update-dpmdiskstorage"></a><span data-ttu-id="e12c0-154">Update-DPMDiskStorage</span><span class="sxs-lookup"><span data-stu-id="e12c0-154">Update-DPMDiskStorage</span></span>

<span data-ttu-id="e12c0-155">Хранилище с учетом рабочих нагрузок можно настроить с помощью командлета PowerShell Update-DPMDiskStorage, обновляющего свойства тома в пуле носителей на сервере Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="e12c0-155">You can set up workload-aware storage by using the PowerShell cmdlet Update-DPMDiskStorage, which updates the properties of a volume in the storage pool on a Data Protection Manager server.</span></span>

<span data-ttu-id="e12c0-156">Синтаксис:</span><span class="sxs-lookup"><span data-stu-id="e12c0-156">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```
<span data-ttu-id="e12c0-157">На следующем изображении показан командлет Update-DPMDiskStorage в окне PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e12c0-157">The following screenshot shows the Update-DPMDiskStorage cmdlet in the PowerShell window.</span></span>

![Команда Update-DPMDiskStorage в окне PowerShell](./media/backup-mabs-add-storage/mabs-add-storage-8.png)

<span data-ttu-id="e12c0-159">Изменения, внесенные с помощью PowerShell, отражаются в консоли администрирования Backup Server.</span><span class="sxs-lookup"><span data-stu-id="e12c0-159">The changes you make by using PowerShell are reflected in the Backup Server Administrator Console.</span></span>

![Диски и тома в консоли администрирования](./media/backup-mabs-add-storage/mabs-add-storage-9.png)

## <a name="next-steps"></a><span data-ttu-id="e12c0-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e12c0-161">Next steps</span></span>
<span data-ttu-id="e12c0-162">После установки Backup Server узнайте, как подготовить сервер или обеспечить защиту рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e12c0-162">After you install Backup Server, learn how to prepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="e12c0-163">Подготовка к резервному копированию рабочих нагрузок с использованием Azure Backup Server</span><span class="sxs-lookup"><span data-stu-id="e12c0-163">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="e12c0-164">Резервное копирование сервера VMware в Azure</span><span class="sxs-lookup"><span data-stu-id="e12c0-164">Use Backup Server to back up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="e12c0-165">Архивация баз данных SQL Server в Azure с помощью Azure Backup Server</span><span class="sxs-lookup"><span data-stu-id="e12c0-165">Use Backup Server to back up SQL Server</span></span>](backup-azure-sql-mabs.md)

