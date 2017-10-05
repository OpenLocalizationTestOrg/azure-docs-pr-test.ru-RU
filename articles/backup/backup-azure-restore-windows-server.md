---
title: "Восстановление данных из Azure на сервер Windows Server или компьютер Windows | Документация Майкрософт"
description: "Узнайте, как восстановить данные из Azure на сервер Windows Server или компьютер Windows."
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
ms.openlocfilehash: 231dd61f95267b3a504ed70e9b3a5abc470b69b2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="restore-files-to-a-windows-server-or-windows-client-machine-using-resource-manager-deployment-model"></a><span data-ttu-id="89bd2-103">Восстановление файлов на сервере Windows Server или клиентском компьютере Windows с помощью модели развертывания Resource Manager</span><span class="sxs-lookup"><span data-stu-id="89bd2-103">Restore files to a Windows server or Windows client machine using Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="89bd2-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="89bd2-104">Azure portal</span></span>](backup-azure-restore-windows-server.md)
> * [<span data-ttu-id="89bd2-105">Классический портал.</span><span class="sxs-lookup"><span data-stu-id="89bd2-105">Classic portal</span></span>](backup-azure-restore-windows-server-classic.md)
>
>

<span data-ttu-id="89bd2-106">В этой статье описывается процесс восстановления данных из хранилища службы архивации.</span><span class="sxs-lookup"><span data-stu-id="89bd2-106">This article explains how to restore data from a backup vault.</span></span> <span data-ttu-id="89bd2-107">Чтобы восстановить данные, используйте мастер восстановления данных, доступный в агенте служб восстановления Microsoft Azure (MARS).</span><span class="sxs-lookup"><span data-stu-id="89bd2-107">To restore data, you use the Recover Data wizard in the Microsoft Azure Recovery Services (MARS) agent.</span></span> <span data-ttu-id="89bd2-108">При восстановлении данных можно использовать следующие возможности.</span><span class="sxs-lookup"><span data-stu-id="89bd2-108">When you restore data, it is possible to:</span></span>

* <span data-ttu-id="89bd2-109">Восстановление данных на тот же компьютер, с которого создавались резервные копии.</span><span class="sxs-lookup"><span data-stu-id="89bd2-109">Restore data to the same machine from which the backups were taken.</span></span>
* <span data-ttu-id="89bd2-110">Восстановление файлов на другой компьютер.</span><span class="sxs-lookup"><span data-stu-id="89bd2-110">Restore data to an alternate machine.</span></span>

<span data-ttu-id="89bd2-111">В январе 2017 г. корпорация Microsoft выпустила предварительное обновление для агента служб восстановления Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="89bd2-111">In January 2017, Microsoft released a Preview update to the MARS agent.</span></span> <span data-ttu-id="89bd2-112">Наряду с исправлениями ошибок это обновление реализует функцию мгновенного восстановления, которая позволяет подключить доступный для записи моментальный снимок точки восстановления в качестве тома восстановления.</span><span class="sxs-lookup"><span data-stu-id="89bd2-112">Along with bug fixes, this update enables Instant Restore, which allows you to mount a writeable recovery point snapshot as a recovery volume.</span></span> <span data-ttu-id="89bd2-113">Вы сможете изучить этот том восстановления и выборочно восстановить файлы из него, то есть скопировать их на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="89bd2-113">You can then explore the recovery volume and copy files to a local computer thereby selectively restoring files.</span></span>

