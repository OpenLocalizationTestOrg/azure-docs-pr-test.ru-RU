---
title: "aaaBack копирование Exchange server tooAzure резервной копии с Azure Backup Server | Документы Microsoft"
description: "Узнайте, как резервное копирование tooback копирование tooAzure сервера Exchange, используя сервер резервного копирования Azure"
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
ms.assetid: e46557e8-2eaf-4ee0-99ea-00fbb8687dca
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: db874161151fc57c5b79c41531e18d577f567f66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-an-exchange-server-tooazure-backup-with-azure-backup-server"></a><span data-ttu-id="b0cdf-103">Резервное копирование Exchange server tooAzure резервной копии с сервера резервного копирования Azure</span><span class="sxs-lookup"><span data-stu-id="b0cdf-103">Back up an Exchange server tooAzure Backup with Azure Backup Server</span></span>
<span data-ttu-id="b0cdf-104">В этой статье описывается как tooback сервера архивации Microsoft Azure (MABS) tooconfigure копирование tooAzure Microsoft Exchange server.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-104">This article describes how tooconfigure Microsoft Azure Backup Server (MABS) tooback up a Microsoft Exchange server tooAzure.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="b0cdf-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b0cdf-105">Prerequisites</span></span>
<span data-ttu-id="b0cdf-106">Прежде чем продолжить, убедитесь, что Сервер резервного копирования Azure [установлен и подготовлен](backup-azure-microsoft-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="b0cdf-106">Before you continue, make sure that Azure Backup Server is [installed and prepared](backup-azure-microsoft-azure-backup.md).</span></span>

## <a name="mabs-protection-agent"></a><span data-ttu-id="b0cdf-107">Агент защиты MABS</span><span class="sxs-lookup"><span data-stu-id="b0cdf-107">MABS protection agent</span></span>
<span data-ttu-id="b0cdf-108">агент защиты MABS tooinstall hello на hello Exchange server, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-108">tooinstall hello MABS protection agent on hello Exchange server, follow these steps:</span></span>

1. <span data-ttu-id="b0cdf-109">Убедитесь, что hello брандмауэры настроены правильно.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-109">Make sure that hello firewalls are correctly configured.</span></span> <span data-ttu-id="b0cdf-110">В разделе [Настройка исключений брандмауэра для агента hello](https://technet.microsoft.com/library/Hh758204.aspx).</span><span class="sxs-lookup"><span data-stu-id="b0cdf-110">See [Configure firewall exceptions for hello agent](https://technet.microsoft.com/library/Hh758204.aspx).</span></span>
2. <span data-ttu-id="b0cdf-111">Установите агент hello на сервере Exchange hello, щелкнув **управления > агенты > установить** в консоли администрирования MABS.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-111">Install hello agent on hello Exchange server by clicking **Management > Agents > Install** in MABS Administrator Console.</span></span> <span data-ttu-id="b0cdf-112">В разделе [установке агента защиты MABS hello](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) подробное описание шагов.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-112">See [Install hello MABS protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span></span>

## <a name="create-a-protection-group-for-hello-exchange-server"></a><span data-ttu-id="b0cdf-113">Создайте группу защиты для hello Exchange server</span><span class="sxs-lookup"><span data-stu-id="b0cdf-113">Create a protection group for hello Exchange server</span></span>
1. <span data-ttu-id="b0cdf-114">В hello MABS консоль, нажмите кнопку **защиты**и нажмите кнопку **New** на ленте tooopen hello средство hello **создания новой группы защиты** мастера.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-114">In hello MABS Administrator Console, click **Protection**, and then click **New** on hello tool ribbon tooopen hello **Create New Protection Group** wizard.</span></span>
2. <span data-ttu-id="b0cdf-115">На hello **приветствия** экран приветствия мастера выберите **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-115">On hello **Welcome** screen of hello wizard click **Next**.</span></span>
3. <span data-ttu-id="b0cdf-116">На hello **Выбор типа группы защиты** выберите **серверы** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-116">On hello **Select protection group type** screen, select **Servers** and click **Next**.</span></span>
4. <span data-ttu-id="b0cdf-117">Базы данных выберите hello Exchange server tooprotect и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-117">Select hello Exchange server database that you want tooprotect and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b0cdf-118">Если необходимо обеспечить защиту Exchange 2013, проверьте hello [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span><span class="sxs-lookup"><span data-stu-id="b0cdf-118">If you are protecting Exchange 2013, check hello [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span></span>
   >
   >

    <span data-ttu-id="b0cdf-119">В следующем примере hello база данных Exchange 2010 hello выбрана.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-119">In hello following example, hello Exchange 2010 database is selected.</span></span>

    ![Выберите членов группы](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. <span data-ttu-id="b0cdf-121">Выбор метода защиты данных hello.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-121">Select hello data protection method.</span></span>

    <span data-ttu-id="b0cdf-122">Имя группы защиты hello и выберите оба hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="b0cdf-122">Name hello protection group, and then select both of hello following options:</span></span>

   * <span data-ttu-id="b0cdf-123">«Мне нужна краткосрочная защита с использованием диска»;</span><span class="sxs-lookup"><span data-stu-id="b0cdf-123">I want short-term protection using Disk.</span></span>
   * <span data-ttu-id="b0cdf-124">«Мне нужна оперативная защита».</span><span class="sxs-lookup"><span data-stu-id="b0cdf-124">I want online protection.</span></span>
6. <span data-ttu-id="b0cdf-125">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-125">Click **Next**.</span></span>
7. <span data-ttu-id="b0cdf-126">Выберите hello **целостности данных toocheck запустить программу Eseutil** Если требуется toocheck hello целостность баз данных Exchange Server hello.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-126">Select hello **Run Eseutil toocheck data integrity** option if you want toocheck hello integrity of hello Exchange Server databases.</span></span>

    <span data-ttu-id="b0cdf-127">После выбора этого параметра, проверки согласованности резервного копирования будут выполняться на MABS tooavoid hello ввода-вывода трафика, создаваемого при выполнении hello **eseutil** команду на сервере Exchange hello.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-127">After you select this option, backup consistency checking will be run on MABS tooavoid hello I/O traffic that’s generated by running hello **eseutil** command on hello Exchange server.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b0cdf-128">toouse этот параметр, необходимо скопировать hello Ese.dll и Eseutil.exe каталога C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin toohello файлов на сервере MAB hello.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-128">toouse this option, you must copy hello Ese.dll and Eseutil.exe files toohello C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin directory on hello MAB server.</span></span> <span data-ttu-id="b0cdf-129">В противном случае запускается hello следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="b0cdf-129">Otherwise, hello following error is triggered:</span></span>  
   > <span data-ttu-id="b0cdf-130">![ошибка Eseutil](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span><span class="sxs-lookup"><span data-stu-id="b0cdf-130">![eseutil error](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span></span>
   >
   >
8. <span data-ttu-id="b0cdf-131">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-131">Click **Next**.</span></span>
9. <span data-ttu-id="b0cdf-132">Выберите hello базы данных для **резервного копирования**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-132">Select hello database for **Copy Backup**, and then click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b0cdf-133">Если не выбрать «Полное резервное копирование» хотя бы для одной копии базы данных в группе обеспечения доступности баз данных, журналы не будут усечены.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-133">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span></span>
   >
   >
10. <span data-ttu-id="b0cdf-134">Настройка цели hello для **краткосрочное резервное копирование**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-134">Configure hello goals for **Short-Term backup**, and then click **Next**.</span></span>
11. <span data-ttu-id="b0cdf-135">Просмотрите hello места на диске и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-135">Review hello available disk space, and then click **Next**.</span></span>
12. <span data-ttu-id="b0cdf-136">Выберите время hello в какой hello MAB сервер создаст hello начальной репликации и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-136">Select hello time at which hello MAB Server will create hello initial replication, and then click **Next**.</span></span>
13. <span data-ttu-id="b0cdf-137">Выберите параметры проверки согласованности hello и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-137">Select hello consistency check options, and then click **Next**.</span></span>
14. <span data-ttu-id="b0cdf-138">Выберите базу данных hello требуется tooback копирование tooAzure и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-138">Choose hello database that you want tooback up tooAzure, and then click **Next**.</span></span> <span data-ttu-id="b0cdf-139">Например:</span><span class="sxs-lookup"><span data-stu-id="b0cdf-139">For example:</span></span>

    ![Выбор оперативной защиты данных](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. <span data-ttu-id="b0cdf-141">Определение расписания hello для **резервного копирования Azure**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-141">Define hello schedule for **Azure Backup**, and then click **Next**.</span></span> <span data-ttu-id="b0cdf-142">Например:</span><span class="sxs-lookup"><span data-stu-id="b0cdf-142">For example:</span></span>

    ![Выбор расписания оперативного резервного копирования](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="b0cdf-144">Обратите внимание, что точки оперативного восстановления создаются на основании точек быстрого полного восстановления.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-144">Note Online recovery points are based on express full recovery points.</span></span> <span data-ttu-id="b0cdf-145">Таким образом, необходимо запланировать hello точку восстановления после hello времени, указанный для hello express точки полного восстановления.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-145">Therefore, you must schedule hello online recovery point after hello time that’s specified for hello express full recovery point.</span></span>
    >
    >
16. <span data-ttu-id="b0cdf-146">Настроить политику хранения hello для **резервного копирования Azure**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-146">Configure hello retention policy for **Azure Backup**, and then click **Next**.</span></span>
17. <span data-ttu-id="b0cdf-147">Выберите параметр оперативной репликации и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-147">Choose an online replication option and click **Next**.</span></span>

    <span data-ttu-id="b0cdf-148">При наличии больших баз данных может занять много времени для резервного копирования toobe с начальной hello создания сети hello.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-148">If you have a large database, it could take a long time for hello initial backup toobe created over hello network.</span></span> <span data-ttu-id="b0cdf-149">tooavoid эту проблему, можно создать автономный архив.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-149">tooavoid this issue, you can create an offline backup.</span></span>  

    ![Выбор политики оперативного хранения](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. <span data-ttu-id="b0cdf-151">Подтверждение параметров hello и нажмите кнопку **создать группу**.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-151">Confirm hello settings, and then click **Create Group**.</span></span>
19. <span data-ttu-id="b0cdf-152">Нажмите кнопку **Закрыть**</span><span class="sxs-lookup"><span data-stu-id="b0cdf-152">Click **Close**.</span></span>

## <a name="recover-hello-exchange-database"></a><span data-ttu-id="b0cdf-153">Восстановление базы данных Exchange hello</span><span class="sxs-lookup"><span data-stu-id="b0cdf-153">Recover hello Exchange database</span></span>
1. <span data-ttu-id="b0cdf-154">Нажмите кнопку toorecover базы данных Exchange, **восстановления** в консоли администрирования MABS hello.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-154">toorecover an Exchange database, click **Recovery** in hello MABS Administrator Console.</span></span>
2. <span data-ttu-id="b0cdf-155">Найдите hello базы данных Exchange, которые должны toorecover.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-155">Locate hello Exchange database that you want toorecover.</span></span>
3. <span data-ttu-id="b0cdf-156">Выберите точку восстановления из hello *время восстановления* раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-156">Select an online recovery point from hello *recovery time* drop-down list.</span></span>
4. <span data-ttu-id="b0cdf-157">Нажмите кнопку **восстановить** toostart hello **мастер восстановления**.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-157">Click **Recover** toostart hello **Recovery Wizard**.</span></span>

<span data-ttu-id="b0cdf-158">Для точек оперативного восстановления существует пять типов восстановления:</span><span class="sxs-lookup"><span data-stu-id="b0cdf-158">For online recovery points, there are five recovery types:</span></span>

* <span data-ttu-id="b0cdf-159">**Восстановить toooriginal расположение сервера Exchange:** hello данные будут восстановленные toohello исходного сервера Exchange.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-159">**Recover toooriginal Exchange Server location:** hello data will be recovered toohello original Exchange server.</span></span>
* <span data-ttu-id="b0cdf-160">**Восстановление базы данных tooanother на сервере Exchange Server:** hello данные будут tooanother восстановленной базы данных на другой сервер Exchange server.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-160">**Recover tooanother database on an Exchange Server:** hello data will be recovered tooanother database on another Exchange server.</span></span>
* <span data-ttu-id="b0cdf-161">**Восстановление базы данных восстановления tooa:** hello данные будут tooan восстановленной базы данных Exchange восстановления (RDB).</span><span class="sxs-lookup"><span data-stu-id="b0cdf-161">**Recover tooa Recovery Database:** hello data will be recovered tooan Exchange Recovery Database (RDB).</span></span>
* <span data-ttu-id="b0cdf-162">**Копирование tooa сетевой папки:** hello данные будут восстановленные tooa сетевую папку.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-162">**Copy tooa network folder:** hello data will be recovered tooa network folder.</span></span>
* <span data-ttu-id="b0cdf-163">**Скопируйте tootape:** Если у вас есть ленточную библиотеку или изолированный ленточный накопитель, присоединенных и не настроен на MABS hello точки восстановления будут скопированы tooa свободная лента.</span><span class="sxs-lookup"><span data-stu-id="b0cdf-163">**Copy tootape:** If you have a tape library or a stand-alone tape drive attached and configured on MABS, hello recovery point will be copied tooa free tape.</span></span>

    ![Выбор оперативной репликации](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a><span data-ttu-id="b0cdf-165">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b0cdf-165">Next steps</span></span>
* [<span data-ttu-id="b0cdf-166">Часто задаваемые вопросы о службе архивации Azure</span><span class="sxs-lookup"><span data-stu-id="b0cdf-166">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
