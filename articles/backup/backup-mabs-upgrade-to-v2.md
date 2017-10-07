---
title: "Резервное копирование Azure v2 aaaInstall | Документы Microsoft"
description: "Azure Backup Server версии 2 предоставляет расширенные возможности резервного копирования для защиты виртуальных машин, файлов и папок, рабочих нагрузок и т. д. Узнайте, как tooinstall или обновление tooAzure v2 резервное копирование."
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
ms.openlocfilehash: 5b1699dadd3a173f1c0ef91a1a600bc5e12f20ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-azure-backup-server-v2"></a><span data-ttu-id="64ebb-104">Установка Azure Backup Server версии 2</span><span class="sxs-lookup"><span data-stu-id="64ebb-104">Install Azure Backup Server v2</span></span>

<span data-ttu-id="64ebb-105">Azure Backup Server обеспечивает защиту виртуальных машин, рабочих нагрузок, файлов, папок и т. д.</span><span class="sxs-lookup"><span data-stu-id="64ebb-105">Azure Backup Server helps protect your virtual machines (VMs), workloads, files and folders, and more.</span></span> <span data-ttu-id="64ebb-106">Компонент Azure Backup Server версии 2 основан на Azure Backup Server версии 1 и предоставляет новые функции, недоступные в версии 1.</span><span class="sxs-lookup"><span data-stu-id="64ebb-106">Azure Backup Server v2 builds on Azure Backup Server v1, and gives you new features that are not available in v1.</span></span> <span data-ttu-id="64ebb-107">Сравнение функций версии 1 и версии 2 см. в [таблице поддержки защиты Azure Backup Server](backup-mabs-protection-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="64ebb-107">For a comparison of features between v1 and v2, see [Azure Backup Server protection matrix](backup-mabs-protection-matrix.md).</span></span> 

<span data-ttu-id="64ebb-108">Дополнительные компоненты Hello в версии v2 резервное копирование не обновление с версии 1 сервер резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="64ebb-108">hello additional features in Backup Server v2 are an upgrade from Backup Server v1.</span></span> <span data-ttu-id="64ebb-109">Тем не менее Backup Server версии 1 не является необходимым компонентом для установки Backup Server версии 2.</span><span class="sxs-lookup"><span data-stu-id="64ebb-109">However, Backup Server v1 is not a prerequisite for installing Backup Server v2.</span></span> <span data-ttu-id="64ebb-110">Если вы хотите tooupgrade из tooBackup v1 резервное копирование сервера v2, установите v2 резервное копирование на сервере защиты резервное копирование сервера hello.</span><span class="sxs-lookup"><span data-stu-id="64ebb-110">If you want tooupgrade from Backup Server v1 tooBackup Server v2, install Backup Server v2 on hello Backup Server protection server.</span></span> <span data-ttu-id="64ebb-111">Существующие параметры Backup Server останутся неизменными.</span><span class="sxs-lookup"><span data-stu-id="64ebb-111">Your existing Backup Server settings remain intact.</span></span>

<span data-ttu-id="64ebb-112">Backup Server версии 2 можно установить на сервере Windows Server 2012 R2 или Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="64ebb-112">You can install Backup Server v2 on Windows Server 2012 R2 or Windows Server 2016.</span></span> <span data-ttu-id="64ebb-113">tootake преимуществами новых функций, например System Center 2016 данных защиты диспетчера современном хранилища резервных копий и v2 резервное копирование сервера необходимо установить на Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="64ebb-113">tootake advantage of new features like System Center 2016 Data Protection Manager Modern Backup Storage, you must install Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="64ebb-114">Перед обновлением установки tooor v2 резервное копирование, узнайте, как hello [необходимые условия для установки](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="64ebb-114">Before you upgrade tooor install Backup Server v2, read about hello [installation prerequisites](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites).</span></span>

> [!NOTE]
> <span data-ttu-id="64ebb-115">Сервер резервного копирования Azure имеет hello одинаковый код базовой как System Center Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="64ebb-115">Azure Backup Server has hello same code base as System Center Data Protection Manager.</span></span> <span data-ttu-id="64ebb-116">Резервного копирования сервера v1 эквивалентные tooData Protection Manager 2012 R2, который v2 резервное копирование эквивалентные tooData 2016 Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="64ebb-116">Backup Server v1 is equivalent tooData Protection Manager 2012 R2, and Backup Server v2 is equivalent tooData Protection Manager 2016.</span></span> <span data-ttu-id="64ebb-117">В этой статье иногда ссылается документации hello Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="64ebb-117">This article occasionally references hello Data Protection Manager documentation.</span></span>
>
>

## <a name="upgrade-backup-server-toov2"></a><span data-ttu-id="64ebb-118">Обновление toov2 резервное копирование сервера</span><span class="sxs-lookup"><span data-stu-id="64ebb-118">Upgrade Backup Server toov2</span></span>
<span data-ttu-id="64ebb-119">tooupgrade из tooBackup v1 резервное копирование сервера v2, обеспечивающее установку hello необходимых обновлений:</span><span class="sxs-lookup"><span data-stu-id="64ebb-119">tooupgrade from Backup Server v1 tooBackup Server v2, make sure your installation has hello required updates:</span></span>

- <span data-ttu-id="64ebb-120">[Обновление агентов защиты hello](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent) на hello защищенные серверы.</span><span class="sxs-lookup"><span data-stu-id="64ebb-120">[Update hello protection agents](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent) on hello protected servers.</span></span>
- <span data-ttu-id="64ebb-121">Обновление Windows Server 2012 R2 tooWindows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="64ebb-121">Upgrade Windows Server 2012 R2 tooWindows Server 2016.</span></span>
- <span data-ttu-id="64ebb-122">обновление удаленного администратора Azure Backup Server на всех рабочих серверах;</span><span class="sxs-lookup"><span data-stu-id="64ebb-122">Upgrade Azure Backup Server Remote Administrator on all production servers.</span></span>
- <span data-ttu-id="64ebb-123">Убедитесь, что резервные копии являются toocontinue без перезагрузки рабочего сервера.</span><span class="sxs-lookup"><span data-stu-id="64ebb-123">Ensure that backups are set toocontinue without restarting your production server.</span></span>


### <a name="upgrade-steps-for-backup-server-v2"></a><span data-ttu-id="64ebb-124">Действия по обновлению до Backup Server версии 2</span><span class="sxs-lookup"><span data-stu-id="64ebb-124">Upgrade steps for Backup Server v2</span></span>

1. <span data-ttu-id="64ebb-125">В hello центра загрузки Майкрософт [загрузить установщик обновления hello](https://go.microsoft.com/fwlink/?LinkId=626082).</span><span class="sxs-lookup"><span data-stu-id="64ebb-125">In hello Download Center, [download hello upgrade installer](https://go.microsoft.com/fwlink/?LinkId=626082).</span></span>

2. <span data-ttu-id="64ebb-126">После извлечения приветствия мастера установки убедитесь, что **выполнения setup.exe** выбранного, а затем выберите **Готово**.</span><span class="sxs-lookup"><span data-stu-id="64ebb-126">After you extract hello setup wizard, make sure that **Execute setup.exe** is selected, and then select **Finish**.</span></span>

  ![Установщик — выполнение установки](./media/backup-mabs-upgrade-to-v2/run-setup.png)

3. <span data-ttu-id="64ebb-128">В мастере Microsoft Azure Backup Server hello под **установить**выберите **Microsoft Azure Backup Server**.</span><span class="sxs-lookup"><span data-stu-id="64ebb-128">In hello Microsoft Azure Backup Server wizard, under **Install**, select **Microsoft Azure Backup Server**.</span></span>

  ![Установщик — выбор установки](./media/backup-mabs-upgrade-to-v2/mabs-installer-s1.png)

4. <span data-ttu-id="64ebb-130">На hello **приветствия** страницы, просмотрите предупреждения hello и выберите **Далее**.</span><span class="sxs-lookup"><span data-stu-id="64ebb-130">On hello **Welcome** page, review hello warnings, and then select **Next**.</span></span>

  ![Установщик — страница приветствия](./media/backup-mabs-upgrade-to-v2/mabs-installer-s2.png)

5. <span data-ttu-id="64ebb-132">Мастер установки Hello выполняет проверки предварительных требований для toomake том, что можно обновить в вашей среде.</span><span class="sxs-lookup"><span data-stu-id="64ebb-132">hello setup wizard performs prerequisite checks toomake sure your environment can upgrade.</span></span> <span data-ttu-id="64ebb-133">На hello **Prerequisite Checks** выберите **проверьте**.</span><span class="sxs-lookup"><span data-stu-id="64ebb-133">On hello **Prerequisite Checks** page, select **Check**.</span></span>

  ![Установщик — страница "Проверки на наличие необходимых компонентов"](./media/backup-mabs-upgrade-to-v2/mabs-installer-s3-perform-checks.png)

6. <span data-ttu-id="64ebb-135">Среды должны пройти проверки готовности к установке hello.</span><span class="sxs-lookup"><span data-stu-id="64ebb-135">Your environment must pass hello prerequisite checks.</span></span> <span data-ttu-id="64ebb-136">Если в вашей среде не прошли проверку hello, обратите внимание hello проблемы и устранить ее.</span><span class="sxs-lookup"><span data-stu-id="64ebb-136">If your environment doesn't pass hello checks, note hello issues and fix them.</span></span> <span data-ttu-id="64ebb-137">Затем нажмите кнопку **Повторить проверку**.</span><span class="sxs-lookup"><span data-stu-id="64ebb-137">Then, select **Check Again**.</span></span> <span data-ttu-id="64ebb-138">После прохождения проверки предварительных требований для hello выберите **Далее**.</span><span class="sxs-lookup"><span data-stu-id="64ebb-138">After you pass hello prerequisite checks, select **Next**.</span></span>

  ![Установщик — кнопка "Повторить проверку"](./media/backup-mabs-upgrade-to-v2/mabs-installer-s4-pass-checks.png)

7. <span data-ttu-id="64ebb-140">На hello **параметры SQL** выберите hello соответствующий параметр для установки SQL и затем выберите **проверить и установить**.</span><span class="sxs-lookup"><span data-stu-id="64ebb-140">On hello **SQL Settings** page, select hello relevant option for your SQL installation, and then select **Check and Install**.</span></span>

  ![Установщик — страница "Настройки SQL"](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5-sql-settings.png)

  <span data-ttu-id="64ebb-142">Hello проверки может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="64ebb-142">hello checks might take a few minutes.</span></span> <span data-ttu-id="64ebb-143">Когда hello проверки завершается, выберите **Далее**.</span><span class="sxs-lookup"><span data-stu-id="64ebb-143">When hello checks are finished, select **Next**.</span></span>

  ![Установщик — кнопка "Проверить и установить" на странице "Настройки SQL"](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5a-check-and fix-settings.png)

8. <span data-ttu-id="64ebb-145">На hello **параметры установки** задайте любые изменения toohello каталоге, где установлен сервер резервного копирования или toohello расположение временных файлов.</span><span class="sxs-lookup"><span data-stu-id="64ebb-145">On hello **Installation Settings** page, make any changes toohello location where Backup Server is installed, or toohello Scratch Location.</span></span> <span data-ttu-id="64ebb-146">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="64ebb-146">Select **Next**.</span></span>

  ![Установщик — страница "Параметры установки"](./media/backup-mabs-upgrade-to-v2/mabs-installer-s6-installation-settings.png)

9. <span data-ttu-id="64ebb-148">toofinish приветствия мастера установки выберите **Готово**.</span><span class="sxs-lookup"><span data-stu-id="64ebb-148">toofinish hello setup wizard, select **Finish**.</span></span>

  ![Установщик — кнопка "Готово"](./media/backup-mabs-upgrade-to-v2/run-setup.png)



## <a name="add-storage-for-modern-backup-storage"></a><span data-ttu-id="64ebb-150">Добавление хранилища для Modern Backup Storage</span><span class="sxs-lookup"><span data-stu-id="64ebb-150">Add storage for Modern Backup Storage</span></span>

<span data-ttu-id="64ebb-151">эффективность хранения резервных копий tooimprove, резервное копирование сервера v2 добавляет поддержку для тома.</span><span class="sxs-lookup"><span data-stu-id="64ebb-151">tooimprove backup storage efficiency, Backup Server v2 adds support for volumes.</span></span> <span data-ttu-id="64ebb-152">Как и Backup Server версии 1, Backup Server версии 2 поддерживает диски.</span><span class="sxs-lookup"><span data-stu-id="64ebb-152">Like Backup Server v1, Backup Server v2 supports disks.</span></span>

### <a name="add-volumes-and-disks"></a><span data-ttu-id="64ebb-153">Добавление томов и дисков</span><span class="sxs-lookup"><span data-stu-id="64ebb-153">Add volumes and disks</span></span>
<span data-ttu-id="64ebb-154">При запуске v2 резервное копирование сервера в Windows Server 2016 можно использовать тома toostore резервных копий данных.</span><span class="sxs-lookup"><span data-stu-id="64ebb-154">If you run Backup Server v2 on Windows Server 2016, you can use volumes toostore backup data.</span></span> <span data-ttu-id="64ebb-155">Тома обеспечивают экономию места в хранилище и более быстрое создание резервных копий.</span><span class="sxs-lookup"><span data-stu-id="64ebb-155">Volumes offer storage savings and faster backups.</span></span> <span data-ttu-id="64ebb-156">Так как тома tooBackup новый сервер, необходимо добавить их.</span><span class="sxs-lookup"><span data-stu-id="64ebb-156">Because volumes are new tooBackup Server, you must add them.</span></span> 

<span data-ttu-id="64ebb-157">При добавлении тома tooBackup сервера hello тома можно дать понятное имя.</span><span class="sxs-lookup"><span data-stu-id="64ebb-157">When you add a volume tooBackup Server, you can give hello volume a friendly name.</span></span> <span data-ttu-id="64ebb-158">Нажмите кнопку hello **понятное имя** столбца hello тома требуется tooname.</span><span class="sxs-lookup"><span data-stu-id="64ebb-158">Click hello **Friendly Name** column of hello volume you want tooname.</span></span> <span data-ttu-id="64ebb-159">Можно изменить имя hello позже, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="64ebb-159">You can change hello name later, if necessary.</span></span> <span data-ttu-id="64ebb-160">Также можно использовать PowerShell tooadd или изменить понятные имена для тома.</span><span class="sxs-lookup"><span data-stu-id="64ebb-160">You also can use PowerShell tooadd or change friendly names for volumes.</span></span>

<span data-ttu-id="64ebb-161">tooadd тома в hello консоль администратора:</span><span class="sxs-lookup"><span data-stu-id="64ebb-161">tooadd a volume in hello Administrator Console:</span></span>

1. <span data-ttu-id="64ebb-162">В hello консоли администратора сервера для резервного копирования Azure, выберите **управления** > **дисковый накопитель** > **добавить**.</span><span class="sxs-lookup"><span data-stu-id="64ebb-162">In hello Azure Backup Server Administrator Console, select **Management** > **Disk Storage** > **Add**.</span></span>

    ![Привет открыть мастер Добавление дискового хранилища](./media//backup-mabs-upgrade-to-v2/open-add-disk-storage-wizard.png)

    <span data-ttu-id="64ebb-164">Откроется мастер добавления дискового хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="64ebb-164">This opens hello Add Disk Storage wizard.</span></span>

2. <span data-ttu-id="64ebb-165">На hello **Добавление дискового хранилища** страницы в hello **доступные тома** выберите тома и затем выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="64ebb-165">On hello **Add Disk Storage** page, in hello **Available volumes** box, select a volume, and then select **Add**.</span></span>
3. <span data-ttu-id="64ebb-166">В hello **выбранных томов** введите понятное имя для hello тома и затем выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="64ebb-166">In hello **Selected volumes** box, enter a friendly name for hello volume, and then select **OK**.</span></span>

      ![Мастер добавления дискового накопителя — добавление тома](./media/backup-mabs-upgrade-to-v2/add-volume.png)

  <span data-ttu-id="64ebb-168">Следует tooadd диск hello диск должен принадлежать группы защиты tooa с предыдущих версий хранилища.</span><span class="sxs-lookup"><span data-stu-id="64ebb-168">If you want tooadd a disk, hello disk must belong tooa protection group that has legacy storage.</span></span> <span data-ttu-id="64ebb-169">Такие диски можно использовать только для этих групп защиты.</span><span class="sxs-lookup"><span data-stu-id="64ebb-169">These disks can only be used for these protection groups.</span></span> <span data-ttu-id="64ebb-170">Если резервное копирование не содержит источников, которые имеют защиты прежних версий, hello диска нет в списке.</span><span class="sxs-lookup"><span data-stu-id="64ebb-170">If Backup Server doesn't have sources that have legacy protection, hello disk isn't listed.</span></span>

  <span data-ttu-id="64ebb-171">Дополнительные сведения о добавлении дисков см. в разделе [добавлять диски tooincrease устаревших хранилища](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage).</span><span class="sxs-lookup"><span data-stu-id="64ebb-171">For more information about adding disks, see [Adding disks tooincrease legacy storage](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage).</span></span> <span data-ttu-id="64ebb-172">Диску нельзя присвоить понятное имя.</span><span class="sxs-lookup"><span data-stu-id="64ebb-172">You can't give a disk a friendly name.</span></span>


### <a name="assign-workloads-toovolumes"></a><span data-ttu-id="64ebb-173">Назначьте toovolumes рабочих нагрузок</span><span class="sxs-lookup"><span data-stu-id="64ebb-173">Assign workloads toovolumes</span></span>

<span data-ttu-id="64ebb-174">В резервное копирование сервера можно указать, рабочая нагрузка назначаются toowhich тома.</span><span class="sxs-lookup"><span data-stu-id="64ebb-174">In Backup Server, you specify which workloads are assigned toowhich volumes.</span></span> <span data-ttu-id="64ebb-175">Например можно задать дорогих тома, которые поддерживают большое количество операций ввода вывода на второй (IOPS) toostore только рабочих нагрузок, требующих частые резервные большого объема.</span><span class="sxs-lookup"><span data-stu-id="64ebb-175">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) toostore only workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="64ebb-176">Примером может быть SQL Server с журналами транзакций.</span><span class="sxs-lookup"><span data-stu-id="64ebb-176">An example is SQL Server with transaction logs.</span></span>

#### <a name="update-dpmdiskstorage"></a><span data-ttu-id="64ebb-177">Update-DPMDiskStorage</span><span class="sxs-lookup"><span data-stu-id="64ebb-177">Update-DPMDiskStorage</span></span>

<span data-ttu-id="64ebb-178">свойства hello tooupdate тома в пуле носителей hello в резервное копирование с помощью командлета PowerShell hello DPMDiskStorage обновления.</span><span class="sxs-lookup"><span data-stu-id="64ebb-178">tooupdate hello properties of a volume in hello storage pool in Backup Server, use hello PowerShell cmdlet Update-DPMDiskStorage.</span></span>

<span data-ttu-id="64ebb-179">Синтаксис:</span><span class="sxs-lookup"><span data-stu-id="64ebb-179">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

<span data-ttu-id="64ebb-180">Все изменения, внесенные с помощью PowerShell, отражаются в hello пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="64ebb-180">All changes that you make by using PowerShell are reflected in hello UI.</span></span>


## <a name="protect-data-sources"></a><span data-ttu-id="64ebb-181">Защита источников данных</span><span class="sxs-lookup"><span data-stu-id="64ebb-181">Protect data sources</span></span>
<span data-ttu-id="64ebb-182">toobegin защиту источников данных, создайте группу защиты.</span><span class="sxs-lookup"><span data-stu-id="64ebb-182">toobegin protecting data sources, create a protection group.</span></span> <span data-ttu-id="64ebb-183">Здравствуйте, выполнив шаги выделения изменения или дополнения toohello мастера новой группы защиты.</span><span class="sxs-lookup"><span data-stu-id="64ebb-183">hello following steps highlight changes or additions toohello New Protection Group wizard.</span></span>

<span data-ttu-id="64ebb-184">toocreate группы защиты:</span><span class="sxs-lookup"><span data-stu-id="64ebb-184">toocreate a protection group:</span></span>

1. <span data-ttu-id="64ebb-185">В hello консоли администрирования сервера резервной копии, выберите **защиты**.</span><span class="sxs-lookup"><span data-stu-id="64ebb-185">In hello Backup Server Administrator Console, select **Protection**.</span></span>

2. <span data-ttu-id="64ebb-186">Выберите на ленте инструментов hello, **New**.</span><span class="sxs-lookup"><span data-stu-id="64ebb-186">On hello tool ribbon, select **New**.</span></span>

    <span data-ttu-id="64ebb-187">Откроется мастер создания новой группы защиты hello.</span><span class="sxs-lookup"><span data-stu-id="64ebb-187">This opens hello Create New Protection Group wizard.</span></span>

  ![Создание мастера создания новой группы защиты](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-1.png)

3. <span data-ttu-id="64ebb-189">На hello **приветствия** выберите **Далее**.</span><span class="sxs-lookup"><span data-stu-id="64ebb-189">On hello **Welcome** page, select **Next**.</span></span>
4. <span data-ttu-id="64ebb-190">На hello **Выбор типа группы защиты** выберите тип hello группы защиты toocreate и затем выберите **Далее**.</span><span class="sxs-lookup"><span data-stu-id="64ebb-190">On hello **Select Protection Group Type** page, select hello type of protection group you want toocreate, and then select **Next**.</span></span>

  ![Страница "Выбор типа группы защиты"](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-2.png)

5. <span data-ttu-id="64ebb-192">На hello **Выбор членов группы** страницы в hello **доступные элементы** панели, элементы hello перечисленных агентов защиты.</span><span class="sxs-lookup"><span data-stu-id="64ebb-192">On hello **Select Group Members** page, in hello **Available members** pane, hello members with protection agents are listed.</span></span> <span data-ttu-id="64ebb-193">Например, выберите том D:\ и E:\ и добавить их toohello **выбранные элементы** области.</span><span class="sxs-lookup"><span data-stu-id="64ebb-193">For this example, select volume D:\ and E:\ and add them toohello **Selected members** pane.</span></span> <span data-ttu-id="64ebb-194">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="64ebb-194">Select **Next**.</span></span>

  ![Страница "Выбор элементов группы"](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-3.png)

6. <span data-ttu-id="64ebb-196">На hello **Выбор метода защиты данных** введите **имя группы защиты**, Выбор метода защиты hello, а затем выберите **Далее**.</span><span class="sxs-lookup"><span data-stu-id="64ebb-196">On hello **Select Data Protection Method** page, enter a **Protection group name**, select hello protection method, and then select **Next**.</span></span> <span data-ttu-id="64ebb-197">Если вы хотите краткосрочной защиты, необходимо выбрать hello **диска** метод резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="64ebb-197">If you want short-term protection, you must select hello **Disk** backup method.</span></span>

  ![Страница "Выбор метода защиты данных"](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-4.png)

7. <span data-ttu-id="64ebb-199">На hello **Выбор краткосрочных целей** , выберите hello параметры страницы для **диапазон хранения** и **частоты синхронизации**.</span><span class="sxs-lookup"><span data-stu-id="64ebb-199">On hello **Specify Short-Term Goals** page, select hello details for **Retention range** and **Synchronization frequency**.</span></span> <span data-ttu-id="64ebb-200">Затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="64ebb-200">Then, select **Next**.</span></span> <span data-ttu-id="64ebb-201">При необходимости toochange hello расписания для при точек восстановления, сделанной, выберите **изменить**.</span><span class="sxs-lookup"><span data-stu-id="64ebb-201">Optionally, toochange hello schedule for when recovery points are taken, select **Modify**.</span></span>

  ![Страница "Выбор краткосрочных целей"](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-5.png)

8. <span data-ttu-id="64ebb-203">На hello **Просмотр выделения дискового накопителя** просмотрите подробные сведения о выбранных источников данных hello, размер и значения для подготовки toobe пространства hello и hello конечный том хранилища.</span><span class="sxs-lookup"><span data-stu-id="64ebb-203">On hello **Review Disk Storage Allocation** page, review details about hello data sources you selected, their size, and  values for hello space toobe provisioned and hello target storage volume.</span></span>

  ![Страница "Проверка выделения дискового накопителя"](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-6.png)

  <span data-ttu-id="64ebb-205">Тома хранилища основаны на выделение hello на томе рабочей нагрузки (задается с помощью PowerShell) и hello доступное хранилище.</span><span class="sxs-lookup"><span data-stu-id="64ebb-205">Storage volumes are based on hello workload volume allocation (set by using PowerShell) and hello available storage.</span></span> <span data-ttu-id="64ebb-206">Hello томов хранения данных можно изменить, выбрав другие тома в раскрывающемся меню hello.</span><span class="sxs-lookup"><span data-stu-id="64ebb-206">You can change hello storage volumes by selecting other volumes in hello drop-down menu.</span></span> <span data-ttu-id="64ebb-207">Если изменить значение hello для **целевое хранилище**, hello значение для **свободного хранилища** динамически изменяется tooreflect значения в разделе **свободного места** и **Underprovisioned пространства**.</span><span class="sxs-lookup"><span data-stu-id="64ebb-207">If you change hello value for **Target Storage**, hello value for **Available disk storage** dynamically changes tooreflect values under **Free Space** and **Underprovisioned Space**.</span></span>

  <span data-ttu-id="64ebb-208">Если источники данных hello как планировалось, hello значение hello **Underprovisioned пространства** столбца в **свободного хранилища** отображает hello объем дополнительного хранилища, которые необходимы.</span><span class="sxs-lookup"><span data-stu-id="64ebb-208">If hello data sources grow as planned, hello value for hello **Underprovisioned Space** column in **Available disk storage** reflects hello amount of additional storage that's needed.</span></span> <span data-ttu-id="64ebb-209">Используйте этот план toohelp значение требуемый объем дискового пространства для smooth резервных копий.</span><span class="sxs-lookup"><span data-stu-id="64ebb-209">Use this value toohelp plan your storage needs for smooth backups.</span></span> <span data-ttu-id="64ebb-210">Если hello значение равно нулю, нет никаких потенциальных проблем с хранилищем в обозримом будущем hello.</span><span class="sxs-lookup"><span data-stu-id="64ebb-210">If hello value is zero, there are no potential problems with storage in hello foreseeable future.</span></span> <span data-ttu-id="64ebb-211">Если значение hello число, отличное от нуля, у вас недостаточно места в хранилище (в зависимости от вашей защиты политики и hello размер данных защищенных членов).</span><span class="sxs-lookup"><span data-stu-id="64ebb-211">If hello value is a number other than zero, you do not have sufficient storage allocated  (based on your protection policy and hello data size of your protected members).</span></span>

  ![Неподготовленное дисковое пространство](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-7.png)

   <span data-ttu-id="64ebb-213">Создание группы, завершенной hello мастер защиты toofinish.</span><span class="sxs-lookup"><span data-stu-id="64ebb-213">toofinish creating your protection group, complete hello wizard.</span></span>

## <a name="migrate-legacy-storage-toomodern-backup-storage"></a><span data-ttu-id="64ebb-214">Миграция устаревших хранилища tooModern хранилища резервных копий</span><span class="sxs-lookup"><span data-stu-id="64ebb-214">Migrate legacy storage tooModern Backup Storage</span></span>
<span data-ttu-id="64ebb-215">После обновления установки tooor v2 резервное копирование и обновления hello операционной системы tooWindows Server 2016, обновите ваш toouse групп защиты современных хранилища резервных копий.</span><span class="sxs-lookup"><span data-stu-id="64ebb-215">After you upgrade tooor install Backup Server v2 and upgrade hello operating system tooWindows Server 2016, update your protection groups toouse Modern Backup Storage.</span></span> <span data-ttu-id="64ebb-216">По умолчанию группы защиты не изменяются.</span><span class="sxs-lookup"><span data-stu-id="64ebb-216">By default, protection groups are not changed.</span></span> <span data-ttu-id="64ebb-217">Они toofunction выполняться так, как они были изначально настроены.</span><span class="sxs-lookup"><span data-stu-id="64ebb-217">They continue toofunction as they were initially set up.</span></span> 

<span data-ttu-id="64ebb-218">Обновление группы защиты toouse современных хранилища резервных копий является необязательным.</span><span class="sxs-lookup"><span data-stu-id="64ebb-218">Updating protection groups toouse Modern Backup Storage is optional.</span></span> <span data-ttu-id="64ebb-219">группы защиты tooupdate hello, остановите защиту всех источников данных с помощью hello вариант сохранения данных.</span><span class="sxs-lookup"><span data-stu-id="64ebb-219">tooupdate hello protection group, stop protection of all data sources by using hello retain data option.</span></span> <span data-ttu-id="64ebb-220">Затем добавьте hello данных источников tooa новой группы защиты.</span><span class="sxs-lookup"><span data-stu-id="64ebb-220">Then, add hello data sources tooa new protection group.</span></span>

1. <span data-ttu-id="64ebb-221">В hello консоли администрирования, выберите hello **защиты** компонентов.</span><span class="sxs-lookup"><span data-stu-id="64ebb-221">In hello Administrator Console, select hello **Protection** feature.</span></span> <span data-ttu-id="64ebb-222">В hello **члена группы защиты** , щелкните правой кнопкой мыши элемент hello и затем выберите **остановить защиту элемента**.</span><span class="sxs-lookup"><span data-stu-id="64ebb-222">In hello **Protection Group Member** list, right-click hello member, and then select **Stop protection of member**.</span></span>

  ![Остановка защиты элемента](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-stop-protection1.png)

2. <span data-ttu-id="64ebb-224">В hello **удалить из группы** диалоговое окно, просмотрите hello используется дискового пространства и hello свободное место для пула носителей hello.</span><span class="sxs-lookup"><span data-stu-id="64ebb-224">In hello **Remove from Group** dialog box, review hello used disk space and hello available free space for hello storage pool.</span></span> <span data-ttu-id="64ebb-225">по умолчанию Hello — точек восстановления hello tooleave на диске hello и разрешить им tooexpire на их политику хранения, связанные.</span><span class="sxs-lookup"><span data-stu-id="64ebb-225">hello default is tooleave hello recovery points on hello disk and allow them tooexpire per their associated retention policy.</span></span> <span data-ttu-id="64ebb-226">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="64ebb-226">Click **OK**.</span></span>

  <span data-ttu-id="64ebb-227">Tooimmediately возвращаемого hello используется дискового пространства toohello свободного накопителя, установите hello **удалить реплику на диске** флажок toodelete hello резервных копий данных (и точек восстановления), связанный с этим элементом.</span><span class="sxs-lookup"><span data-stu-id="64ebb-227">If you want tooimmediately return hello used disk space toohello free storage pool, select hello **Delete replica on disk** check box toodelete hello backup data (and recovery points) associated with that member.</span></span>

  ![Диалоговое окно "Удалить из группы"](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-retain-data.png)

3. <span data-ttu-id="64ebb-229">Создайте группу защиты, которая использует Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="64ebb-229">Create a protection group that uses Modern Backup Storage.</span></span> <span data-ttu-id="64ebb-230">Включает защиту hello источники данных.</span><span class="sxs-lookup"><span data-stu-id="64ebb-230">Include hello unprotected data sources.</span></span>


## <a name="add-disks-tooincrease-legacy-storage"></a><span data-ttu-id="64ebb-231">Добавление дисков tooincrease устаревших хранилища</span><span class="sxs-lookup"><span data-stu-id="64ebb-231">Add disks tooincrease legacy storage</span></span>

<span data-ttu-id="64ebb-232">Следует toouse устаревших хранилища с резервное копирование может потребоваться tooincrease хранения tooadd дисков для прежних версий.</span><span class="sxs-lookup"><span data-stu-id="64ebb-232">If you want toouse legacy storage with Backup Server, you might need tooadd disks tooincrease legacy storage.</span></span> 

<span data-ttu-id="64ebb-233">дисковый накопитель, tooadd:</span><span class="sxs-lookup"><span data-stu-id="64ebb-233">tooadd disk storage:</span></span>

1. <span data-ttu-id="64ebb-234">В hello консоли администрирования, выберите **управления** > **дисковый накопитель** > **добавить**.</span><span class="sxs-lookup"><span data-stu-id="64ebb-234">In hello Administrator Console, select **Management** > **Disk Storage** > **Add**.</span></span>

    ![Диалоговое окно "Добавить дисковый накопитель"](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-add-disk-storage.png)

4. <span data-ttu-id="64ebb-236">В hello **Добавление дискового хранилища** диалогового окна выберите **добавить диски**.</span><span class="sxs-lookup"><span data-stu-id="64ebb-236">In hello **Add Disk Storage** dialog, select **Add disks**.</span></span>

5. <span data-ttu-id="64ebb-237">В список доступных дисков hello, выберите hello дисков требуется tooadd, выберите **добавить**, а затем выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="64ebb-237">In hello list of available disks, select hello disks you want tooadd, select **Add**, and then select **OK**.</span></span>

## <a name="update-hello-data-protection-manager-protection-agent"></a><span data-ttu-id="64ebb-238">Обновление агента защиты hello Data Protection Manager</span><span class="sxs-lookup"><span data-stu-id="64ebb-238">Update hello Data Protection Manager protection agent</span></span>

<span data-ttu-id="64ebb-239">Резервное копирование сервера использует hello агент защиты System Center Data Protection Manager для обновлений.</span><span class="sxs-lookup"><span data-stu-id="64ebb-239">Backup Server uses hello System Center Data Protection Manager protection agent for updates.</span></span> <span data-ttu-id="64ebb-240">При обновлении агента защиты, которая не является toohello подключенной сети нельзя использовать консоль администрирования диспетчера защиты данных toocomplete обновление подключенного агента hello.</span><span class="sxs-lookup"><span data-stu-id="64ebb-240">If you are upgrading a protection agent that is not connected toohello network, you cannot use hello Data Protection Manager Administrator Console toocomplete a connected agent upgrade.</span></span> <span data-ttu-id="64ebb-241">Необходимо обновить агент защиты hello в неактивной доменной среде.</span><span class="sxs-lookup"><span data-stu-id="64ebb-241">You must upgrade hello protection agent in a nonactive domain environment.</span></span> <span data-ttu-id="64ebb-242">Пока hello клиентский компьютер не toohello подключенной сети, консоль администрирования диспетчера защиты данных показывает, что обновление агента защиты hello hello находится в состоянии ожидания.</span><span class="sxs-lookup"><span data-stu-id="64ebb-242">Until hello client computer is connected toohello network, hello Data Protection Manager Administrator Console shows that hello protection agent update is pending.</span></span>

<span data-ttu-id="64ebb-243">Hello ниже описано, как tooupdate агенты защиты для клиентских компьютеров, подключенных и клиентских компьютеров, которые не подключены.</span><span class="sxs-lookup"><span data-stu-id="64ebb-243">hello following sections describe how tooupdate protection agents for client computers that are connected and client computers that are not connected.</span></span>

### <a name="update-a-protection-agent-for-a-connected-client-computer"></a><span data-ttu-id="64ebb-244">Обновление агента защиты на клиентском компьютере, подключенном к сети</span><span class="sxs-lookup"><span data-stu-id="64ebb-244">Update a protection agent for a connected client computer</span></span>

1. <span data-ttu-id="64ebb-245">В hello консоли администрирования сервера резервной копии, выберите **управления** > **агенты**.</span><span class="sxs-lookup"><span data-stu-id="64ebb-245">In hello Backup Server Administrator Console, select **Management** > **Agents**.</span></span>

2. <span data-ttu-id="64ebb-246">В области отображения hello выберите hello клиентских компьютеров, для которых требуется агент защиты tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="64ebb-246">In hello display pane, select hello client computers for which you want tooupdate hello protection agent.</span></span>

  > [!NOTE]
  > <span data-ttu-id="64ebb-247">Hello **обновления агентов** столбца указывает, когда обновление агента защиты доступен для каждого защищенного компьютера.</span><span class="sxs-lookup"><span data-stu-id="64ebb-247">hello **Agent Updates** column indicates when a protection agent update is available for each protected computer.</span></span> <span data-ttu-id="64ebb-248">В hello **действия** области, hello **обновление** действие доступно только при выборе защищенного компьютера и обновления становятся доступными.</span><span class="sxs-lookup"><span data-stu-id="64ebb-248">In hello **Actions** pane, hello **Update** action is available only when a protected computer is selected and updates are available.</span></span>
  >
  >

3. <span data-ttu-id="64ebb-249">tooinstall обновить агенты защиты на компьютерах hello выбран hello **действия** выберите **обновление**.</span><span class="sxs-lookup"><span data-stu-id="64ebb-249">tooinstall updated protection agents on hello selected computers, in hello **Actions** pane, select **Update**.</span></span>

### <a name="update-a-protection-agent-on-a-client-computer-that-is-not-connected"></a><span data-ttu-id="64ebb-250">Обновление агента защиты на клиентском компьютере, не подключенном к сети</span><span class="sxs-lookup"><span data-stu-id="64ebb-250">Update a protection agent on a client computer that is not connected</span></span>

1. <span data-ttu-id="64ebb-251">В hello консоли администрирования сервера резервной копии, выберите **управления** > **агенты**.</span><span class="sxs-lookup"><span data-stu-id="64ebb-251">In hello Backup Server Administrator Console, select **Management** > **Agents**.</span></span>

2. <span data-ttu-id="64ebb-252">В области отображения hello выберите hello клиентских компьютеров, для которых требуется агент защиты tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="64ebb-252">In hello display pane, select hello client computers for which you want tooupdate hello protection agent.</span></span>

  > [!NOTE]
   > <span data-ttu-id="64ebb-253">Hello **обновления агентов** столбца указывает, когда обновление агента защиты доступен для каждого защищенного компьютера.</span><span class="sxs-lookup"><span data-stu-id="64ebb-253">hello **Agent Updates** column indicates when a protection agent update is available for each protected computer.</span></span> <span data-ttu-id="64ebb-254">В hello **действия** области, hello **обновление** действие не было доступно при выборе защищенного компьютера, если обновления недоступны.</span><span class="sxs-lookup"><span data-stu-id="64ebb-254">In hello **Actions** pane, hello **Update** action is not available when a protected computer is selected unless updates are available.</span></span>
  >
  >

3. <span data-ttu-id="64ebb-255">tooinstall обновить агенты защиты на компьютерах, выбранных hello, выберите **обновление**.</span><span class="sxs-lookup"><span data-stu-id="64ebb-255">tooinstall updated protection agents on hello selected computers, select **Update**.</span></span>

4. <span data-ttu-id="64ebb-256">Для клиентского компьютера, не подключен сети toohello до компьютера hello toohello подключенной сети, hello **состояние агента** столбце отображается состояние **обновить Ожидание**.</span><span class="sxs-lookup"><span data-stu-id="64ebb-256">For a client computer that is not connected toohello network, until hello computer is connected toohello network, hello **Agent Status** column shows a status of **Update Pending**.</span></span>

  <span data-ttu-id="64ebb-257">После toohello подключенной сети клиентский компьютер hello **обновления агентов** для hello в столбце отображается состояние **обновление**.</span><span class="sxs-lookup"><span data-stu-id="64ebb-257">After a client computer is connected toohello network, hello **Agent Updates** column for hello client computer shows a status of **Updating**.</span></span>
  
### <a name="move-legacy-protection-groups-from-old-version-and-sync-hello-new-version-with-azure"></a><span data-ttu-id="64ebb-258">Перемещение старых групп защиты из старая и новая версия синхронизации hello с Azure</span><span class="sxs-lookup"><span data-stu-id="64ebb-258">Move legacy Protection groups from old version and sync hello new version with Azure</span></span>

<span data-ttu-id="64ebb-259">После резервного копирования Azure и hello ОС обновления, предпринимается готов tooprotect современных хранилища резервных копий с помощью новых источников данных.</span><span class="sxs-lookup"><span data-stu-id="64ebb-259">Once Azure Backup Server and hello OS are both updated, you are ready tooprotect new data sources using Modern Backup Storage.</span></span> <span data-ttu-id="64ebb-260">Однако уже защищенные источники данных по-прежнему toobe, защищены hello прежних версий, каким образом они находились в Azure Backup Server, но все новые защиты будут использовать современные хранилища резервных копий.</span><span class="sxs-lookup"><span data-stu-id="64ebb-260">However already protected data sources will continue toobe protected in hello legacy way as they were in Azure Backup Server but all new protection will use Modern Backup Storage.</span></span>

<span data-ttu-id="64ebb-261">Шаги, описанные ниже являются источниками данных toomigrate из устаревший режим защиты tooModern резервного хранилища.</span><span class="sxs-lookup"><span data-stu-id="64ebb-261">Below steps are toomigrate data sources from legacy  mode of protection tooModern backup storage.</span></span>

<span data-ttu-id="64ebb-262">• Добавьте hello нового тома toohello пула носителей DPM и назначить понятные имена и данные источника теги при необходимости.</span><span class="sxs-lookup"><span data-stu-id="64ebb-262">• Add hello new volume(s) toohello DPM storage pool and assign friendly names and data source tags if desired.</span></span>
<span data-ttu-id="64ebb-263">• Для каждого источника данных, который находится в стандартном режиме, остановите защиту источников данных hello и «Сохранить защищенные данные».</span><span class="sxs-lookup"><span data-stu-id="64ebb-263">• For each data source that is in legacy mode, stop protection of hello data sources and “Retain Protected Data”.</span></span>  <span data-ttu-id="64ebb-264">Так вы сможете восстановить старые точки восстановления после миграции.</span><span class="sxs-lookup"><span data-stu-id="64ebb-264">This will allow recovery of old recovery points after migration.</span></span>

<span data-ttu-id="64ebb-265">• Создание новой группы защиты и выберите hello источников данных, которые являются toobe, сохраненных с помощью нового формата.</span><span class="sxs-lookup"><span data-stu-id="64ebb-265">• Create a new PG and select hello data sources that are toobe stored using new format.</span></span>
<span data-ttu-id="64ebb-266">• DPM будет выполнять копирование реплики из хранилища резервных копий предыдущих версий hello в hello современных хранения резервных копий томов локально.</span><span class="sxs-lookup"><span data-stu-id="64ebb-266">• DPM will do a replica copy from hello legacy backup storage into hello Modern Backup Storage volume locally.</span></span>
<span data-ttu-id="64ebb-267">Примечание. Это будет рассматриваться как задания операций, выполняемых после восстановления. • Все новые точки синхронизации и восстановления будут храниться в Modern Backup Storage.</span><span class="sxs-lookup"><span data-stu-id="64ebb-267">Note: This will be seen as a post-recovery operation job • All new sync and recovery points will then be stored in Modern Backup Storage.</span></span>
<span data-ttu-id="64ebb-268">• Старые точки восстановления будут очищены как их действия и в конечном итоге освобождения дискового пространства hello.</span><span class="sxs-lookup"><span data-stu-id="64ebb-268">• Old recovery points will be pruned out as they expire and eventually free up hello disk space.</span></span>
<span data-ttu-id="64ebb-269">• После hello томов, удаляются из hello старое хранилище, hello диск можно удалить из системы резервного копирования и hello Azure.</span><span class="sxs-lookup"><span data-stu-id="64ebb-269">• Once all hello legacy volumes are deleted from hello old storage, hello disk can be removed from Azure backup and hello system.</span></span>
<span data-ttu-id="64ebb-270">• Резервное копирование hello Azure DPMDB.</span><span class="sxs-lookup"><span data-stu-id="64ebb-270">• Take a backup of hello  Azure DPMDB.</span></span>

<span data-ttu-id="64ebb-271">Часть 2:-важные элементы > hello новом сервере должна toobe с таким же именем как hello исходный сервер службы архивации Azure.</span><span class="sxs-lookup"><span data-stu-id="64ebb-271">Part 2: -Important items> hello new server will need toobe named same as hello original Azure Backup server.</span></span> <span data-ttu-id="64ebb-272">Невозможно изменить имя hello hello нового сервера Azure резервного копирования toouse старый пул носителей и точек восстановления tooretain DPMDB - должен иметь резервную копию DPMDB, как его потребуется восстановить toobe</span><span class="sxs-lookup"><span data-stu-id="64ebb-272">You cannot change hello name of hello new Azure backup server if you want toouse old storage pool and DPMDB tooretain recovery points -Must have backup of DPMDB  as it will need toobe restored</span></span>

1) <span data-ttu-id="64ebb-273">Завершение работы hello исходного сервера Azure резервного копирования или убрать hello сети.</span><span class="sxs-lookup"><span data-stu-id="64ebb-273">Shutdown hello original Azure backup server or take it off hello wire.</span></span>
2) <span data-ttu-id="64ebb-274">Сброс hello учетной записи компьютера в active directory.</span><span class="sxs-lookup"><span data-stu-id="64ebb-274">Reset hello machine account in active directory.</span></span>
3) <span data-ttu-id="64ebb-275">Установите Server 2016 на новом компьютере, а имя его hello машины именем hello исходного сервера Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="64ebb-275">Install Server 2016 on new machine and name it hello same machine name as hello original Azure Backup server.</span></span>
4) <span data-ttu-id="64ebb-276">Присоединение hello домена</span><span class="sxs-lookup"><span data-stu-id="64ebb-276">Join hello Domain</span></span>
5) <span data-ttu-id="64ebb-277">Установите Azure Backup Server V2 (переместите диски пула хранилища DPM со старого сервера и выполните импорт).</span><span class="sxs-lookup"><span data-stu-id="64ebb-277">Install Azure Backup server V2 (Move DPM Storage pool disks from old server and import)</span></span>
6) <span data-ttu-id="64ebb-278">Восстановление hello DPMDB, взяты из конца часть 2</span><span class="sxs-lookup"><span data-stu-id="64ebb-278">Restore hello DPMDB taken from end of part 2</span></span>
7) <span data-ttu-id="64ebb-279">Подключите hello хранилища из hello исходный сервер резервного копирования toohello новый сервер.</span><span class="sxs-lookup"><span data-stu-id="64ebb-279">Attach hello storage from hello original backup server toohello new server.</span></span>
8) <span data-ttu-id="64ebb-280">Из восстановления SQL hello DPMDB</span><span class="sxs-lookup"><span data-stu-id="64ebb-280">From SQL Restore hello DPMDB</span></span>
9) <span data-ttu-id="64ebb-281">Из командной строки администратора на компакт-диск tooMicrosoft нового сервера Azure Backup установите папку bin</span><span class="sxs-lookup"><span data-stu-id="64ebb-281">From admin command line on new server cd tooMicrosoft Azure Backup install location and bin folder</span></span>

