---
title: "Резервного копирования Azure: Tooa восстановления состояния системы Windows Server | Документы Microsoft"
description: "Это пошаговое руководство по восстановлению состояния системы Windows Server из резервной копии в Azure."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/18/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: a45506507f53e2744350d3b6b2e52f1db415de4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="restore-system-state-toowindows-server"></a><span data-ttu-id="d9288-103">TooWindows восстановления состояния системы сервера</span><span class="sxs-lookup"><span data-stu-id="d9288-103">Restore System State tooWindows Server</span></span>

<span data-ttu-id="d9288-104">В этой статье объясняется, как хранилище резервных копий состояния системы Windows Server toorestore из служб восстановления Azure.</span><span class="sxs-lookup"><span data-stu-id="d9288-104">This article explains how toorestore Windows Server System State backups from an Azure Recovery Services vault.</span></span> <span data-ttu-id="d9288-105">toorestore состояния системы, необходимо иметь резервную копию состояния системы (созданные с помощью инструкции hello в [создайте резервную копию состояния системы](backup-azure-system-state.md#back-up-windows-server-system-state-preview)) и убедитесь, что вы установили hello [последнюю версию hello восстановления Microsoft Azure Агент служб (режим MARS)](http://aka.ms/azurebackup_agent).</span><span class="sxs-lookup"><span data-stu-id="d9288-105">toorestore System State, you must have a System State backup (created using hello instructions in [Back up System State](backup-azure-system-state.md#back-up-windows-server-system-state-preview)), and make sure you have installed hello [latest version of hello Microsoft Azure Recovery Services (MARS) agent](http://aka.ms/azurebackup_agent).</span></span> <span data-ttu-id="d9288-106">Восстановление данных состояния системы Windows Server из хранилища службы восстановления Azure состоит из двух этапов:</span><span class="sxs-lookup"><span data-stu-id="d9288-106">Recovering Windows Server System State data from an Azure Recovery Services vault is a two-step process:</span></span>

1. <span data-ttu-id="d9288-107">Восстановление состояния системы в виде файлов из службы Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="d9288-107">Restore System State as files from Azure Backup.</span></span> <span data-ttu-id="d9288-108">При восстановлении состояния системы в виде файлов из службы Azure Backup вы можете:</span><span class="sxs-lookup"><span data-stu-id="d9288-108">When restoring System State as files from Azure Backup, you can either:</span></span>
  * <span data-ttu-id="d9288-109">Восстановить состояние системы toohello же сервере, где было выполнено резервное копирование журнала hello, или</span><span class="sxs-lookup"><span data-stu-id="d9288-109">Restore System State toohello same server where hello backups were taken, or</span></span>
  * <span data-ttu-id="d9288-110">Восстановление состояния системы файл tooan альтернативного сервера.</span><span class="sxs-lookup"><span data-stu-id="d9288-110">Restore System State file tooan alternate server.</span></span>

2. <span data-ttu-id="d9288-111">Примените tooa файлы hello восстановить состояние системы Windows Server.</span><span class="sxs-lookup"><span data-stu-id="d9288-111">Apply hello restored System State files tooa Windows Server.</span></span>


## <a name="recover-system-state-files-toohello-same-server"></a><span data-ttu-id="d9288-112">Восстановить состояние системы файлы toohello того же сервера.</span><span class="sxs-lookup"><span data-stu-id="d9288-112">Recover System State files toohello same server</span></span>
<span data-ttu-id="d9288-113">Hello следующие шаги поясняют, как tooroll обратно к конфигурации Windows Server tooa предыдущее состояние.</span><span class="sxs-lookup"><span data-stu-id="d9288-113">hello following steps explain how tooroll back your Windows Server configuration tooa previous state.</span></span> <span data-ttu-id="d9288-114">Последовательное задней tooa конфигурации известны, устойчивое состояние сервера может быть особо важных.</span><span class="sxs-lookup"><span data-stu-id="d9288-114">Rolling your server configuration back tooa known, stable state, can be extremely valuable.</span></span> <span data-ttu-id="d9288-115">Здравствуйте, следующие шаги восстановления hello server состояние системы из хранилища служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="d9288-115">hello following steps restore hello server's System State from a Recovery Services vault.</span></span> 

1. <span data-ttu-id="d9288-116">Откройте hello **архивации Microsoft Azure** оснастки.</span><span class="sxs-lookup"><span data-stu-id="d9288-116">Open hello **Microsoft Azure Backup** snap-in.</span></span> <span data-ttu-id="d9288-117">Если вы не знаете, где установлена оснастка hello, поиск hello компьютере или сервере **архивации Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="d9288-117">If you don't know where hello snap-in was installed, search hello computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="d9288-118">Настольные приложения Hello должны отображаться в результатах поиска hello.</span><span class="sxs-lookup"><span data-stu-id="d9288-118">hello desktop app should appear in hello search results.</span></span>

2. <span data-ttu-id="d9288-119">Нажмите кнопку **восстановить данные** toostart приветствия мастера.</span><span class="sxs-lookup"><span data-stu-id="d9288-119">Click **Recover Data** toostart hello wizard.</span></span>

    ![Восстановить данные](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="d9288-121">На hello **Приступая к работе** области, toohello данных hello toorestore того же сервера или компьютера, выберите **этим сервером (`<server name>`)** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d9288-121">On hello **Getting Started** pane, toorestore hello data toohello same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![Выберите этот сервер toohello параметр toorestore hello данных того же компьютера](./media/backup-azure-restore-system-state/samemachine.png)

4. <span data-ttu-id="d9288-123">На hello **выберите режим восстановления** области, выберите **состояния системы** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d9288-123">On hello **Select Recovery Mode** pane, choose **System State** and then click **Next**.</span></span>

    ![Обзор файлов](./media/backup-azure-restore-system-state/recover-type-selection.png)

5. <span data-ttu-id="d9288-125">В календаре hello в **выберите том и дату** точки выберите восстановления.</span><span class="sxs-lookup"><span data-stu-id="d9288-125">On hello calendar in **Select Volume and Date** pane, select a recovery point.</span></span> 

    <span data-ttu-id="d9288-126">Можно восстановить данные на любой момент времени.</span><span class="sxs-lookup"><span data-stu-id="d9288-126">You can restore from any recovery point in time.</span></span> <span data-ttu-id="d9288-127">Даты в **полужирным** указать hello доступность по крайней мере одна точка восстановления.</span><span class="sxs-lookup"><span data-stu-id="d9288-127">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="d9288-128">После выбора даты, если доступны несколько точек восстановления, выберите hello конкретную точку восстановления из hello **время** раскрывающееся меню.</span><span class="sxs-lookup"><span data-stu-id="d9288-128">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![Том и дата](./media/backup-azure-restore-system-state/select-date.png)

6. <span data-ttu-id="d9288-130">После выбора toorestore точки восстановления hello щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d9288-130">Once you have chosen hello recovery point toorestore, click **Next**.</span></span>

    <span data-ttu-id="d9288-131">Резервное копирование Azure подключает точку локального восстановления hello и использует его в качестве тома для восстановления.</span><span class="sxs-lookup"><span data-stu-id="d9288-131">Azure Backup mounts hello local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="d9288-132">На следующей панели hello, укажите место назначения hello для hello восстановленные файлы состояния системы и нажмите кнопку **Обзор** требуется tooopen проводника поиска hello файлы и папки.</span><span class="sxs-lookup"><span data-stu-id="d9288-132">On hello next pane, specify hello destination for hello recovered System State files and click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span> <span data-ttu-id="d9288-133">Здравствуйте, параметр, **создавать копии, чтобы иметь обе версии**, создает копии отдельных файлов в существующий файл архив состояния системы вместо создания копии hello hello весь архив состояния системы.</span><span class="sxs-lookup"><span data-stu-id="d9288-133">hello option, **Create copies so that you have both versions**, creates copies of individual files in an existing System State file archive instead of creating hello copy of hello entire System State archive.</span></span>

    ![Варианты восстановления](./media/backup-azure-restore-system-state/recover-as-files.png)

8. <span data-ttu-id="d9288-135">Убедитесь, что сведения hello восстановления на hello **Подтверждение** панели и нажмите **восстановить**.</span><span class="sxs-lookup"><span data-stu-id="d9288-135">Verify hello details of recovery on hello **Confirmation** pane and click **Recover**.</span></span>

   ![Выберите действие восстановления hello tooacknowledge восстановления](./media/backup-azure-restore-system-state/confirm-recovery.png)

9. <span data-ttu-id="d9288-137">Копировать hello *WindowsImageBackup* каталог в hello назначения tooa некритические тома восстановления сервера hello.</span><span class="sxs-lookup"><span data-stu-id="d9288-137">Copy hello *WindowsImageBackup* directory in hello Recovery destination tooa non-critical volume of hello server.</span></span> <span data-ttu-id="d9288-138">Как правило hello тома операционной системы Windows — критический том hello.</span><span class="sxs-lookup"><span data-stu-id="d9288-138">Usually, hello Windows OS volume is hello critical volume.</span></span>

10. <span data-ttu-id="d9288-139">После успешного восстановления hello, выполните действия hello в разделе "hello" [применить восстановить toohello файлы состояния системы Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), toocomplete hello процесс восстановления состояния системы.</span><span class="sxs-lookup"><span data-stu-id="d9288-139">Once hello recovery is successful, follow hello steps in hello section, [Apply restored System State files toohello Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), toocomplete hello System State recovery process.</span></span>

## <a name="recover-system-state-files-tooan-alternate-server"></a><span data-ttu-id="d9288-140">Восстановить состояние системы файлы tooan альтернативный сервер</span><span class="sxs-lookup"><span data-stu-id="d9288-140">Recover System State files tooan alternate server</span></span>

<span data-ttu-id="d9288-141">Если сервер Windows, поврежден или недоступен, и требуется, чтобы toorestore его tooa устойчивое состояние путем восстановления Здравствуйте состояния системы Windows Server, можно восстановить состояние системы hello поврежденный сервера с другого сервера.</span><span class="sxs-lookup"><span data-stu-id="d9288-141">If your Windows Server is corrupted or inaccessible, and you want toorestore it tooa stable state by recovering hello Windows Server System State, you can restore hello corrupted server's System State from another server.</span></span> <span data-ttu-id="d9288-142">Используйте следующие шаги toohello восстановления состояния системы на отдельном сервере hello.</span><span class="sxs-lookup"><span data-stu-id="d9288-142">Use hello following steps toohello restore System State on a separate server.</span></span>  

<span data-ttu-id="d9288-143">включает Hello терминология, используемая в этом пошаговом руководстве:</span><span class="sxs-lookup"><span data-stu-id="d9288-143">hello terminology used in these steps includes:</span></span>

- <span data-ttu-id="d9288-144">*Исходный компьютер* — была сделана hello исходной машины, из какой резервный hello и который в данный момент недоступен.</span><span class="sxs-lookup"><span data-stu-id="d9288-144">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
- <span data-ttu-id="d9288-145">*Целевой компьютер* — восстанавливаются данные hello toowhich машины hello.</span><span class="sxs-lookup"><span data-stu-id="d9288-145">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
- <span data-ttu-id="d9288-146">*Образец хранилища* — hello toowhich хранилище служб восстановления hello *исходной машины* и *целевой компьютер* зарегистрированы.</span><span class="sxs-lookup"><span data-stu-id="d9288-146">*Sample vault* – hello Recovery Services vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="d9288-147">Резервные копии, созданные с одного компьютера не может быть восстановленной tooa компьютере, работающем под управлением более ранней версии операционной системы hello.</span><span class="sxs-lookup"><span data-stu-id="d9288-147">Backups taken from one machine cannot be restored tooa machine running an earlier version of hello operating system.</span></span> <span data-ttu-id="d9288-148">Например резервные копии, созданные из Windows Server 2016 машины не может быть восстановлена tooWindows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="d9288-148">For example, backups taken from a Windows Server 2016 machine can't be restored tooWindows Server 2012 R2.</span></span> <span data-ttu-id="d9288-149">Тем не менее возможна hello обратное.</span><span class="sxs-lookup"><span data-stu-id="d9288-149">However, hello inverse is possible.</span></span> <span data-ttu-id="d9288-150">Можно использовать резервные копии из Windows Server 2012 R2 toorestore Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="d9288-150">You can use backups from Windows Server 2012 R2 toorestore Windows Server 2016.</span></span>
>

1. <span data-ttu-id="d9288-151">Откройте hello **архивации Microsoft Azure** оснастки на hello *целевой компьютер*.</span><span class="sxs-lookup"><span data-stu-id="d9288-151">Open hello **Microsoft Azure Backup** snap-in on hello *Target machine*.</span></span>
2. <span data-ttu-id="d9288-152">Убедитесь, что hello *целевой компьютер* и hello *исходной машины* , зарегистрированных toohello же восстановления службы в хранилище.</span><span class="sxs-lookup"><span data-stu-id="d9288-152">Ensure that hello *Target machine* and hello *Source machine* are registered toohello same Recovery Services vault.</span></span>
3. <span data-ttu-id="d9288-153">Нажмите кнопку **восстановить данные** рабочего процесса tooinitiate hello.</span><span class="sxs-lookup"><span data-stu-id="d9288-153">Click **Recover Data** tooinitiate hello workflow.</span></span>

    ![Восстановить данные](./media/backup-azure-restore-windows-server-classic/recover.png)

4. <span data-ttu-id="d9288-155">Выберите **Другой сервер**</span><span class="sxs-lookup"><span data-stu-id="d9288-155">Select **Another server**</span></span>

    ![Другой сервер](./media/backup-azure-restore-system-state/anotherserver.png)

5. <span data-ttu-id="d9288-157">Укажите файл hello хранилище учетных данных, который соответствует toohello *хранилище образец*.</span><span class="sxs-lookup"><span data-stu-id="d9288-157">Provide hello vault credential file that corresponds toohello *Sample vault*.</span></span> <span data-ttu-id="d9288-158">Если файл учетных данных хранилища hello является недопустимым (или истекшим сроком действия), загрузите новый файл учетных данных хранилища из hello *хранилище образец* в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d9288-158">If hello vault credential file is invalid (or expired), download a new vault credential file from hello *Sample vault* in hello Azure portal.</span></span> <span data-ttu-id="d9288-159">После задания предоставляется файл учетных данных хранилища hello, отображается hello хранилище служб восстановления, связанных с hello файл учетных данных хранилища.</span><span class="sxs-lookup"><span data-stu-id="d9288-159">Once hello vault credential file is provided, hello Recovery Services vault associated with hello vault credential file appears.</span></span>

6. <span data-ttu-id="d9288-160">На панели выберите резервный сервер hello выберите hello *исходной машины* из списка отображаемых машины hello.</span><span class="sxs-lookup"><span data-stu-id="d9288-160">On hello Select Backup Server pane, select hello *Source machine* from hello list of displayed machines.</span></span>

    ![Список компьютеров](./media/backup-azure-restore-windows-server-classic/machinelist.png)

7. <span data-ttu-id="d9288-162">В области hello выберите режим восстановления, выберите **состояния системы** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d9288-162">On hello Select Recovery Mode pane, choose **System State** and click **Next**.</span></span> 

    ![Поиск](./media/backup-azure-restore-system-state/recover-type-selection.png)

8. <span data-ttu-id="d9288-164">На hello календаря в hello **выберите том и дату** точки выберите восстановления.</span><span class="sxs-lookup"><span data-stu-id="d9288-164">On hello Calendar in hello **Select Volume and Date** pane, select a recovery point.</span></span> <span data-ttu-id="d9288-165">Можно восстановить данные на любой момент времени.</span><span class="sxs-lookup"><span data-stu-id="d9288-165">You can restore from any recovery point in time.</span></span> <span data-ttu-id="d9288-166">Даты в **полужирным** указать hello доступность по крайней мере одна точка восстановления.</span><span class="sxs-lookup"><span data-stu-id="d9288-166">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="d9288-167">После выбора даты, если доступны несколько точек восстановления, выберите hello конкретную точку восстановления из hello **время** раскрывающееся меню.</span><span class="sxs-lookup"><span data-stu-id="d9288-167">Once  you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span> 

    ![Поиск элементов](./media/backup-azure-restore-system-state/select-date.png)

9. <span data-ttu-id="d9288-169">После выбора toorestore точки восстановления hello щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d9288-169">Once you have chosen hello recovery point toorestore, click **Next**.</span></span>

10. <span data-ttu-id="d9288-170">На hello **выберите режим восстановления состояния системы** области, укажите hello место назначения toobe восстановить файлы состояния системы, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d9288-170">On hello **Select System State Recovery Mode** pane, specify hello destination where you want System State files toobe recovered, then click **Next**.</span></span>

    ![Шифрование](./media/backup-azure-restore-system-state/recover-as-files.png)

    <span data-ttu-id="d9288-172">Здравствуйте, параметр, **создавать копии, чтобы иметь обе версии**, создает копии отдельных файлов в существующий файл архив состояния системы вместо создания копии hello hello весь архив состояния системы.</span><span class="sxs-lookup"><span data-stu-id="d9288-172">hello option, **Create copies so that you have both versions**, creates copies of individual files in an existing System State file archive instead of creating hello copy of hello entire System State archive.</span></span>

11. <span data-ttu-id="d9288-173">Убедитесь, что сведения hello восстановления на панели hello подтверждения и нажмите кнопку **восстановить**.</span><span class="sxs-lookup"><span data-stu-id="d9288-173">Verify hello details of recovery on hello Confirmation pane, and click **Recover**.</span></span> 

    ![Нажмите кнопку hello hello восстановить кнопки tooconfirm процесс восстановления](./media/backup-azure-restore-system-state/confirm-recovery.png)

12. <span data-ttu-id="d9288-175">Копировать hello *WindowsImageBackup* каталога tooa некритические тома hello сервере (например D:\).</span><span class="sxs-lookup"><span data-stu-id="d9288-175">Copy hello *WindowsImageBackup* directory tooa non-critical volume of hello server (for example D:\).</span></span> <span data-ttu-id="d9288-176">Обычно hello тома операционной системы Windows — критический том hello.</span><span class="sxs-lookup"><span data-stu-id="d9288-176">Usually hello Windows OS volume is hello critical volume.</span></span>

13. <span data-ttu-id="d9288-177">процесс восстановления toocomplete hello, используйте следующие hello статьи слишком[применять hello восстановить файлы состояния системы в Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).</span><span class="sxs-lookup"><span data-stu-id="d9288-177">toocomplete hello recovery process, use hello following section too[apply hello restored System State files on a Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).</span></span>




## <a name="apply-restored-system-state-on-a-windows-server"></a><span data-ttu-id="d9288-178">Применение восстановленного состояния системы в Windows Server</span><span class="sxs-lookup"><span data-stu-id="d9288-178">Apply restored System State on a Windows Server</span></span>

<span data-ttu-id="d9288-179">После восстановления состояния системы как файлы, используя агент служб восстановления Azure используйте hello архивации данных Windows Server программа tooapply hello восстановить tooWindows состояние системы сервера.</span><span class="sxs-lookup"><span data-stu-id="d9288-179">Once you have recovered System State as files using Azure Recovery Services Agent, use hello Windows Server Backup utility tooapply hello recovered System State tooWindows Server.</span></span> <span data-ttu-id="d9288-180">Hello программа архивации данных Windows Server уже доступна на сервере hello.</span><span class="sxs-lookup"><span data-stu-id="d9288-180">hello Windows Server Backup utility is already available on hello server.</span></span> <span data-ttu-id="d9288-181">Hello следующие шаги поясняют, как tooapply hello восстановить состояние системы.</span><span class="sxs-lookup"><span data-stu-id="d9288-181">hello following steps explain how tooapply hello recovered System State.</span></span>

1. <span data-ttu-id="d9288-182">Используйте hello следующими командами tooreboot к серверу в *режиме восстановления служб каталогов*.</span><span class="sxs-lookup"><span data-stu-id="d9288-182">Use hello following commands tooreboot your server in *Directory Services Repair Mode*.</span></span> <span data-ttu-id="d9288-183">В командной строке с повышенными привилегиями:</span><span class="sxs-lookup"><span data-stu-id="d9288-183">In an elevated command prompt:</span></span>

    ```
    PS C:\> Bcdedit /set safeboot dsrepair
    PS C:\> Shutdown /r /t 0
    ```

2. <span data-ttu-id="d9288-184">После перезагрузки hello откройте оснастку hello архивации данных Windows Server.</span><span class="sxs-lookup"><span data-stu-id="d9288-184">After hello reboot, open hello Windows Server Backup snap-in.</span></span> <span data-ttu-id="d9288-185">Если вы не знаете, где установлена оснастка hello, поиск hello компьютере или сервере **архивации данных Windows Server**.</span><span class="sxs-lookup"><span data-stu-id="d9288-185">If you don't know where hello snap-in was installed, search hello computer or server for **Windows Server Backup**.</span></span>

    <span data-ttu-id="d9288-186">Настольные приложения Hello появится в результатах поиска hello.</span><span class="sxs-lookup"><span data-stu-id="d9288-186">hello desktop app appears in hello search results.</span></span>

3. <span data-ttu-id="d9288-187">В оснастке hello, выберите **локальная Архивация**.</span><span class="sxs-lookup"><span data-stu-id="d9288-187">In hello snap-in, select **Local Backup**.</span></span>

    ![Выберите toorestore локальная архивация оттуда.](./media/backup-azure-restore-system-state/win-server-backup-local-backup.png)

4. <span data-ttu-id="d9288-189">На консоли локальной резервной копии hello в hello **панель действий**, нажмите кнопку **восстановить** tooopen приветствия мастера восстановления.</span><span class="sxs-lookup"><span data-stu-id="d9288-189">On hello Local Backup console, in hello **Actions Pane**, click **Recover** tooopen hello Recovery Wizard.</span></span>

5. <span data-ttu-id="d9288-190">Выберите параметр hello **резервной копии, хранящейся в другом месте**и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d9288-190">Select hello option, **A backup stored in another location**, and click **Next**.</span></span>

   ![Выберите другой сервер tooa toorecover](./media/backup-azure-restore-system-state/backup-stored-in-diff-location.png)

6. <span data-ttu-id="d9288-192">При указании типа расположения hello выберите **удаленная общая папка** восстановленные tooanother сервера в случае резервного копирования состояния системы.</span><span class="sxs-lookup"><span data-stu-id="d9288-192">When specifying hello location type, select **Remote shared folder** if your System State backup was recovered tooanother server.</span></span> <span data-ttu-id="d9288-193">Если состояние системы было восстановлено локально, выберите **Локальные диски**.</span><span class="sxs-lookup"><span data-stu-id="d9288-193">If your System State was recovered locally, then select **Local drives**.</span></span> 

    ![Выберите ли toorecovery с локального сервера или другой](./media/backup-azure-restore-system-state/ss-recovery-remote-shared-folder.png)

7. <span data-ttu-id="d9288-195">Введите путь toohello hello *WindowsImageBackup* каталога, или выберите hello локальный диск, содержащий этот каталог (например, D:\WindowsImageBackup), восстановление в процессе восстановления файлов hello состояния системы, с помощью службы восстановления Azure Службы агента и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d9288-195">Enter hello path toohello *WindowsImageBackup* directory, or choose hello local drive containing this directory (for example, D:\WindowsImageBackup), recovered as part of hello System State files recovery using Azure Recovery Services Agent and click **Next**.</span></span>

    ![путь toohello общего файла](./media/backup-azure-restore-system-state/ss-recovery-remote-folder.png)

8. <span data-ttu-id="d9288-197">Версия состояния системы выберите hello требуется toorestore и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d9288-197">Select hello System State version that you want toorestore, and click **Next**.</span></span>

9. <span data-ttu-id="d9288-198">В области выберите тип восстановления hello выберите **состояния системы** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d9288-198">In hello Select Recovery Type pane, select **System State** and click **Next**.</span></span>

10. <span data-ttu-id="d9288-199">Расположение hello hello восстановления состояния системы, выберите **исходное расположение**и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="d9288-199">For hello location of hello System State Recovery, select **Original Location**, and click **Next**.</span></span>

11. <span data-ttu-id="d9288-200">Просмотрите сведения о подтверждении hello, проверьте параметры перезагрузки hello и нажмите кнопку **восстановить** tooapplly hello восстановленных файлов состояния системы.</span><span class="sxs-lookup"><span data-stu-id="d9288-200">Review hello confirmation details, verify hello reboot settings, and click **Recover** tooapplly hello restored System State files.</span></span>

    ![hello запуска восстановления состояния системы файлов](./media/backup-azure-restore-system-state/launch-ss-recovery.png)

## <a name="special-considerations-for-system-state-recovery-on-active-directory-server"></a><span data-ttu-id="d9288-202">Специальные рекомендации для восстановления состояния системы на сервере Active Directory</span><span class="sxs-lookup"><span data-stu-id="d9288-202">Special considerations for System State recovery on Active Directory server</span></span>

<span data-ttu-id="d9288-203">Резервная копия состояния системы включает данные Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d9288-203">System State backup includes Active Directory data.</span></span> <span data-ttu-id="d9288-204">Используйте следующие шаги toorestore доменные службы Active Directory (AD DS) из текущего состояния tooa предыдущего состояния hello.</span><span class="sxs-lookup"><span data-stu-id="d9288-204">Use hello following steps toorestore Active Directory Domain Service (AD DS) from its current state tooa previous state.</span></span>

1. <span data-ttu-id="d9288-205">Перезапустите контроллер домена hello в режиме восстановления служб каталогов (DSRM).</span><span class="sxs-lookup"><span data-stu-id="d9288-205">Restart hello domain controller in Directory Services Restore Mode (DSRM).</span></span>
2. <span data-ttu-id="d9288-206">Выполните действия hello [здесь](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) toorecover командлеты toouse архивации данных Windows Server AD DS.</span><span class="sxs-lookup"><span data-stu-id="d9288-206">Follow hello steps [here](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) toouse Windows Server Backup cmdlets toorecover AD DS.</span></span>


## <a name="troubleshoot-failed-system-state-restore"></a><span data-ttu-id="d9288-207">Устранение неполадок при сбое восстановления состояния системы</span><span class="sxs-lookup"><span data-stu-id="d9288-207">Troubleshoot failed System State restore</span></span>

<span data-ttu-id="d9288-208">Если hello предыдущий процесс применения состояния системы не завершается успешно, используйте toorecover hello среды восстановления Windows (Win RE) Windows Server.</span><span class="sxs-lookup"><span data-stu-id="d9288-208">If hello previous process of applying System State does not complete successfully, use hello Windows Recovery Environment (Win RE) toorecover your Windows Server.</span></span> <span data-ttu-id="d9288-209">Hello следующие шаги поясняют, как с помощью Win RE toorecover.</span><span class="sxs-lookup"><span data-stu-id="d9288-209">hello following steps explain how toorecover using Win RE.</span></span> <span data-ttu-id="d9288-210">Используйте этот вариант, только если Windows Server не загружается нормально после восстановления состояния системы.</span><span class="sxs-lookup"><span data-stu-id="d9288-210">Use This option only if Windows Server does not boot normally after a System State restore.</span></span> <span data-ttu-id="d9288-211">Привет, следуйте процедуре стирает данные систем, соблюдайте осторожность.</span><span class="sxs-lookup"><span data-stu-id="d9288-211">hello following process erases non-system data, use caution.</span></span> 

1. <span data-ttu-id="d9288-212">Загрузка сервера Windows hello среды восстановления Windows (Win RE).</span><span class="sxs-lookup"><span data-stu-id="d9288-212">Boot your Windows Server into hello Windows Recovery Environment (Win RE).</span></span>

2. <span data-ttu-id="d9288-213">Выберите Устранение неполадок из трех доступных вариантов hello.</span><span class="sxs-lookup"><span data-stu-id="d9288-213">Select Troubleshoot from hello three available options.</span></span>

    ![Открытие меню](./media/backup-azure-restore-system-state/winre-1.png)

3. <span data-ttu-id="d9288-215">Из hello **Дополнительные параметры** выберите **командной строки** и укажите имя пользователя администратора сервера hello и пароль.</span><span class="sxs-lookup"><span data-stu-id="d9288-215">From hello **Advanced Options** screen, select **Command Prompt** and provide hello server administrator username and password.</span></span>

   ![Открытие меню](./media/backup-azure-restore-system-state/winre-2.png)

4. <span data-ttu-id="d9288-217">Укажите имя пользователя администратора сервера hello и пароль.</span><span class="sxs-lookup"><span data-stu-id="d9288-217">Provide hello server administrator username and password.</span></span>

    ![Открытие меню](./media/backup-azure-restore-system-state/winre-3.png)

5. <span data-ttu-id="d9288-219">При открытии hello командной строки с правами администратора, запустите следующие версии резервного копирования состояния системы hello tooget команды.</span><span class="sxs-lookup"><span data-stu-id="d9288-219">When you open hello command prompt in administrator mode, run following command tooget hello System State backup versions.</span></span>

    ```
    Wbadmin get versions -backuptarget:<Volume where WindowsImageBackup folder is copied>:
    ```
    ![Получение версий резервного копирования состояния системы](./media/backup-azure-restore-system-state/winre-4.png)

6. <span data-ttu-id="d9288-221">Запустите следующие команды tooget hello все тома в резервной копии hello.</span><span class="sxs-lookup"><span data-stu-id="d9288-221">Run hello following command tooget all volumes available in hello backup.</span></span>

    ```
    Wbadmin get items -version:<copy version from above step> -backuptarget:<Backup volume>
    ```

    ![Получение версий резервного копирования состояния системы](./media/backup-azure-restore-system-state/winre-5.png)

7. <span data-ttu-id="d9288-223">Hello следующая команда восстанавливает все тома, которые являются частью hello резервной копии состояния системы.</span><span class="sxs-lookup"><span data-stu-id="d9288-223">hello following command recovers all volumes that are part of hello System State Backup.</span></span> <span data-ttu-id="d9288-224">Обратите внимание, что этот шаг восстанавливает только hello критические тома, которые являются частью hello состояния системы.</span><span class="sxs-lookup"><span data-stu-id="d9288-224">Note that this step recovers only hello critical volumes that are part of hello System State.</span></span> <span data-ttu-id="d9288-225">Все несистемные данные удаляются.</span><span class="sxs-lookup"><span data-stu-id="d9288-225">All non-System data is erased.</span></span>

    ```
    Wbadmin start recovery -items:C: -itemtype:Volume -version:<Backupversion> -backuptarget:<backup target volume>
    ```
     ![Получение версий резервного копирования состояния системы](./media/backup-azure-restore-system-state/winre-6.png)



## <a name="next-steps"></a><span data-ttu-id="d9288-227">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d9288-227">Next steps</span></span>
* <span data-ttu-id="d9288-228">Теперь после восстановления файлов и папок можно [управлять резервными копиями](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="d9288-228">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span></span>
