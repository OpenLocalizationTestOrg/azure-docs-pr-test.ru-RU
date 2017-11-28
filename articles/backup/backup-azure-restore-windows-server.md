---
title: "aaaRestore данные в Azure tooa Windows Server или Windows | Документы Microsoft"
description: "Узнайте, toorestore хранения в Azure tooa Windows Server или Windows."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 742f4b9e-c0ab-4eeb-8e22-ee29b83c22c4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/16/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 11335495e448986a74f1733406f87e04331641d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="restore-files-tooa-windows-server-or-windows-client-machine-using-resource-manager-deployment-model"></a><span data-ttu-id="0aa19-103">Восстановить файлы tooa Windows server и клиентским компьютером Windows, с помощью модели развертывания диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="0aa19-103">Restore files tooa Windows server or Windows client machine using Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0aa19-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="0aa19-104">Azure portal</span></span>](backup-azure-restore-windows-server.md)
> * [<span data-ttu-id="0aa19-105">Классический портал.</span><span class="sxs-lookup"><span data-stu-id="0aa19-105">Classic portal</span></span>](backup-azure-restore-windows-server-classic.md)
>
>

<span data-ttu-id="0aa19-106">В этой статье объясняется, как данные toorestore из резервного хранилища.</span><span class="sxs-lookup"><span data-stu-id="0aa19-106">This article explains how toorestore data from a backup vault.</span></span> <span data-ttu-id="0aa19-107">toorestore данных, используется мастер восстановления данных hello hello агента служб восстановления Microsoft Azure (режим MARS).</span><span class="sxs-lookup"><span data-stu-id="0aa19-107">toorestore data, you use hello Recover Data wizard in hello Microsoft Azure Recovery Services (MARS) agent.</span></span> <span data-ttu-id="0aa19-108">При восстановлении данных можно использовать следующие возможности.</span><span class="sxs-lookup"><span data-stu-id="0aa19-108">When you restore data, it is possible to:</span></span>

* <span data-ttu-id="0aa19-109">Восстановление данных toohello же машину из какие резервные копии hello были выполнены.</span><span class="sxs-lookup"><span data-stu-id="0aa19-109">Restore data toohello same machine from which hello backups were taken.</span></span>
* <span data-ttu-id="0aa19-110">Восстановление данных tooan альтернативный машины.</span><span class="sxs-lookup"><span data-stu-id="0aa19-110">Restore data tooan alternate machine.</span></span>

<span data-ttu-id="0aa19-111">В января 2017 г. Корпорация Майкрософт выпустила агент предварительной версии обновления toohello режима MARS.</span><span class="sxs-lookup"><span data-stu-id="0aa19-111">In January 2017, Microsoft released a Preview update toohello MARS agent.</span></span> <span data-ttu-id="0aa19-112">Вместе с исправления ошибок это обновление позволяет мгновенное восстановление, позволяющий toomount моментальный снимок точки восстановления для записи в качестве тома для восстановления.</span><span class="sxs-lookup"><span data-stu-id="0aa19-112">Along with bug fixes, this update enables Instant Restore, which allows you toomount a writeable recovery point snapshot as a recovery volume.</span></span> <span data-ttu-id="0aa19-113">Затем можно исследовать hello восстановления тома и скопируйте файлы tooa локального компьютера выборочно тем самым восстановление файлов.</span><span class="sxs-lookup"><span data-stu-id="0aa19-113">You can then explore hello recovery volume and copy files tooa local computer thereby selectively restoring files.</span></span>