<span data-ttu-id="64ebb-282">Пример пути: C:\windows\system32>cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\\</span><span class="sxs-lookup"><span data-stu-id="64ebb-282">Path example: C:\windows\system32>cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\\</span></span>
<span data-ttu-id="64ebb-283">резервное копирование tooAzure выполните команду DPMSYNC-SYNC</span><span class="sxs-lookup"><span data-stu-id="64ebb-283">tooAzure backup Run DPMSYNC -SYNC</span></span>

10) <span data-ttu-id="64ebb-284">Выполните команду DPMSYNC-SYNC Примечание При добавлении НОВЫХ дисков пул носителей DPM toohello вместо перемещения hello старых, выполните команду DPMSYNC - Reallocatereplica</span><span class="sxs-lookup"><span data-stu-id="64ebb-284">Run DPMSYNC -SYNC Note If you have added NEW disks toohello DPM Storage pool instead of moving hello old ones, then run DPMSYNC -Reallocatereplica</span></span>

## <a name="new-powershell-cmdlets-in-v2"></a><span data-ttu-id="64ebb-285">Новые командлеты PowerShell в версии 2</span><span class="sxs-lookup"><span data-stu-id="64ebb-285">New PowerShell cmdlets in v2</span></span>

<span data-ttu-id="64ebb-286">При установке Azure Backup Server версии 2 доступны два новых командлета:</span><span class="sxs-lookup"><span data-stu-id="64ebb-286">When you install Azure Backup Server v2, two new cmdlets are available:</span></span> 
* <span data-ttu-id="64ebb-287">[Mount-DPMRecoveryPoint](https://technet.microsoft.com/library/mt787159.aspx);</span><span class="sxs-lookup"><span data-stu-id="64ebb-287">[Mount-DPMRecoveryPoint](https://technet.microsoft.com/library/mt787159.aspx)</span></span>
* <span data-ttu-id="64ebb-288">[Dismount-DPMRecoveryPoint](https://technet.microsoft.com/library/mt787158.aspx).</span><span class="sxs-lookup"><span data-stu-id="64ebb-288">[Dismount-DPMRecoveryPoint](https://technet.microsoft.com/library/mt787158.aspx)</span></span>

## <a name="next-steps"></a><span data-ttu-id="64ebb-289">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="64ebb-289">Next steps</span></span>

<span data-ttu-id="64ebb-290">Узнайте, как tooprepare сервере или включите защиту рабочей нагрузки:</span><span class="sxs-lookup"><span data-stu-id="64ebb-290">Learn how tooprepare your server or begin protecting a workload:</span></span>
- [<span data-ttu-id="64ebb-291">Подготовка к резервному копированию рабочих нагрузок с использованием Azure Backup Server</span><span class="sxs-lookup"><span data-stu-id="64ebb-291">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="64ebb-292">Используйте резервное копирование сервера tooback сервер VMware</span><span class="sxs-lookup"><span data-stu-id="64ebb-292">Use Backup Server tooback up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="64ebb-293">Используйте резервное копирование сервера tooback копирование SQL Server</span><span class="sxs-lookup"><span data-stu-id="64ebb-293">Use Backup Server tooback up SQL Server</span></span>](backup-azure-sql-mabs.md)
- <span data-ttu-id="64ebb-294">[Add storage to Azure Backup Server v2](backup-mabs-add-storage.md) (Добавление хранилища к Azure Backup Server версии 2)</span><span class="sxs-lookup"><span data-stu-id="64ebb-294">[Use Modern Backup Storage with Backup Server](backup-mabs-add-storage.md)</span></span>

