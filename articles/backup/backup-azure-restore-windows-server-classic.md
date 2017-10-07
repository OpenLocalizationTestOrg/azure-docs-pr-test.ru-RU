---
title: "Здравствуйте, aaaRestore tooa данных Windows Server или Windows клиента из Azure с помощью классической модели развертывания | Документы Microsoft"
description: "Узнайте, как toorestore с сервера или клиента Windows."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 85585dfc-c764-4e8c-8f0e-40b969640ac2
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 4d1458d5233c4f55004ecfa95cbf7b3b18a03dde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="restore-files-tooa-windows-server-or-windows-client-machine-using-hello-classic-deployment-model"></a><span data-ttu-id="2e7c6-103">Восстановить файлы tooa Windows server и клиентским компьютером Windows, с помощью hello классической модели развертывания</span><span class="sxs-lookup"><span data-stu-id="2e7c6-103">Restore files tooa Windows server or Windows client machine using hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2e7c6-104">Классический портал.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-104">Classic portal</span></span>](backup-azure-restore-windows-server-classic.md)
> * [<span data-ttu-id="2e7c6-105">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="2e7c6-105">Azure portal</span></span>](backup-azure-restore-windows-server.md)
>
>

<span data-ttu-id="2e7c6-106">В этой статье объясняется, как toorecover данных из резервной копии в хранилище и восстановить его tooa сервер или компьютер.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-106">This article explains how toorecover data from a backup vault and restore it tooa server or computer.</span></span> <span data-ttu-id="2e7c6-107">Начиная с марта 2017 г., больше не создаются резервные хранилища hello классическом портале.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-107">Starting in March 2017, you can no longer create backup vaults in hello classic portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2e7c6-108">Теперь можно обновить вашими хранилищами служб tooRecovery хранилища резервной копии.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-108">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="2e7c6-109">Дополнительные сведения см. в статье hello [обновление tooa хранилища резервной копии, в хранилище служб восстановления](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="2e7c6-109">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="2e7c6-110">Корпорация Майкрософт рекомендует tooupgrade вашей резервных хранилищ tooRecovery хранилищами служб.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-110">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="2e7c6-111">**15 октября 2017 г.**, вы больше не будет возможности toouse PowerShell toocreate резервное копирование хранилищ.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-111">**October 15, 2017**, you will no longer be able toouse PowerShell toocreate Backup vaults.</span></span> <br/> <span data-ttu-id="2e7c6-112">**Начиная с 1 ноября 2017 г.**:</span><span class="sxs-lookup"><span data-stu-id="2e7c6-112">**Starting November 1, 2017**:</span></span>
>- <span data-ttu-id="2e7c6-113">Все оставшиеся хранилища резервной копии будет автоматически обновленные tooRecovery хранилищами служб.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-113">Any remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="2e7c6-114">Вы не будет возможности tooaccess данные резервной копии hello классического портала.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-114">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="2e7c6-115">Вместо этого используйте hello Azure портала tooaccess резервного копирования данных в хранилищах службы восстановления.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-115">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

<span data-ttu-id="2e7c6-116">toorestore данных, используется мастер восстановления данных hello hello агента служб восстановления Microsoft Azure (режим MARS).</span><span class="sxs-lookup"><span data-stu-id="2e7c6-116">toorestore data, you use hello Recover Data wizard in hello Microsoft Azure Recovery Services (MARS) agent.</span></span> <span data-ttu-id="2e7c6-117">При восстановлении данных можно использовать следующие возможности.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-117">When you restore data, it is possible to:</span></span>

* <span data-ttu-id="2e7c6-118">Восстановление данных toohello же машину из какие резервные копии hello были выполнены.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-118">Restore data toohello same machine from which hello backups were taken.</span></span>
* <span data-ttu-id="2e7c6-119">Восстановление данных tooan альтернативный машины.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-119">Restore data tooan alternate machine.</span></span>

<span data-ttu-id="2e7c6-120">В января 2017 г. Корпорация Майкрософт выпустила агент предварительной версии обновления toohello режима MARS.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-120">In January 2017, Microsoft released a Preview update toohello MARS agent.</span></span> <span data-ttu-id="2e7c6-121">Вместе с исправления ошибок это обновление позволяет мгновенное восстановление, позволяющий toomount моментальный снимок точки восстановления для записи в качестве тома для восстановления.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-121">Along with bug fixes, this update enables Instant Restore, which allows you toomount a writeable recovery point snapshot as a recovery volume.</span></span> <span data-ttu-id="2e7c6-122">Затем можно исследовать hello восстановления тома и скопируйте файлы tooa локального компьютера выборочно тем самым восстановление файлов.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-122">You can then explore hello recovery volume and copy files tooa local computer thereby selectively restoring files.</span></span>

> [!NOTE]
> <span data-ttu-id="2e7c6-123">Hello [января 2017 г. обновление резервного копирования Azure](https://support.microsoft.com/en-us/help/3216528?preview) является обязательным, если вы хотите toouse мгновенное восстановление toorestore данные.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-123">hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is required if you want toouse Instant Restore toorestore data.</span></span> <span data-ttu-id="2e7c6-124">Также в хранилищах в регионах, перечисленных в статье поддержка hello, должны быть защищены hello резервных копий данных.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-124">Also hello backup data must be protected in vaults in locales listed in hello support article.</span></span> <span data-ttu-id="2e7c6-125">Обратитесь к hello [января 2017 г. обновление резервного копирования Azure](https://support.microsoft.com/en-us/help/3216528?preview) для hello последний список языков, поддерживающих мгновенное восстановление.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-125">Consult hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) for hello latest list of locales that support Instant Restore.</span></span> <span data-ttu-id="2e7c6-126">Сейчас мгновенное восстановление доступно **не во всех** регионах.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-126">Instant Restore is **not** currently available in all locales.</span></span>
>

<span data-ttu-id="2e7c6-127">Мгновенное восстановление доступно для использования в хранилищах службы восстановления в hello портал Azure и хранилищ архивации hello классического портала.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-127">Instant Restore is available for use in Recovery Services vaults in hello Azure portal and Backup vaults in hello classic portal.</span></span> <span data-ttu-id="2e7c6-128">Мгновенное восстановление toouse следует загрузить обновление MARS hello и следуйте процедурам hello с упоминанием мгновенное восстановление.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-128">If you want toouse Instant Restore, download hello MARS update, and follow hello procedures that mention Instant Restore.</span></span>


## <a name="use-instant-restore-toorecover-data-toohello-same-machine"></a><span data-ttu-id="2e7c6-129">Используйте мгновенное восстановление данных toohello toorecover компьютере</span><span class="sxs-lookup"><span data-stu-id="2e7c6-129">Use Instant Restore toorecover data toohello same machine</span></span>

<span data-ttu-id="2e7c6-130">Если случайно удален файл и пожеланий toorestore его toohello, на одном компьютере (с какой hello резервная копия), hello следующие шаги помогут вам восстановить данные hello.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-130">If you accidentally deleted a file and wish toorestore it toohello same machine (from which hello backup is taken), hello following steps will help you recover hello data.</span></span>

1. <span data-ttu-id="2e7c6-131">Откройте hello **архивации Microsoft Azure** привязка в.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-131">Open hello **Microsoft Azure Backup** snap in.</span></span> <span data-ttu-id="2e7c6-132">Если вы не знаете, где установлена оснастка hello в, поиск hello компьютере или сервере **архивации Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-132">If you don't know where hello snap in was installed, search hello computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="2e7c6-133">Настольные приложения Hello должны отображаться в результатах поиска hello.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-133">hello desktop app should appear in hello search results.</span></span>

2. <span data-ttu-id="2e7c6-134">Нажмите кнопку **восстановить данные** toostart приветствия мастера.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-134">Click **Recover Data** toostart hello wizard.</span></span>

    ![Восстановить данные](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="2e7c6-136">На hello **Приступая к работе** области, toohello данных hello toorestore того же сервера или компьютера, выберите **этим сервером (`<server name>`)** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-136">On hello **Getting Started** pane, toorestore hello data toohello same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Выберите этот сервер toohello параметр toorestore hello данных того же компьютера](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. <span data-ttu-id="2e7c6-138">На hello **выберите режим восстановления** области, выберите **отдельные файлы и папки** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-138">On hello **Select Recovery Mode** pane, choose **Individual files and folders** and then click **Next**.</span></span>

    ![Обзор файлов](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. <span data-ttu-id="2e7c6-140">На hello **выберите том и дату** области, выберите hello томов, которые содержат hello файлы и папки, которые вы хотите toorestore.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-140">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="2e7c6-141">Hello календаре выберите точку восстановления.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-141">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="2e7c6-142">Можно восстановить данные на любой момент времени.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-142">You can restore from any recovery point in time.</span></span> <span data-ttu-id="2e7c6-143">Даты в **полужирным** указать hello доступность по крайней мере одна точка восстановления.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-143">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="2e7c6-144">После выбора даты, если доступны несколько точек восстановления, выберите hello конкретную точку восстановления из hello **время** раскрывающееся меню.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-144">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Том и дата](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. <span data-ttu-id="2e7c6-146">После выбора toorestore точки восстановления hello щелкните **подключить**.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-146">Once you have chosen hello recovery point toorestore, click **Mount**.</span></span>

    <span data-ttu-id="2e7c6-147">Резервное копирование Azure подключает точку локального восстановления hello и использует его в качестве тома для восстановления.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-147">Azure Backup mounts hello local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="2e7c6-148">На hello **обзора и восстанавливать файлы** области, нажмите кнопку **Обзор** tooopen проводника поиска hello файлы и папки требуется.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-148">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![Варианты восстановления](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. <span data-ttu-id="2e7c6-150">В проводнике Windows, hello копировать файлы или папки toorestore и вставить их tooany расположение toohello на локальном сервере или компьютере.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-150">In Windows Explorer, copy hello files and/or folders you want toorestore and paste them tooany location local toohello server or computer.</span></span> <span data-ttu-id="2e7c6-151">Можно открыть или поток файлов hello непосредственно из тома для восстановления hello и проверить hello правильных версий восстанавливаются.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-151">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![Скопируйте и вставьте файлы и папки из расположения toolocal подключенный том](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. <span data-ttu-id="2e7c6-153">После завершения восстановления hello файлы и папки на hello **обзора и файлов восстановления** области, нажмите кнопку **Unmount**.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-153">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="2e7c6-154">Нажмите кнопку **Да** tooconfirm, что требуется toounmount hello тома.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-154">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![Отсоединить том hello и подтвердите](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="2e7c6-156">Если не щелкнуть Unmount, hello тома для восстановления останется подключенного шесть часов с момента hello, когда он был подключен.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-156">If you do not click Unmount, hello Recovery Volume will remain mounted for six hours from hello time when it was mounted.</span></span> <span data-ttu-id="2e7c6-157">Операции резервного копирования будет выполняться во время монтирования тома hello.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-157">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="2e7c6-158">Toorun все запланированные операции резервного копирования во время hello при монтировании тома hello будет выполняться после восстановления тома hello в отключены.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-158">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >


## <a name="recover-data-toohello-same-machine"></a><span data-ttu-id="2e7c6-159">Восстановление данных toohello же компьютере</span><span class="sxs-lookup"><span data-stu-id="2e7c6-159">Recover data toohello same machine</span></span>
<span data-ttu-id="2e7c6-160">Если случайно удален файл и пожеланий toorestore его toohello, на одном компьютере (с какой hello резервная копия), hello следующие шаги помогут вам восстановить данные hello.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-160">If you accidentally deleted a file and wish toorestore it toohello same machine (from which hello backup is taken), hello following steps will help you recover hello data.</span></span>

1. <span data-ttu-id="2e7c6-161">Откройте hello **архивации Microsoft Azure** привязка в.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-161">Open hello **Microsoft Azure Backup** snap in.</span></span>
2. <span data-ttu-id="2e7c6-162">Нажмите кнопку **восстановить данные** рабочего процесса tooinitiate hello.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-162">Click **Recover Data** tooinitiate hello workflow.</span></span>

    ![Восстановить данные](./media/backup-azure-restore-windows-server-classic/recover.png)
3. <span data-ttu-id="2e7c6-164">Выберите hello  **этот сервер (*имявашегокомпьютера*) ** hello toorestore параметр резервной копии файла на hello же машине.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-164">Select hello **This server (*yourmachinename*)** option toorestore hello backed up file on hello same machine.</span></span>

    ![Тот же компьютер](./media/backup-azure-restore-windows-server-classic/samemachine.png)
4. <span data-ttu-id="2e7c6-166">Выберите слишком**Обзор файлов** или **поиск файлов**.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-166">Choose too**Browse for files** or **Search for files**.</span></span>

    <span data-ttu-id="2e7c6-167">Оставьте параметр по умолчанию hello при планировании toorestore один или несколько файлов, путь которого известен.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-167">Leave hello default option if you plan toorestore one or more files whose path is known.</span></span> <span data-ttu-id="2e7c6-168">Если есть сомнения по поводу hello структуру папок, но хотите toosearch для файла, выберите hello **поиск файлов** параметр.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-168">If you are not sure about hello folder structure but would like toosearch for a file, pick hello **Search for files** option.</span></span> <span data-ttu-id="2e7c6-169">Цель этого раздела hello мы будет продолжена с параметром по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-169">For hello purpose of this section, we will proceed with hello default option.</span></span>

    ![Обзор файлов](./media/backup-azure-restore-windows-server-classic/browseandsearch.png)
5. <span data-ttu-id="2e7c6-171">Выберите том hello, с которого требуется файл toorestore hello.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-171">Select hello volume from which you wish toorestore hello file.</span></span>

    <span data-ttu-id="2e7c6-172">Можно восстановить файл на любой момент времени.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-172">You can restore from any point in time.</span></span> <span data-ttu-id="2e7c6-173">Даты, которые отображаются в **полужирным** в элементе управления календаря hello указать доступность hello точки восстановления.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-173">Dates which appear in **bold** in hello calendar control indicate hello availability of a restore point.</span></span> <span data-ttu-id="2e7c6-174">После выбора даты на основе расписания резервного копирования (и hello успешности выполнения операции резервного копирования), можно выбрать точку времени из hello **время** раскрывающийся список.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-174">Once a date is selected, based on your backup schedule (and hello success of a backup operation), you can select a point in time from hello **Time** drop down.</span></span>

    ![Том и дата](./media/backup-azure-restore-windows-server-classic/volanddate.png)
6. <span data-ttu-id="2e7c6-176">Выберите элементы toorecover hello.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-176">Select hello items toorecover.</span></span> <span data-ttu-id="2e7c6-177">Вы можете выбрать несколько папок и файлов нужно toorestore.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-177">You can multi-select folders/files you wish toorestore.</span></span>

    ![Выбор файлов](./media/backup-azure-restore-windows-server-classic/selectfiles.png)
7. <span data-ttu-id="2e7c6-179">Укажите параметры восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-179">Specify hello recovery parameters.</span></span>

    ![Варианты восстановления](./media/backup-azure-restore-windows-server-classic/recoveroptions.png)

   * <span data-ttu-id="2e7c6-181">У вас есть возможность восстановить исходное расположение toohello (в которой hello файла или папки, будут перезаписываться) или tooanother расположение в hello же компьютере.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-181">You have an option of restoring toohello original location (in which hello file/folder would be overwritten) or tooanother location in hello same machine.</span></span>
   * <span data-ttu-id="2e7c6-182">Если hello файл или папку, нужно toorestore существует в целевом расположении hello, можно создать копии (hello две версии одного файла), перезаписать файлы hello в целевом расположении hello или пропустить восстановление hello hello файлов, которые существуют в целевом hello.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-182">If hello file/folder you wish toorestore exists in hello target location, you can create copies (two versions of hello same file), overwrite hello files in hello target location, or skip hello recovery of hello files which exist in hello target.</span></span>
   * <span data-ttu-id="2e7c6-183">Настоятельно рекомендуется оставить параметр по умолчанию hello восстановление списков ACL hello hello файлов, которые восстановлены.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-183">It is highly recommended that you leave hello default option of restoring hello ACLs on hello files which are being recovered.</span></span>
8. <span data-ttu-id="2e7c6-184">Предоставив эти входные данные, нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-184">Once these inputs are provided, click **Next**.</span></span> <span data-ttu-id="2e7c6-185">рабочий процесс восстановления Hello, который восстанавливает машины toothis файлы hello, начнется.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-185">hello recovery workflow, which restores hello files toothis machine, will begin.</span></span>

## <a name="recover-tooan-alternate-machine"></a><span data-ttu-id="2e7c6-186">Восстановление альтернативного машины tooan</span><span class="sxs-lookup"><span data-stu-id="2e7c6-186">Recover tooan alternate machine</span></span>
<span data-ttu-id="2e7c6-187">В случае утери всего сервера по-прежнему можно восстановить данные с другого компьютера tooa резервного копирования Azure.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-187">If your entire server is lost, you can still recover data from Azure Backup tooa different machine.</span></span> <span data-ttu-id="2e7c6-188">Привет, следующие шаги иллюстрируют hello рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-188">hello following steps illustrate hello workflow.</span></span>  

<span data-ttu-id="2e7c6-189">включает Hello терминология, используемая в этом пошаговом руководстве:</span><span class="sxs-lookup"><span data-stu-id="2e7c6-189">hello terminology used in these steps includes:</span></span>

* <span data-ttu-id="2e7c6-190">*Исходный компьютер* — была сделана hello исходной машины, из какой резервный hello и который в данный момент недоступен.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-190">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="2e7c6-191">*Целевой компьютер* — восстанавливаются данные hello toowhich машины hello.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-191">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
* <span data-ttu-id="2e7c6-192">*Образец хранилища* — hello toowhich хранилища резервной копии hello *исходной машины* и *целевой компьютер* зарегистрированы.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-192">*Sample vault* – hello Backup vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="2e7c6-193">Невозможно восстановить резервные копии, созданные с компьютера на компьютере, где выполняется более ранней версии операционной системы hello.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-193">Backups taken from a machine cannot be restored on a machine which is running an earlier version of hello operating system.</span></span> <span data-ttu-id="2e7c6-194">Например, если резервные копии созданы с компьютера под управлением Windows 7, их можно восстановить на компьютер под управлением Windows 8 или более поздних версий ОС,</span><span class="sxs-lookup"><span data-stu-id="2e7c6-194">For example, if backups are taken from a Windows 7 machine, it can be restored on a Windows 8 or above machine.</span></span> <span data-ttu-id="2e7c6-195">Однако hello наоборот не выполняются.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-195">However, hello vice-versa does not hold true.</span></span>
>
>

1. <span data-ttu-id="2e7c6-196">Откройте hello **архивации Microsoft Azure** привязка в на hello *целевой компьютер*.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-196">Open hello **Microsoft Azure Backup** snap in on hello *Target machine*.</span></span>
2. <span data-ttu-id="2e7c6-197">Убедитесь, что hello *целевой компьютер* и hello *исходной машины* являются зарегистрированными toohello же резервного хранилища.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-197">Ensure that hello *Target machine* and hello *Source machine* are registered toohello same backup vault.</span></span>
3. <span data-ttu-id="2e7c6-198">Нажмите кнопку **восстановить данные** рабочего процесса tooinitiate hello.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-198">Click **Recover Data** tooinitiate hello workflow.</span></span>

    ![Восстановить данные](./media/backup-azure-restore-windows-server-classic/recover.png)
4. <span data-ttu-id="2e7c6-200">Выберите **Другой сервер**</span><span class="sxs-lookup"><span data-stu-id="2e7c6-200">Select **Another server**</span></span>

    ![Другой сервер](./media/backup-azure-restore-windows-server-classic/anotherserver.png)
5. <span data-ttu-id="2e7c6-202">Укажите файл hello хранилище учетных данных, который соответствует toohello *хранилище образец*.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-202">Provide hello vault credential file that corresponds toohello *Sample vault*.</span></span> <span data-ttu-id="2e7c6-203">Если hello файл учетных данных хранилища является недопустимым (или истекшим сроком действия) Загрузите новый файл учетных данных хранилища из hello *хранилище образец* в hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-203">If hello vault credential file is invalid (or expired) download a new vault credential file from hello *Sample vault* in hello Azure classic portal.</span></span> <span data-ttu-id="2e7c6-204">Когда предоставляется файл учетных данных хранилища hello, отображается hello резервного хранилища для hello файл учетных данных хранилища.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-204">Once hello vault credential file is provided, hello backup vault against hello vault credential file is displayed.</span></span>
6. <span data-ttu-id="2e7c6-205">Выберите hello *исходной машины* из списка отображаемых машины hello.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-205">Select hello *Source machine* from hello list of displayed machines.</span></span>

    ![Список компьютеров](./media/backup-azure-restore-windows-server-classic/machinelist.png)
7. <span data-ttu-id="2e7c6-207">Выберите либо hello **поиск файлов** или **Обзор файлов** параметр.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-207">Select either hello **Search for files** or **Browse for files** option.</span></span> <span data-ttu-id="2e7c6-208">В целях hello в этом разделе, мы будем использовать hello **поиск файлов** параметр.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-208">For hello purpose of this section, we will use hello **Search for files** option.</span></span>

    ![Поиск](./media/backup-azure-restore-windows-server-classic/search.png)
8. <span data-ttu-id="2e7c6-210">Выберите том hello и дату в следующем экране приветствия.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-210">Select hello volume and date in hello next screen.</span></span> <span data-ttu-id="2e7c6-211">Поиск имени папка или файл hello требуется toorestore.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-211">Search for hello folder/file name you want toorestore.</span></span>

    ![Поиск элементов](./media/backup-azure-restore-windows-server-classic/searchitems.png)
9. <span data-ttu-id="2e7c6-213">Выберите расположение hello, где hello файлы должны toobe восстановлена.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-213">Select hello location where hello files need toobe restored.</span></span>

    ![Расположение для восстанавливаемых данных](./media/backup-azure-restore-windows-server-classic/restorelocation.png)
10. <span data-ttu-id="2e7c6-215">Укажите парольную фразу для шифрования hello, который указывался во *исходной машины* регистрации слишком*образец хранилища*.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-215">Provide hello encryption passphrase that was provided during *Source machine’s* registration too*Sample vault*.</span></span>

    ![Шифрование](./media/backup-azure-restore-windows-server-classic/encryption.png)
11. <span data-ttu-id="2e7c6-217">После ввода приветствия щелкните **восстановить**, который триггеры hello восстановление hello, резервное копирование toohello файлы путь назначения, указанный.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-217">Once hello input is provided, click **Recover**, which triggers hello restore of hello backed up files toohello destination provided.</span></span>

## <a name="use-instant-restore-toorestore-data-tooan-alternate-machine"></a><span data-ttu-id="2e7c6-218">Использовать мгновенное восстановление toorestore данных tooan альтернативный компьютер</span><span class="sxs-lookup"><span data-stu-id="2e7c6-218">Use Instant Restore toorestore data tooan alternate machine</span></span>
<span data-ttu-id="2e7c6-219">В случае утери всего сервера по-прежнему можно восстановить данные с другого компьютера tooa резервного копирования Azure.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-219">If your entire server is lost, you can still recover data from Azure Backup tooa different machine.</span></span> <span data-ttu-id="2e7c6-220">Привет, следующие шаги иллюстрируют hello рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-220">hello following steps illustrate hello workflow.</span></span>

<span data-ttu-id="2e7c6-221">включает Hello терминология, используемая в этом пошаговом руководстве:</span><span class="sxs-lookup"><span data-stu-id="2e7c6-221">hello terminology used in these steps includes:</span></span>

* <span data-ttu-id="2e7c6-222">*Исходный компьютер* — была сделана hello исходной машины, из какой резервный hello и который в данный момент недоступен.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-222">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="2e7c6-223">*Целевой компьютер* — восстанавливаются данные hello toowhich машины hello.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-223">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
* <span data-ttu-id="2e7c6-224">*Образец хранилища* — hello toowhich хранилище служб восстановления hello *исходной машины* и *целевой компьютер* зарегистрированы.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-224">*Sample vault* – hello Recovery Services vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="2e7c6-225">Резервные копии, не может быть восстановленной tooa целевой компьютер под управлением более ранней версии операционной системы hello.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-225">Backups can't be restored tooa target machine running an earlier version of hello operating system.</span></span> <span data-ttu-id="2e7c6-226">Например, резервную копию, созданную на компьютере Windows 7, можно восстановить на компьютере под управлением Windows 8 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-226">For example, a backup taken from a Windows 7 computer can be restored on a Windows 8, or later, computer.</span></span> <span data-ttu-id="2e7c6-227">Создание резервных копий с компьютера Windows 8, не может быть компьютер восстановленной tooa Windows 7.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-227">A backup taken from a Windows 8 computer cannot be restored tooa Windows 7 computer.</span></span>
>
>

1. <span data-ttu-id="2e7c6-228">Откройте hello **архивации Microsoft Azure** привязка в на hello *целевой компьютер*.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-228">Open hello **Microsoft Azure Backup** snap in on hello *Target machine*.</span></span>

2. <span data-ttu-id="2e7c6-229">Обеспечить hello *целевой компьютер* и hello *исходной машины* , зарегистрированных toohello же восстановления службы в хранилище.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-229">Ensure hello *Target machine* and hello *Source machine* are registered toohello same Recovery Services vault.</span></span>

3. <span data-ttu-id="2e7c6-230">Нажмите кнопку **восстановить данные** tooopen hello **мастер восстановления данных**.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-230">Click **Recover Data** tooopen hello **Recover Data wizard**.</span></span>

    ![Восстановить данные](./media/backup-azure-restore-windows-server/recover.png)

4. <span data-ttu-id="2e7c6-232">На hello **Приступая к работе** выберите **другой сервер**</span><span class="sxs-lookup"><span data-stu-id="2e7c6-232">On hello **Getting Started** pane, select **Another server**</span></span>

    ![Другой сервер](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. <span data-ttu-id="2e7c6-234">Укажите файл hello хранилище учетных данных, который соответствует toohello *хранилище образец*и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-234">Provide hello vault credential file that corresponds toohello *Sample vault*, and click **Next**.</span></span>

    <span data-ttu-id="2e7c6-235">Если файл учетных данных хранилища hello является недопустимым (или истекшим сроком действия), загрузите новый файл учетных данных хранилища из hello *хранилище образец* в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-235">If hello vault credential file is invalid (or expired), download a new vault credential file from hello *Sample vault* in hello Azure portal.</span></span> <span data-ttu-id="2e7c6-236">После предоставления учетных данных хранилища допустимым появится имя hello hello соответствующего резервного хранилища.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-236">Once you provide a valid vault credential, hello name of hello corresponding Backup Vault appears.</span></span>

6. <span data-ttu-id="2e7c6-237">На hello **выберите резервный сервер** области, выберите hello *исходной машины* из списка отображаемых машины hello и предоставить hello парольную фразу.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-237">On hello **Select Backup Server** pane, select hello *Source machine* from hello list of displayed machines and provide hello passphrase.</span></span> <span data-ttu-id="2e7c6-238">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-238">Then click **Next**.</span></span>

    ![Список компьютеров](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. <span data-ttu-id="2e7c6-240">На hello **выберите режим восстановления** выберите **отдельные файлы и папки** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-240">On hello **Select Recovery Mode** pane, select **Individual files and folders** and click **Next**.</span></span>

    ![Поиск](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. <span data-ttu-id="2e7c6-242">На hello **выберите том и дату** области, выберите hello томов, которые содержат hello файлы и папки, которые вы хотите toorestore.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-242">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="2e7c6-243">Hello календаре выберите точку восстановления.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-243">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="2e7c6-244">Можно восстановить данные на любой момент времени.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-244">You can restore from any recovery point in time.</span></span> <span data-ttu-id="2e7c6-245">Даты в **полужирным** указать hello доступность по крайней мере одна точка восстановления.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-245">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="2e7c6-246">После выбора даты, если доступны несколько точек восстановления, выберите hello конкретную точку восстановления из hello **время** раскрывающееся меню.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-246">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Поиск элементов](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. <span data-ttu-id="2e7c6-248">Нажмите кнопку **подключить** toolocally точки восстановления hello подключения как тома для восстановления на ваш *целевой компьютер*.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-248">Click **Mount** toolocally mount hello recovery point as a recovery volume on your *Target machine*.</span></span>

10. <span data-ttu-id="2e7c6-249">На hello **обзора и восстанавливать файлы** области, нажмите кнопку **Обзор** tooopen проводника поиска hello файлы и папки требуется.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-249">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![Шифрование](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. <span data-ttu-id="2e7c6-251">В проводнике Windows, скопируйте hello файлов и папок из тома для восстановления hello и вставьте их tooyour *целевой компьютер* расположение.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-251">In Windows Explorer, copy hello files and/or folders from hello recovery volume and paste them tooyour *Target machine* location.</span></span> <span data-ttu-id="2e7c6-252">Можно открыть или поток файлов hello непосредственно из тома для восстановления hello и проверить hello правильных версий восстанавливаются.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-252">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![Шифрование](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. <span data-ttu-id="2e7c6-254">После завершения восстановления hello файлы и папки на hello **обзора и файлов восстановления** области, нажмите кнопку **Unmount**.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-254">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="2e7c6-255">Нажмите кнопку **Да** tooconfirm, что требуется toounmount hello тома.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-255">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![Шифрование](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="2e7c6-257">Если не щелкнуть Unmount, hello тома для восстановления останется подключенного шесть часов с момента hello, когда он был подключен.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-257">If you do not click Unmount, hello Recovery Volume will remain mounted for six hours from hello time when it was mounted.</span></span> <span data-ttu-id="2e7c6-258">Операции резервного копирования будет выполняться во время монтирования тома hello.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-258">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="2e7c6-259">Toorun все запланированные операции резервного копирования во время hello при монтировании тома hello будет выполняться после восстановления тома hello в отключены.</span><span class="sxs-lookup"><span data-stu-id="2e7c6-259">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >


## <a name="next-steps"></a><span data-ttu-id="2e7c6-260">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2e7c6-260">Next steps</span></span>
* [<span data-ttu-id="2e7c6-261">Часто задаваемые вопросы о службе архивации Azure</span><span class="sxs-lookup"><span data-stu-id="2e7c6-261">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
* <span data-ttu-id="2e7c6-262">Посетите hello [форуме резервного копирования Azure](http://go.microsoft.com/fwlink/p/?LinkId=290933).</span><span class="sxs-lookup"><span data-stu-id="2e7c6-262">Visit hello [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933).</span></span>

## <a name="learn-more"></a><span data-ttu-id="2e7c6-263">Подробнее</span><span class="sxs-lookup"><span data-stu-id="2e7c6-263">Learn more</span></span>
* [<span data-ttu-id="2e7c6-264">Обзор службы архивации Azure</span><span class="sxs-lookup"><span data-stu-id="2e7c6-264">Azure Backup Overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=222425)
* [<span data-ttu-id="2e7c6-265">Резервное копирование виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="2e7c6-265">Backup Azure virtual machines</span></span>](backup-azure-vms-introduction.md)
* [<span data-ttu-id="2e7c6-266">Резервное копирование рабочих нагрузок Майкрософт</span><span class="sxs-lookup"><span data-stu-id="2e7c6-266">Backup up Microsoft workloads</span></span>](backup-azure-dpm-introduction.md)