> [!NOTE]
> <span data-ttu-id="0aa19-114">Hello [января 2017 г. обновление резервного копирования Azure](https://support.microsoft.com/en-us/help/3216528?preview) является обязательным, если вы хотите toouse мгновенное восстановление toorestore данные.</span><span class="sxs-lookup"><span data-stu-id="0aa19-114">hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is required if you want toouse Instant Restore toorestore data.</span></span> <span data-ttu-id="0aa19-115">Также в хранилищах в регионах, перечисленных в статье поддержка hello, должны быть защищены hello резервных копий данных.</span><span class="sxs-lookup"><span data-stu-id="0aa19-115">Also hello backup data must be protected in vaults in locales listed in hello support article.</span></span> <span data-ttu-id="0aa19-116">Обратитесь к hello [января 2017 г. обновление резервного копирования Azure](https://support.microsoft.com/en-us/help/3216528?preview) для hello последний список языков, поддерживающих мгновенное восстановление.</span><span class="sxs-lookup"><span data-stu-id="0aa19-116">Consult hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) for hello latest list of locales that support Instant Restore.</span></span> <span data-ttu-id="0aa19-117">Сейчас мгновенное восстановление доступно **не во всех** регионах.</span><span class="sxs-lookup"><span data-stu-id="0aa19-117">Instant Restore is **not** currently available in all locales.</span></span>
>

<span data-ttu-id="0aa19-118">Мгновенное восстановление доступно для использования в хранилищах службы восстановления в hello портал Azure и хранилищ архивации hello классического портала.</span><span class="sxs-lookup"><span data-stu-id="0aa19-118">Instant Restore is available for use in Recovery Services vaults in hello Azure portal and Backup vaults in hello classic portal.</span></span> <span data-ttu-id="0aa19-119">Мгновенное восстановление toouse следует загрузить обновление MARS hello и следуйте процедурам hello с упоминанием мгновенное восстановление.</span><span class="sxs-lookup"><span data-stu-id="0aa19-119">If you want toouse Instant Restore, download hello MARS update, and follow hello procedures that mention Instant Restore.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="use-instant-restore-toorecover-data-toohello-same-machine"></a><span data-ttu-id="0aa19-120">Используйте мгновенное восстановление данных toohello toorecover компьютере</span><span class="sxs-lookup"><span data-stu-id="0aa19-120">Use Instant Restore toorecover data toohello same machine</span></span>

<span data-ttu-id="0aa19-121">Если случайно удален файл и пожеланий toorestore его toohello, на одном компьютере (с какой hello резервная копия), hello следующие шаги помогут вам восстановить данные hello.</span><span class="sxs-lookup"><span data-stu-id="0aa19-121">If you accidentally deleted a file and wish toorestore it toohello same machine (from which hello backup is taken), hello following steps will help you recover hello data.</span></span>

1. <span data-ttu-id="0aa19-122">Откройте hello **архивации Microsoft Azure** привязка в.</span><span class="sxs-lookup"><span data-stu-id="0aa19-122">Open hello **Microsoft Azure Backup** snap in.</span></span> <span data-ttu-id="0aa19-123">Если вы не знаете, где установлена оснастка hello в, поиск hello компьютере или сервере **архивации Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="0aa19-123">If you don't know where hello snap in was installed, search hello computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="0aa19-124">Настольные приложения Hello должны отображаться в результатах поиска hello.</span><span class="sxs-lookup"><span data-stu-id="0aa19-124">hello desktop app should appear in hello search results.</span></span>

2. <span data-ttu-id="0aa19-125">Нажмите кнопку **восстановить данные** toostart приветствия мастера.</span><span class="sxs-lookup"><span data-stu-id="0aa19-125">Click **Recover Data** toostart hello wizard.</span></span>

    ![Восстановить данные](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="0aa19-127">На hello **Приступая к работе** области, toohello данных hello toorestore того же сервера или компьютера, выберите **этим сервером (`<server name>`)** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="0aa19-127">On hello **Getting Started** pane, toorestore hello data toohello same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Выберите этот сервер toohello параметр toorestore hello данных того же компьютера](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. <span data-ttu-id="0aa19-129">На hello **выберите режим восстановления** области, выберите **отдельные файлы и папки** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="0aa19-129">On hello **Select Recovery Mode** pane, choose **Individual files and folders** and then click **Next**.</span></span>

    ![Обзор файлов](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. <span data-ttu-id="0aa19-131">На hello **выберите том и дату** области, выберите hello томов, которые содержат hello файлы и папки, которые вы хотите toorestore.</span><span class="sxs-lookup"><span data-stu-id="0aa19-131">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="0aa19-132">Hello календаре выберите точку восстановления.</span><span class="sxs-lookup"><span data-stu-id="0aa19-132">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="0aa19-133">Можно восстановить данные на любой момент времени.</span><span class="sxs-lookup"><span data-stu-id="0aa19-133">You can restore from any recovery point in time.</span></span> <span data-ttu-id="0aa19-134">Даты в **полужирным** указать hello доступность по крайней мере одна точка восстановления.</span><span class="sxs-lookup"><span data-stu-id="0aa19-134">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="0aa19-135">После выбора даты, если доступны несколько точек восстановления, выберите hello конкретную точку восстановления из hello **время** раскрывающееся меню.</span><span class="sxs-lookup"><span data-stu-id="0aa19-135">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Том и дата](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. <span data-ttu-id="0aa19-137">После выбора toorestore точки восстановления hello щелкните **подключить**.</span><span class="sxs-lookup"><span data-stu-id="0aa19-137">Once you have chosen hello recovery point toorestore, click **Mount**.</span></span>

    <span data-ttu-id="0aa19-138">Резервное копирование Azure подключает точку локального восстановления hello и использует его в качестве тома для восстановления.</span><span class="sxs-lookup"><span data-stu-id="0aa19-138">Azure Backup mounts hello local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="0aa19-139">На hello **обзора и восстанавливать файлы** области, нажмите кнопку **Обзор** tooopen проводника поиска hello файлы и папки требуется.</span><span class="sxs-lookup"><span data-stu-id="0aa19-139">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![Варианты восстановления](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. <span data-ttu-id="0aa19-141">В проводнике Windows, hello копировать файлы или папки toorestore и вставить их tooany расположение toohello на локальном сервере или компьютере.</span><span class="sxs-lookup"><span data-stu-id="0aa19-141">In Windows Explorer, copy hello files and/or folders you want toorestore and paste them tooany location local toohello server or computer.</span></span> <span data-ttu-id="0aa19-142">Можно открыть или поток файлов hello непосредственно из тома для восстановления hello и проверить hello правильных версий восстанавливаются.</span><span class="sxs-lookup"><span data-stu-id="0aa19-142">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![Скопируйте и вставьте файлы и папки из расположения toolocal подключенный том](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. <span data-ttu-id="0aa19-144">После завершения восстановления hello файлы и папки на hello **обзора и файлов восстановления** области, нажмите кнопку **Unmount**.</span><span class="sxs-lookup"><span data-stu-id="0aa19-144">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="0aa19-145">Нажмите кнопку **Да** tooconfirm, что требуется toounmount hello тома.</span><span class="sxs-lookup"><span data-stu-id="0aa19-145">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![Отсоединить том hello и подтвердите](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="0aa19-147">Если не щелкнуть Unmount, hello тома для восстановления останется подключенного на 6 часов с момента hello, когда он был подключен.</span><span class="sxs-lookup"><span data-stu-id="0aa19-147">If you do not click Unmount, hello Recovery Volume will remain mounted for 6 hours from hello time when it was mounted.</span></span> <span data-ttu-id="0aa19-148">Время подключения hello то, расширенного до максимального значения 24 часа в случае текущей копии файла.</span><span class="sxs-lookup"><span data-stu-id="0aa19-148">However, hello mount time is extended upto a maximum of 24 hours in case of an ongoing file-copy.</span></span> <span data-ttu-id="0aa19-149">Операции резервного копирования будет выполняться во время монтирования тома hello.</span><span class="sxs-lookup"><span data-stu-id="0aa19-149">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="0aa19-150">Toorun все запланированные операции резервного копирования во время hello при монтировании тома hello будет выполняться после восстановления тома hello в отключены.</span><span class="sxs-lookup"><span data-stu-id="0aa19-150">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >


## <a name="use-instant-restore-toorestore-data-tooan-alternate-machine"></a><span data-ttu-id="0aa19-151">Использовать мгновенное восстановление toorestore данных tooan альтернативный компьютер</span><span class="sxs-lookup"><span data-stu-id="0aa19-151">Use Instant Restore toorestore data tooan alternate machine</span></span>
<span data-ttu-id="0aa19-152">В случае утери всего сервера по-прежнему можно восстановить данные с другого компьютера tooa резервного копирования Azure.</span><span class="sxs-lookup"><span data-stu-id="0aa19-152">If your entire server is lost, you can still recover data from Azure Backup tooa different machine.</span></span> <span data-ttu-id="0aa19-153">Привет, следующие шаги иллюстрируют hello рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="0aa19-153">hello following steps illustrate hello workflow.</span></span>


<span data-ttu-id="0aa19-154">включает Hello терминология, используемая в этом пошаговом руководстве:</span><span class="sxs-lookup"><span data-stu-id="0aa19-154">hello terminology used in these steps includes:</span></span>

* <span data-ttu-id="0aa19-155">*Исходный компьютер* — была сделана hello исходной машины, из какой резервный hello и который в данный момент недоступен.</span><span class="sxs-lookup"><span data-stu-id="0aa19-155">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="0aa19-156">*Целевой компьютер* — восстанавливаются данные hello toowhich машины hello.</span><span class="sxs-lookup"><span data-stu-id="0aa19-156">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
* <span data-ttu-id="0aa19-157">*Образец хранилища* — hello toowhich хранилище служб восстановления hello *исходной машины* и *целевой компьютер* зарегистрированы.</span><span class="sxs-lookup"><span data-stu-id="0aa19-157">*Sample vault* – hello Recovery Services vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="0aa19-158">Резервные копии, не может быть восстановленной tooa целевой компьютер под управлением более ранней версии операционной системы hello.</span><span class="sxs-lookup"><span data-stu-id="0aa19-158">Backups can't be restored tooa target machine running an earlier version of hello operating system.</span></span> <span data-ttu-id="0aa19-159">Например, резервную копию, созданную на компьютере Windows 7, можно восстановить на компьютере под управлением Windows 8 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="0aa19-159">For example, a backup taken from a Windows 7 computer can be restored on a Windows 8, or later, computer.</span></span> <span data-ttu-id="0aa19-160">Создание резервных копий с компьютера Windows 8, не может быть компьютер восстановленной tooa Windows 7.</span><span class="sxs-lookup"><span data-stu-id="0aa19-160">A backup taken from a Windows 8 computer cannot be restored tooa Windows 7 computer.</span></span>
>
>

1. <span data-ttu-id="0aa19-161">Откройте hello **архивации Microsoft Azure** привязка в на hello *целевой компьютер*.</span><span class="sxs-lookup"><span data-stu-id="0aa19-161">Open hello **Microsoft Azure Backup** snap in on hello *Target machine*.</span></span>

2. <span data-ttu-id="0aa19-162">Обеспечить hello *целевой компьютер* и hello *исходной машины* , зарегистрированных toohello же восстановления службы в хранилище.</span><span class="sxs-lookup"><span data-stu-id="0aa19-162">Ensure hello *Target machine* and hello *Source machine* are registered toohello same Recovery Services vault.</span></span>

3. <span data-ttu-id="0aa19-163">Нажмите кнопку **восстановить данные** tooopen hello **мастер восстановления данных**.</span><span class="sxs-lookup"><span data-stu-id="0aa19-163">Click **Recover Data** tooopen hello **Recover Data wizard**.</span></span>

    ![Восстановить данные](./media/backup-azure-restore-windows-server/recover.png)

4. <span data-ttu-id="0aa19-165">На hello **Приступая к работе** выберите **другой сервер**</span><span class="sxs-lookup"><span data-stu-id="0aa19-165">On hello **Getting Started** pane, select **Another server**</span></span>

    ![Другой сервер](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. <span data-ttu-id="0aa19-167">Укажите файл hello хранилище учетных данных, который соответствует toohello *хранилище образец*и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="0aa19-167">Provide hello vault credential file that corresponds toohello *Sample vault*, and click **Next**.</span></span>

    <span data-ttu-id="0aa19-168">Если файл учетных данных хранилища hello является недопустимым (или истекшим сроком действия), загрузите новый файл учетных данных хранилища из hello *хранилище образец* в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="0aa19-168">If hello vault credential file is invalid (or expired), download a new vault credential file from hello *Sample vault* in hello Azure portal.</span></span> <span data-ttu-id="0aa19-169">После предоставления учетных данных хранилища допустимым появится имя hello hello соответствующего резервного хранилища.</span><span class="sxs-lookup"><span data-stu-id="0aa19-169">Once you provide a valid vault credential, hello name of hello corresponding Backup Vault appears.</span></span>


6. <span data-ttu-id="0aa19-170">На hello **выберите резервный сервер** области, выберите hello *исходной машины* из списка отображаемых машины hello и предоставить hello парольную фразу.</span><span class="sxs-lookup"><span data-stu-id="0aa19-170">On hello **Select Backup Server** pane, select hello *Source machine* from hello list of displayed machines and provide hello passphrase.</span></span> <span data-ttu-id="0aa19-171">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="0aa19-171">Then click **Next**.</span></span>

    ![Список компьютеров](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. <span data-ttu-id="0aa19-173">На hello **выберите режим восстановления** выберите **отдельные файлы и папки** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="0aa19-173">On hello **Select Recovery Mode** pane, select **Individual files and folders** and click **Next**.</span></span>

    ![Поиск](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. <span data-ttu-id="0aa19-175">На hello **выберите том и дату** области, выберите hello томов, которые содержат hello файлы и папки, которые вы хотите toorestore.</span><span class="sxs-lookup"><span data-stu-id="0aa19-175">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="0aa19-176">Hello календаре выберите точку восстановления.</span><span class="sxs-lookup"><span data-stu-id="0aa19-176">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="0aa19-177">Можно восстановить данные на любой момент времени.</span><span class="sxs-lookup"><span data-stu-id="0aa19-177">You can restore from any recovery point in time.</span></span> <span data-ttu-id="0aa19-178">Даты в **полужирным** указать hello доступность по крайней мере одна точка восстановления.</span><span class="sxs-lookup"><span data-stu-id="0aa19-178">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="0aa19-179">После выбора даты, если доступны несколько точек восстановления, выберите hello конкретную точку восстановления из hello **время** раскрывающееся меню.</span><span class="sxs-lookup"><span data-stu-id="0aa19-179">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Поиск элементов](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. <span data-ttu-id="0aa19-181">Нажмите кнопку **подключить** toolocally точки восстановления hello подключения как тома для восстановления на ваш *целевой компьютер*.</span><span class="sxs-lookup"><span data-stu-id="0aa19-181">Click **Mount** toolocally mount hello recovery point as a recovery volume on your *Target machine*.</span></span>

10. <span data-ttu-id="0aa19-182">На hello **обзора и восстанавливать файлы** области, нажмите кнопку **Обзор** tooopen проводника поиска hello файлы и папки требуется.</span><span class="sxs-lookup"><span data-stu-id="0aa19-182">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![Шифрование](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. <span data-ttu-id="0aa19-184">В проводнике Windows, скопируйте hello файлов и папок из тома для восстановления hello и вставьте их tooyour *целевой компьютер* расположение.</span><span class="sxs-lookup"><span data-stu-id="0aa19-184">In Windows Explorer, copy hello files and/or folders from hello recovery volume and paste them tooyour *Target machine* location.</span></span> <span data-ttu-id="0aa19-185">Можно открыть или поток файлов hello непосредственно из тома для восстановления hello и проверить hello правильных версий восстанавливаются.</span><span class="sxs-lookup"><span data-stu-id="0aa19-185">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![Шифрование](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. <span data-ttu-id="0aa19-187">После завершения восстановления hello файлы и папки на hello **обзора и файлов восстановления** области, нажмите кнопку **Unmount**.</span><span class="sxs-lookup"><span data-stu-id="0aa19-187">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="0aa19-188">Нажмите кнопку **Да** tooconfirm, что требуется toounmount hello тома.</span><span class="sxs-lookup"><span data-stu-id="0aa19-188">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![Шифрование](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="0aa19-190">Если не щелкнуть Unmount, hello тома для восстановления останется подключенного на 6 часов с момента hello, когда он был подключен.</span><span class="sxs-lookup"><span data-stu-id="0aa19-190">If you do not click Unmount, hello Recovery Volume will remain mounted for 6 hours from hello time when it was mounted.</span></span> <span data-ttu-id="0aa19-191">Время подключения hello то, расширенного до максимального значения 24 часа в случае текущей копии файла.</span><span class="sxs-lookup"><span data-stu-id="0aa19-191">However, hello mount time is extended upto a maximum of 24 hours in case of an ongoing file-copy.</span></span> <span data-ttu-id="0aa19-192">Операции резервного копирования будет выполняться во время монтирования тома hello.</span><span class="sxs-lookup"><span data-stu-id="0aa19-192">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="0aa19-193">Toorun все запланированные операции резервного копирования во время hello при монтировании тома hello будет выполняться после восстановления тома hello в отключены.</span><span class="sxs-lookup"><span data-stu-id="0aa19-193">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >

## <a name="troubleshooting"></a><span data-ttu-id="0aa19-194">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="0aa19-194">Troubleshooting</span></span>
<span data-ttu-id="0aa19-195">Если Azure Backup не подключаются тома для восстановления hello даже через несколько минут, выбор команды **подключить** или завершается с ошибкой toomount hello восстановленного тома с ошибками, выполните действия hello ниже toobegin восстановление обычно.</span><span class="sxs-lookup"><span data-stu-id="0aa19-195">If Azure Backup does not successfully mount hello recovery volume even after several minutes of clicking **Mount** or fails toomount hello recovery volume with one or more errors, follow hello steps below toobegin recovering normally.</span></span>

1.  <span data-ttu-id="0aa19-196">Отмените процесс hello текущего подключения в случае его выполнения в течение нескольких минут.</span><span class="sxs-lookup"><span data-stu-id="0aa19-196">Cancel hello ongoing mount process in case it has been running for several minutes.</span></span>

2.  <span data-ttu-id="0aa19-197">Убедитесь, что находитесь на последнюю версию агента резервного копирования Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="0aa19-197">Ensure that you are on hello latest version of hello Azure Backup agent.</span></span> <span data-ttu-id="0aa19-198">toofind сведения hello версия агента резервного копирования Azure, щелкните на **о Azure агента служб восстановления Microsoft** на hello **действия** области архивации Microsoft Azure консоли и убедитесь, что hello  **Версия** число — равно tooor выше, чем версия hello, упомянутые в [в этой статье](https://go.microsoft.com/fwlink/?linkid=229525).</span><span class="sxs-lookup"><span data-stu-id="0aa19-198">toofind out hello version information of Azure Backup agent, click on **About Microsoft Azure Recovery Services Agent** on hello **Actions** pane of Microsoft Azure Backup console and ensure that hello **Version** number is equal tooor higher than hello version mentioned in [this article](https://go.microsoft.com/fwlink/?linkid=229525).</span></span> <span data-ttu-id="0aa19-199">Можно загрузить последнюю версию hello с [здесь](https://go.microsoft.com/fwLink/?LinkID=288905)</span><span class="sxs-lookup"><span data-stu-id="0aa19-199">You can download hello latest version from [here](https://go.microsoft.com/fwLink/?LinkID=288905)</span></span>

3.  <span data-ttu-id="0aa19-200">Go слишком**диспетчер устройств** -> **контроллеров запоминающих устройств** и убедиться, что можно найти **инициатора iSCSI (Майкрософт)**.</span><span class="sxs-lookup"><span data-stu-id="0aa19-200">Go too**Device Manager** -> **Storage Controllers** and ensure that you can locate **Microsoft iSCSI Initiator**.</span></span> <span data-ttu-id="0aa19-201">Если его можно найти, напрямую перейти toostep ниже 7.</span><span class="sxs-lookup"><span data-stu-id="0aa19-201">If you can locate it, directly go toostep 7 below.</span></span> 

4.  <span data-ttu-id="0aa19-202">Если не удается найти службу инициатора Microsoft iSCSI, как указано в шаге 3, проверьте toosee можно найти запись в списке **диспетчер устройств** -> **контроллеров запоминающих устройств** вызывается  **Неизвестное устройство** с Идентификатором оборудования **ROOT\ISCSIPRT**.</span><span class="sxs-lookup"><span data-stu-id="0aa19-202">If you cannot locate Microsoft iSCSI Initiator service as mentioned in step 3, check toosee if you can find an entry under **Device Manager** -> **Storage Controllers** called **Unknown Device** with Hardware ID **ROOT\ISCSIPRT**.</span></span>

5.  <span data-ttu-id="0aa19-203">Щелкните правой кнопкой мыши **Неизвестное устройство** и выберите команду **Обновить драйверы**.</span><span class="sxs-lookup"><span data-stu-id="0aa19-203">Right click on **Unknown Device** and select **Update Driver Software**.</span></span>

6.  <span data-ttu-id="0aa19-204">Обновить драйвер hello, выбрав параметр hello слишком **автоматический поиск обновленных драйверов**.</span><span class="sxs-lookup"><span data-stu-id="0aa19-204">Update hello driver by selecting hello option too **Search automatically for updated driver software**.</span></span> <span data-ttu-id="0aa19-205">Завершение обновления hello следует изменить **неизвестного устройства** слишком**инициатора iSCSI (Майкрософт)** как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="0aa19-205">Completion of hello update should change **Unknown Device** too**Microsoft iSCSI Initiator** as shown below.</span></span> 

    ![Шифрование](./media/backup-azure-restore-windows-server/UnknowniSCSIDevice.png)

7.  <span data-ttu-id="0aa19-207">Go слишком**диспетчер задач** -> **службы (локальные)** -> **службу инициатора Microsoft iSCSI**.</span><span class="sxs-lookup"><span data-stu-id="0aa19-207">Go too**Task Manager** -> **Services (Local)** -> **Microsoft iSCSI Initiator Service**.</span></span> 

    ![Шифрование](./media/backup-azure-restore-windows-server/MicrosoftInitiatorServiceRunning.png)
    
8.  <span data-ttu-id="0aa19-209">Перезапустите службы инициатора iSCSI Microsoft hello, щелкнув службу hello, щелкнув **остановить** и Далее, щелкните правой кнопкой мыши еще раз и щелкнув **запустить**.</span><span class="sxs-lookup"><span data-stu-id="0aa19-209">Restart hello Microsoft iSCSI Initiator service by right-clicking on hello service, clicking on **Stop** and further right clicking again and clicking on **Start**.</span></span>

9.  <span data-ttu-id="0aa19-210">Повторите восстановление с помощью мгновенного восстановления.</span><span class="sxs-lookup"><span data-stu-id="0aa19-210">Retry recovering using Instant Restore.</span></span> 

<span data-ttu-id="0aa19-211">Если hello восстановления по-прежнему не удается, перезагрузите сервер и клиент.</span><span class="sxs-lookup"><span data-stu-id="0aa19-211">If hello recovery still fails, reboot your server/client.</span></span> <span data-ttu-id="0aa19-212">Если нежелательно перезагрузки или hello восстановления по-прежнему не даже после перезагрузки сервера hello, попробуйте восстановить из альтернативного машины и обратитесь в службу поддержки Azure, перейдя слишком[портала Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) и отправка запроса на техническую поддержку.</span><span class="sxs-lookup"><span data-stu-id="0aa19-212">If a reboot is not desirable or hello recovery still fails even after rebooting hello server, try recovering from an Alternate Machine, and contact Azure Support by going too[Azure Portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and submitting a support request.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0aa19-213">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0aa19-213">Next steps</span></span>
* <span data-ttu-id="0aa19-214">Теперь после восстановления файлов и папок можно [управлять резервными копиями](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="0aa19-214">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span></span>