> [!NOTE]
> <span data-ttu-id="89bd2-114">Если вы хотите использовать мгновенное восстановление данных, необходимо использовать [обновление службы архивации Azure за январь 2017 г.](https://support.microsoft.com/en-us/help/3216528?preview)</span><span class="sxs-lookup"><span data-stu-id="89bd2-114">The [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is required if you want to use Instant Restore to restore data.</span></span> <span data-ttu-id="89bd2-115">Кроме того, архивные данные должны быть защищены в хранилищах в местонахождениях, перечисленных в статье технической поддержки.</span><span class="sxs-lookup"><span data-stu-id="89bd2-115">Also the backup data must be protected in vaults in locales listed in the support article.</span></span> <span data-ttu-id="89bd2-116">В описании [обновления службы архивации Azure за январь 2017 г.](https://support.microsoft.com/en-us/help/3216528?preview) вы найдете актуальный список регионов, поддерживающих мгновенное восстановление.</span><span class="sxs-lookup"><span data-stu-id="89bd2-116">Consult the [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) for the latest list of locales that support Instant Restore.</span></span> <span data-ttu-id="89bd2-117">Сейчас мгновенное восстановление доступно **не во всех** регионах.</span><span class="sxs-lookup"><span data-stu-id="89bd2-117">Instant Restore is **not** currently available in all locales.</span></span>
>

<span data-ttu-id="89bd2-118">Мгновенное восстановление можно использовать для хранилищ службы восстановления на портале Azure и хранилищ службы архивации на классическом портале.</span><span class="sxs-lookup"><span data-stu-id="89bd2-118">Instant Restore is available for use in Recovery Services vaults in the Azure portal and Backup vaults in the classic portal.</span></span> <span data-ttu-id="89bd2-119">Если вы хотите использовать мгновенное восстановление, загрузите обновление служб восстановления Microsoft Azure и выполните процедуры, в которых упоминается мгновенное восстановление.</span><span class="sxs-lookup"><span data-stu-id="89bd2-119">If you want to use Instant Restore, download the MARS update, and follow the procedures that mention Instant Restore.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="use-instant-restore-to-recover-data-to-the-same-machine"></a><span data-ttu-id="89bd2-120">Восстановление данных на тот же компьютер с помощью мгновенного восстановления</span><span class="sxs-lookup"><span data-stu-id="89bd2-120">Use Instant Restore to recover data to the same machine</span></span>

<span data-ttu-id="89bd2-121">Если вы случайно удалили файл и хотите восстановить его на том же компьютере (с которого создана резервная копия), указанные ниже действия помогут вам восстановить данные.</span><span class="sxs-lookup"><span data-stu-id="89bd2-121">If you accidentally deleted a file and wish to restore it to the same machine (from which the backup is taken), the following steps will help you recover the data.</span></span>

1. <span data-ttu-id="89bd2-122">Откройте оснастку **Служба архивации Microsoft Azure** .</span><span class="sxs-lookup"><span data-stu-id="89bd2-122">Open the **Microsoft Azure Backup** snap in.</span></span> <span data-ttu-id="89bd2-123">Если вы не знаете, куда была установлена оснастка, найдите на компьютере или сервере **службу архивации Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="89bd2-123">If you don't know where the snap in was installed, search the computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="89bd2-124">Классическое приложение должны быть в результатах поиска.</span><span class="sxs-lookup"><span data-stu-id="89bd2-124">The desktop app should appear in the search results.</span></span>

2. <span data-ttu-id="89bd2-125">Щелкните **Восстановить данные** для запуска мастера.</span><span class="sxs-lookup"><span data-stu-id="89bd2-125">Click **Recover Data** to start the wizard.</span></span>

    ![Восстановить данные](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="89bd2-127">Чтобы восстановить данные на тот же сервер или компьютер, в области **Приступая к работе** выберите **Этот сервер (`<server name>`)** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="89bd2-127">On the **Getting Started** pane, to restore the data to the same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Выберите параметр "Этот сервер", чтобы восстановить данные на тот же компьютер](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. <span data-ttu-id="89bd2-129">В области **Выбор режима восстановления** выберите **Отдельные файлы и папки**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="89bd2-129">On the **Select Recovery Mode** pane, choose **Individual files and folders** and then click **Next**.</span></span>

    ![Обзор файлов](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. <span data-ttu-id="89bd2-131">В области **Выбор тома и даты** выберите диск, содержащий файлы и (или) папки, который необходимо восстановить.</span><span class="sxs-lookup"><span data-stu-id="89bd2-131">On the **Select Volume and Date** pane, select the volume that contains the files and/or folders you want to restore.</span></span>

    <span data-ttu-id="89bd2-132">В календаре выберите точку восстановления.</span><span class="sxs-lookup"><span data-stu-id="89bd2-132">On the calendar, select a recovery point.</span></span> <span data-ttu-id="89bd2-133">Можно восстановить данные на любой момент времени.</span><span class="sxs-lookup"><span data-stu-id="89bd2-133">You can restore from any recovery point in time.</span></span> <span data-ttu-id="89bd2-134">Даты **полужирным** шрифтом означают доступность по крайней мере одной точки восстановления.</span><span class="sxs-lookup"><span data-stu-id="89bd2-134">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="89bd2-135">Если после выбора даты доступно несколько точек восстановления, выберите конкретную точку восстановления из раскрывающегося меню **Время**.</span><span class="sxs-lookup"><span data-stu-id="89bd2-135">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![Том и дата](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. <span data-ttu-id="89bd2-137">После выбора точки восстановления нажмите кнопку **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="89bd2-137">Once you have chosen the recovery point to restore, click **Mount**.</span></span>

    <span data-ttu-id="89bd2-138">Служба архивации Azure подключит локальную точку восстановления и использует ее в качестве тома для восстановления.</span><span class="sxs-lookup"><span data-stu-id="89bd2-138">Azure Backup mounts the local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="89bd2-139">В области **Поиск и восстановление файлов** нажмите кнопку **Обзор**, чтобы открыть проводник Windows и найти нужные файлы и папки.</span><span class="sxs-lookup"><span data-stu-id="89bd2-139">On the **Browse and Recover Files** pane, click **Browse** to open Windows Explorer and find the files and folders you want.</span></span>

    ![Варианты восстановления](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. <span data-ttu-id="89bd2-141">В проводнике Windows скопируйте файлы и (или) папки, которые требуется восстановить, и вставьте их в любую локальную папку на сервере или компьютере.</span><span class="sxs-lookup"><span data-stu-id="89bd2-141">In Windows Explorer, copy the files and/or folders you want to restore and paste them to any location local to the server or computer.</span></span> <span data-ttu-id="89bd2-142">Вы можете можно открыть или передать потоком эти файлы непосредственно из тома восстановления и затем убедиться, что восстанавливаются правильные версии.</span><span class="sxs-lookup"><span data-stu-id="89bd2-142">You can open or stream the files directly from the recovery volume and verify the correct versions are recovered.</span></span>

    ![Копирование и вставка файлов и папок из подключенного тома в локальное расположение](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. <span data-ttu-id="89bd2-144">Завершив восстановление файлов и (или) папок в области **Поиск и восстановление файлов**, щелкните **Отключить**.</span><span class="sxs-lookup"><span data-stu-id="89bd2-144">When you are finished restoring the files and/or folders, on the **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="89bd2-145">Щелкните **Да**, чтобы подтвердить отключение тома.</span><span class="sxs-lookup"><span data-stu-id="89bd2-145">Then click **Yes** to confirm that you want to unmount the volume.</span></span>

    ![Отключение тома и подтверждение](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="89bd2-147">Если не щелкнуть "Отключить", то том восстановления останется подключенным в течение 6 часов с момента подключения.</span><span class="sxs-lookup"><span data-stu-id="89bd2-147">If you do not click Unmount, the Recovery Volume will remain mounted for 6 hours from the time when it was mounted.</span></span> <span data-ttu-id="89bd2-148">Но в случае, если выполняется копирование файлов, время подключения продлевается максимум на 24 часа.</span><span class="sxs-lookup"><span data-stu-id="89bd2-148">However, the mount time is extended upto a maximum of 24 hours in case of an ongoing file-copy.</span></span> <span data-ttu-id="89bd2-149">И пока он останется подключенным, невозможно будет выполнять какие-либо операции архивации.</span><span class="sxs-lookup"><span data-stu-id="89bd2-149">No backup operations will run while the volume is mounted.</span></span> <span data-ttu-id="89bd2-150">Любая операция архивации, запланированная на период, когда том восстановления подключен, будет выполнена только после его отключения.</span><span class="sxs-lookup"><span data-stu-id="89bd2-150">Any backup operation scheduled to run during the time when the volume is mounted, will run after the recovery volume is unmounted.</span></span>
    >


## <a name="use-instant-restore-to-restore-data-to-an-alternate-machine"></a><span data-ttu-id="89bd2-151">Использование мгновенного восстановления для восстановления данных на другой компьютер</span><span class="sxs-lookup"><span data-stu-id="89bd2-151">Use Instant Restore to restore data to an alternate machine</span></span>
<span data-ttu-id="89bd2-152">При потере всего содержимого сервера вы все равно можете восстановить данные из службы архивации Azure на другом компьютере.</span><span class="sxs-lookup"><span data-stu-id="89bd2-152">If your entire server is lost, you can still recover data from Azure Backup to a different machine.</span></span> <span data-ttu-id="89bd2-153">Соответствующий рабочий процесс описан ниже.</span><span class="sxs-lookup"><span data-stu-id="89bd2-153">The following steps illustrate the workflow.</span></span>


<span data-ttu-id="89bd2-154">Ниже приведена терминология, используемая в этих действиях:</span><span class="sxs-lookup"><span data-stu-id="89bd2-154">The terminology used in these steps includes:</span></span>

* <span data-ttu-id="89bd2-155">*Исходный компьютер* — компьютер, для данных на котором была создана резервная копия и который в настоящий момент недоступен.</span><span class="sxs-lookup"><span data-stu-id="89bd2-155">*Source machine* – The original machine from which the backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="89bd2-156">*Целевой компьютер* — компьютер, на который восстанавливаются данные.</span><span class="sxs-lookup"><span data-stu-id="89bd2-156">*Target machine* – The machine to which the data is being recovered.</span></span>
* <span data-ttu-id="89bd2-157">*Пример хранилища* — хранилище служб восстановления, в котором зарегистрированы *исходный* и *целевой* компьютеры.</span><span class="sxs-lookup"><span data-stu-id="89bd2-157">*Sample vault* – The Recovery Services vault to which the *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="89bd2-158">Резервные копии невозможно восстановить на целевой компьютер с более ранней версии операционной системы.</span><span class="sxs-lookup"><span data-stu-id="89bd2-158">Backups can't be restored to a target machine running an earlier version of the operating system.</span></span> <span data-ttu-id="89bd2-159">Например, резервную копию, созданную на компьютере Windows 7, можно восстановить на компьютере под управлением Windows 8 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="89bd2-159">For example, a backup taken from a Windows 7 computer can be restored on a Windows 8, or later, computer.</span></span> <span data-ttu-id="89bd2-160">А резервную копию, созданную на компьютере Windows 8, невозможно восстановить на компьютере Windows 7.</span><span class="sxs-lookup"><span data-stu-id="89bd2-160">A backup taken from a Windows 8 computer cannot be restored to a Windows 7 computer.</span></span>
>
>

1. <span data-ttu-id="89bd2-161">Откройте на **целевом компьютере** оснастку *Служба архивации Microsoft Azure*.</span><span class="sxs-lookup"><span data-stu-id="89bd2-161">Open the **Microsoft Azure Backup** snap in on the *Target machine*.</span></span>

2. <span data-ttu-id="89bd2-162">Обязательно зарегистрируйте *целевой* и *исходный* компьютеры в одном хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="89bd2-162">Ensure the *Target machine* and the *Source machine* are registered to the same Recovery Services vault.</span></span>

3. <span data-ttu-id="89bd2-163">Щелкните **Восстановить данные**, чтобы открыть **мастер восстановления данных**.</span><span class="sxs-lookup"><span data-stu-id="89bd2-163">Click **Recover Data** to open the **Recover Data wizard**.</span></span>

    ![Восстановить данные](./media/backup-azure-restore-windows-server/recover.png)

4. <span data-ttu-id="89bd2-165">В области **Приступая к работе** выберите **Другой сервер**.</span><span class="sxs-lookup"><span data-stu-id="89bd2-165">On the **Getting Started** pane, select **Another server**</span></span>

    ![Другой сервер](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. <span data-ttu-id="89bd2-167">Укажите файл с учетными данными хранилища, который соответствует *примеру хранилища*, и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="89bd2-167">Provide the vault credential file that corresponds to the *Sample vault*, and click **Next**.</span></span>

    <span data-ttu-id="89bd2-168">Если файл с учетными данными хранилища недействителен (или просрочен), скачайте новый файл из *примера хранилища* на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="89bd2-168">If the vault credential file is invalid (or expired), download a new vault credential file from the *Sample vault* in the Azure portal.</span></span> <span data-ttu-id="89bd2-169">После ввода действительных учетных данных хранилища появится имя соответствующего хранилища архивации.</span><span class="sxs-lookup"><span data-stu-id="89bd2-169">Once you provide a valid vault credential, the name of the corresponding Backup Vault appears.</span></span>


6. <span data-ttu-id="89bd2-170">В области **Выбор резервного сервера** из списка компьютеров выберите *исходный компьютер* и укажите парольную фразу.</span><span class="sxs-lookup"><span data-stu-id="89bd2-170">On the **Select Backup Server** pane, select the *Source machine* from the list of displayed machines and provide the passphrase.</span></span> <span data-ttu-id="89bd2-171">Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="89bd2-171">Then click **Next**.</span></span>

    ![Список компьютеров](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. <span data-ttu-id="89bd2-173">В области **Выбор режима восстановления** выберите **Отдельные файлы и папки** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="89bd2-173">On the **Select Recovery Mode** pane, select **Individual files and folders** and click **Next**.</span></span>

    ![Поиск](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. <span data-ttu-id="89bd2-175">В области **Выбор тома и даты** выберите диск, содержащий файлы и (или) папки, который необходимо восстановить.</span><span class="sxs-lookup"><span data-stu-id="89bd2-175">On the **Select Volume and Date** pane, select the volume that contains the files and/or folders you want to restore.</span></span>

    <span data-ttu-id="89bd2-176">В календаре выберите точку восстановления.</span><span class="sxs-lookup"><span data-stu-id="89bd2-176">On the calendar, select a recovery point.</span></span> <span data-ttu-id="89bd2-177">Можно восстановить данные на любой момент времени.</span><span class="sxs-lookup"><span data-stu-id="89bd2-177">You can restore from any recovery point in time.</span></span> <span data-ttu-id="89bd2-178">Даты **полужирным** шрифтом означают доступность по крайней мере одной точки восстановления.</span><span class="sxs-lookup"><span data-stu-id="89bd2-178">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="89bd2-179">Если после выбора даты доступно несколько точек восстановления, выберите конкретную точку восстановления из раскрывающегося меню **Время**.</span><span class="sxs-lookup"><span data-stu-id="89bd2-179">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![Поиск элементов](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. <span data-ttu-id="89bd2-181">Щелкните **Подключить**, чтобы подключить точку восстановления в качестве локального тома восстановления на *целевом компьютере*.</span><span class="sxs-lookup"><span data-stu-id="89bd2-181">Click **Mount** to locally mount the recovery point as a recovery volume on your *Target machine*.</span></span>

10. <span data-ttu-id="89bd2-182">В области **Поиск и восстановление файлов** нажмите кнопку **Обзор**, чтобы открыть проводник Windows и найти нужные файлы и папки.</span><span class="sxs-lookup"><span data-stu-id="89bd2-182">On the **Browse and Recover Files** pane, click **Browse** to open Windows Explorer and find the files and folders you want.</span></span>

    ![Шифрование](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. <span data-ttu-id="89bd2-184">В проводнике Windows скопируйте файлы и (или) папки из восстановленного тома и вставьте их в расположение на *целевом компьютере*.</span><span class="sxs-lookup"><span data-stu-id="89bd2-184">In Windows Explorer, copy the files and/or folders from the recovery volume and paste them to your *Target machine* location.</span></span> <span data-ttu-id="89bd2-185">Вы можете можно открыть или передать потоком эти файлы непосредственно из тома восстановления и затем убедиться, что восстанавливаются правильные версии.</span><span class="sxs-lookup"><span data-stu-id="89bd2-185">You can open or stream the files directly from the recovery volume and verify the correct versions are recovered.</span></span>

    ![Шифрование](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. <span data-ttu-id="89bd2-187">Завершив восстановление файлов и (или) папок в области **Поиск и восстановление файлов**, щелкните **Отключить**.</span><span class="sxs-lookup"><span data-stu-id="89bd2-187">When you are finished restoring the files and/or folders, on the **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="89bd2-188">Щелкните **Да**, чтобы подтвердить отключение тома.</span><span class="sxs-lookup"><span data-stu-id="89bd2-188">Then click **Yes** to confirm that you want to unmount the volume.</span></span>

    ![Шифрование](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="89bd2-190">Если не щелкнуть "Отключить", то том восстановления останется подключенным в течение 6 часов с момента подключения.</span><span class="sxs-lookup"><span data-stu-id="89bd2-190">If you do not click Unmount, the Recovery Volume will remain mounted for 6 hours from the time when it was mounted.</span></span> <span data-ttu-id="89bd2-191">Но в случае, если выполняется копирование файлов, время подключения продлевается максимум на 24 часа.</span><span class="sxs-lookup"><span data-stu-id="89bd2-191">However, the mount time is extended upto a maximum of 24 hours in case of an ongoing file-copy.</span></span> <span data-ttu-id="89bd2-192">И пока он останется подключенным, невозможно будет выполнять какие-либо операции архивации.</span><span class="sxs-lookup"><span data-stu-id="89bd2-192">No backup operations will run while the volume is mounted.</span></span> <span data-ttu-id="89bd2-193">Любая операция архивации, запланированная на период, когда том восстановления подключен, будет выполнена только после его отключения.</span><span class="sxs-lookup"><span data-stu-id="89bd2-193">Any backup operation scheduled to run during the time when the volume is mounted, will run after the recovery volume is unmounted.</span></span>
    >

## <a name="troubleshooting"></a><span data-ttu-id="89bd2-194">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="89bd2-194">Troubleshooting</span></span>
<span data-ttu-id="89bd2-195">Если службе Azure Backup не удалось подключить том восстановления даже по прошествии нескольких минут с момента нажатия кнопки **Подключить** или при попытке подключить том восстановления возникает сбой с отображением одной или нескольких ошибок, выполните указанные ниже действия, чтобы приступить к восстановлению в обычном порядке.</span><span class="sxs-lookup"><span data-stu-id="89bd2-195">If Azure Backup does not successfully mount the recovery volume even after several minutes of clicking **Mount** or fails to mount the recovery volume with one or more errors, follow the steps below to begin recovering normally.</span></span>

1.  <span data-ttu-id="89bd2-196">Отмените текущий процесс подключения, если он уже выполняется в течение нескольких минут.</span><span class="sxs-lookup"><span data-stu-id="89bd2-196">Cancel the ongoing mount process in case it has been running for several minutes.</span></span>

2.  <span data-ttu-id="89bd2-197">Убедитесь, что вы используете самую последнюю версию агента Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="89bd2-197">Ensure that you are on the latest version of the Azure Backup agent.</span></span> <span data-ttu-id="89bd2-198">Чтобы узнать версию агента Azure Backup, нажмите **Сведения об агенте служб восстановления Microsoft Azure** на панели **Действия** консоли Microsoft Azure Backup, а затем убедитесь, что номер в поле **Версия** соответствует номеру версии, упомянутому в [этой статье](https://go.microsoft.com/fwlink/?linkid=229525), или больше этого номера.</span><span class="sxs-lookup"><span data-stu-id="89bd2-198">To find out the version information of Azure Backup agent, click on **About Microsoft Azure Recovery Services Agent** on the **Actions** pane of Microsoft Azure Backup console and ensure that the **Version** number is equal to or higher than the version mentioned in [this article](https://go.microsoft.com/fwlink/?linkid=229525).</span></span> <span data-ttu-id="89bd2-199">Последнюю версию можно загрузить [здесь](https://go.microsoft.com/fwLink/?LinkID=288905).</span><span class="sxs-lookup"><span data-stu-id="89bd2-199">You can download the latest version from [here](https://go.microsoft.com/fwLink/?LinkID=288905)</span></span>

3.  <span data-ttu-id="89bd2-200">Последовательно выберите пункты **Диспетчер устройств** -> **Контроллеры запоминающих устройств** и убедитесь, что в списке присутствует контроллер **Инициатор iSCSI (Майкрософт)**.</span><span class="sxs-lookup"><span data-stu-id="89bd2-200">Go to **Device Manager** -> **Storage Controllers** and ensure that you can locate **Microsoft iSCSI Initiator**.</span></span> <span data-ttu-id="89bd2-201">Если он имеется в списке устройств, переходите к шагу 7 ниже.</span><span class="sxs-lookup"><span data-stu-id="89bd2-201">If you can locate it, directly go to step 7 below.</span></span> 

4.  <span data-ttu-id="89bd2-202">Если не удается найти службу инициатора Майкрософт iSCSI, упомянутую на шаге 3, обратитесь к разделу **Диспетчер устройств** -> **Контроллеры запоминающих устройств** и обратите внимание, имеется ли в этом разделе устройство с именем **Неизвестное устройство** и идентификатором оборудования **ROOT\ISCSIPRT**.</span><span class="sxs-lookup"><span data-stu-id="89bd2-202">If you cannot locate Microsoft iSCSI Initiator service as mentioned in step 3, check to see if you can find an entry under **Device Manager** -> **Storage Controllers** called **Unknown Device** with Hardware ID **ROOT\ISCSIPRT**.</span></span>

5.  <span data-ttu-id="89bd2-203">Щелкните правой кнопкой мыши **Неизвестное устройство** и выберите команду **Обновить драйверы**.</span><span class="sxs-lookup"><span data-stu-id="89bd2-203">Right click on **Unknown Device** and select **Update Driver Software**.</span></span>

6.  <span data-ttu-id="89bd2-204">Обновите драйвер, выбрав параметр **Автоматический поиск обновленных драйверов**.</span><span class="sxs-lookup"><span data-stu-id="89bd2-204">Update the driver by selecting the option to  **Search automatically for updated driver software**.</span></span> <span data-ttu-id="89bd2-205">После обновления драйверов пункт **Неизвестное устройство** должен измениться на **Инициатор iSCSI (Майкрософт)**, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="89bd2-205">Completion of the update should change **Unknown Device** to **Microsoft iSCSI Initiator** as shown below.</span></span> 

    ![Шифрование](./media/backup-azure-restore-windows-server/UnknowniSCSIDevice.png)

7.  <span data-ttu-id="89bd2-207">Последовательно выберите пункты **Диспетчер задач** -> **Службы (локальные)** -> **Служба инициатора Майкрософт iSCSI**.</span><span class="sxs-lookup"><span data-stu-id="89bd2-207">Go to **Task Manager** -> **Services (Local)** -> **Microsoft iSCSI Initiator Service**.</span></span> 

    ![Шифрование](./media/backup-azure-restore-windows-server/MicrosoftInitiatorServiceRunning.png)
    
8.  <span data-ttu-id="89bd2-209">Перезапустите службу инициатора Майкрософт iSCSI. Для этого щелкните службу правой кнопкой мыши, выберите **Остановить**, затем снова щелкните правой кнопкой мыши и нажмите **Запустить**.</span><span class="sxs-lookup"><span data-stu-id="89bd2-209">Restart the Microsoft iSCSI Initiator service by right-clicking on the service, clicking on **Stop** and further right clicking again and clicking on **Start**.</span></span>

9.  <span data-ttu-id="89bd2-210">Повторите восстановление с помощью мгновенного восстановления.</span><span class="sxs-lookup"><span data-stu-id="89bd2-210">Retry recovering using Instant Restore.</span></span> 

<span data-ttu-id="89bd2-211">Если восстановление по-прежнему не удается запустить, перезагрузите сервер и клиент.</span><span class="sxs-lookup"><span data-stu-id="89bd2-211">If the recovery still fails, reboot your server/client.</span></span> <span data-ttu-id="89bd2-212">Если перезагрузка нежелательна или восстановление по-прежнему не запускается даже после перезагрузки сервера, попробуйте выполнить восстановление на другом компьютере и обратитесь в службу поддержки Azure, перейдя на [портал Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) и отправив запрос на техническую поддержку.</span><span class="sxs-lookup"><span data-stu-id="89bd2-212">If a reboot is not desirable or the recovery still fails even after rebooting the server, try recovering from an Alternate Machine, and contact Azure Support by going to [Azure Portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and submitting a support request.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89bd2-213">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="89bd2-213">Next steps</span></span>
* <span data-ttu-id="89bd2-214">Теперь после восстановления файлов и папок можно [управлять резервными копиями](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="89bd2-214">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span></span>
