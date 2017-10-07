---
title: "aaaBack копирование Exchange server tooAzure резервной копии с System Center 2012 R2 DPM | Документы Microsoft"
description: "Узнайте, как резервное копирование tooback копирование tooAzure Exchange server с помощью System Center 2012 R2 DPM"
services: backup
documentationcenter: 
author: MaanasSaran
manager: NKolli1
editor: 
ms.assetid: 13f32256-888e-416e-a78b-40c2a26a5939
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: masaran;jimpark;delhan;trinadhk;markgal
ms.openlocfilehash: fa99296d095c180333474b6d419ebc5ec727547a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-an-exchange-server-tooazure-backup-with-system-center-2012-r2-dpm"></a><span data-ttu-id="31029-103">Резервное копирование Exchange server tooAzure резервной копии с System Center 2012 R2 DPM</span><span class="sxs-lookup"><span data-stu-id="31029-103">Back up an Exchange server tooAzure Backup with System Center 2012 R2 DPM</span></span>
<span data-ttu-id="31029-104">В этой статье описывается как tooconfigure tooback сервера System Center 2012 R2 Data Protection Manager (DPM) сервер Microsoft Exchange слишком Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="31029-104">This article describes how tooconfigure a System Center 2012 R2 Data Protection Manager (DPM) server tooback up a Microsoft Exchange server too Azure Backup.</span></span>  

## <a name="updates"></a><span data-ttu-id="31029-105">Обновления</span><span class="sxs-lookup"><span data-stu-id="31029-105">Updates</span></span>
<span data-ttu-id="31029-106">toosuccessfully регистра hello сервера DPM в службе архивации Azure, необходимо установить hello последний накопительный пакет обновления для System Center 2012 R2 DPM и hello последнюю версию агента резервного копирования Azure hello.</span><span class="sxs-lookup"><span data-stu-id="31029-106">toosuccessfully register hello DPM server with Azure Backup, you must install hello latest update rollup for System Center 2012 R2 DPM and hello latest version of hello Azure Backup Agent.</span></span> <span data-ttu-id="31029-107">Получение последнего накопительного пакета обновления hello из hello [каталога Майкрософт](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager).</span><span class="sxs-lookup"><span data-stu-id="31029-107">Get hello latest update rollup from hello [Microsoft Catalog](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager).</span></span>

> [!NOTE]
> <span data-ttu-id="31029-108">Примеры в этой статье hello 2.0.8719.0 hello Azure Backup Agent версии и на System Center 2012 R2 DPM установлен накопительный пакет обновления 6.</span><span class="sxs-lookup"><span data-stu-id="31029-108">For hello examples in this article, version 2.0.8719.0 of hello Azure Backup Agent is installed, and Update Rollup 6 is installed on System Center 2012 R2 DPM.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="31029-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="31029-109">Prerequisites</span></span>
<span data-ttu-id="31029-110">Прежде чем продолжить, убедитесь, что все hello [необходимых компонентов](backup-azure-dpm-introduction.md#prerequisites) по использованию службы архивации Microsoft Azure выполнены tooprotect рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="31029-110">Before you continue, make sure that all hello [prerequisites](backup-azure-dpm-introduction.md#prerequisites) for using Microsoft Azure Backup tooprotect workloads have been met.</span></span> <span data-ttu-id="31029-111">Эти условия включают hello следующее:</span><span class="sxs-lookup"><span data-stu-id="31029-111">These prerequisites include hello following:</span></span>

* <span data-ttu-id="31029-112">Резервное хранилище на hello Azure сайта был создан.</span><span class="sxs-lookup"><span data-stu-id="31029-112">A backup vault on hello Azure site has been created.</span></span>
* <span data-ttu-id="31029-113">Агент и учетные данные хранилища была toohello загруженный сервер DPM.</span><span class="sxs-lookup"><span data-stu-id="31029-113">Agent and vault credentials have been downloaded toohello DPM server.</span></span>
* <span data-ttu-id="31029-114">Hello агент устанавливается на сервере DPM hello.</span><span class="sxs-lookup"><span data-stu-id="31029-114">hello agent is installed on hello DPM server.</span></span>
* <span data-ttu-id="31029-115">учетные данные хранилища Hello были сервера DPM используется tooregister hello.</span><span class="sxs-lookup"><span data-stu-id="31029-115">hello vault credentials were used tooregister hello DPM server.</span></span>
* <span data-ttu-id="31029-116">Если необходимо обеспечить защиту Exchange 2016, обновите tooDPM 2012 R2 UR9 или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="31029-116">If you are protecting Exchange 2016, please upgrade tooDPM 2012 R2 UR9 or later</span></span>

## <a name="dpm-protection-agent"></a><span data-ttu-id="31029-117">Агент защиты DPM</span><span class="sxs-lookup"><span data-stu-id="31029-117">DPM protection agent</span></span>
<span data-ttu-id="31029-118">tooinstall hello агент защиты DPM на сервере Exchange hello, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="31029-118">tooinstall hello DPM protection agent on hello Exchange server, follow these steps:</span></span>

1. <span data-ttu-id="31029-119">Убедитесь, что hello брандмауэры настроены правильно.</span><span class="sxs-lookup"><span data-stu-id="31029-119">Make sure that hello firewalls are correctly configured.</span></span> <span data-ttu-id="31029-120">В разделе [Настройка исключений брандмауэра для агента hello](https://technet.microsoft.com/library/Hh758204.aspx).</span><span class="sxs-lookup"><span data-stu-id="31029-120">See [Configure firewall exceptions for hello agent](https://technet.microsoft.com/library/Hh758204.aspx).</span></span>
2. <span data-ttu-id="31029-121">Установите агент hello на сервере Exchange hello, щелкнув **управления > агенты > установить** в консоли администрирования DPM.</span><span class="sxs-lookup"><span data-stu-id="31029-121">Install hello agent on hello Exchange server by clicking **Management > Agents > Install** in DPM Administrator Console.</span></span> <span data-ttu-id="31029-122">В разделе [установке агента защиты DPM hello](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) подробное описание шагов.</span><span class="sxs-lookup"><span data-stu-id="31029-122">See [Install hello DPM protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span></span>

## <a name="create-a-protection-group-for-hello-exchange-server"></a><span data-ttu-id="31029-123">Создайте группу защиты для hello Exchange server</span><span class="sxs-lookup"><span data-stu-id="31029-123">Create a protection group for hello Exchange server</span></span>
1. <span data-ttu-id="31029-124">В hello консоли администратора DPM щелкните **защиты**и нажмите кнопку **New** на ленте tooopen hello средство hello **создания новой группы защиты** мастера.</span><span class="sxs-lookup"><span data-stu-id="31029-124">In hello DPM Administrator Console, click **Protection**, and then click **New** on hello tool ribbon tooopen hello **Create New Protection Group** wizard.</span></span>
2. <span data-ttu-id="31029-125">На hello **приветствия** экран приветствия мастера выберите **Далее**.</span><span class="sxs-lookup"><span data-stu-id="31029-125">On hello **Welcome** screen of hello wizard click **Next**.</span></span>
3. <span data-ttu-id="31029-126">На hello **Выбор типа группы защиты** выберите **серверы** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="31029-126">On hello **Select protection group type** screen, select **Servers** and click **Next**.</span></span>
4. <span data-ttu-id="31029-127">Базы данных выберите hello Exchange server tooprotect и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="31029-127">Select hello Exchange server database that you want tooprotect and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="31029-128">Если необходимо обеспечить защиту Exchange 2013, проверьте hello [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span><span class="sxs-lookup"><span data-stu-id="31029-128">If you are protecting Exchange 2013, check hello [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span></span>
   >
   >

    <span data-ttu-id="31029-129">В следующем примере hello база данных Exchange 2010 hello выбрана.</span><span class="sxs-lookup"><span data-stu-id="31029-129">In hello following example, hello Exchange 2010 database is selected.</span></span>

    ![Выберите членов группы](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. <span data-ttu-id="31029-131">Выбор метода защиты данных hello.</span><span class="sxs-lookup"><span data-stu-id="31029-131">Select hello data protection method.</span></span>

    <span data-ttu-id="31029-132">Имя группы защиты hello и выберите оба hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="31029-132">Name hello protection group, and then select both of hello following options:</span></span>

   * <span data-ttu-id="31029-133">«Мне нужна краткосрочная защита с использованием диска»;</span><span class="sxs-lookup"><span data-stu-id="31029-133">I want short-term protection using Disk.</span></span>
   * <span data-ttu-id="31029-134">«Мне нужна оперативная защита».</span><span class="sxs-lookup"><span data-stu-id="31029-134">I want online protection.</span></span>
6. <span data-ttu-id="31029-135">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="31029-135">Click **Next**.</span></span>
7. <span data-ttu-id="31029-136">Выберите hello **целостности данных toocheck запустить программу Eseutil** Если требуется toocheck hello целостность баз данных Exchange Server hello.</span><span class="sxs-lookup"><span data-stu-id="31029-136">Select hello **Run Eseutil toocheck data integrity** option if you want toocheck hello integrity of hello Exchange Server databases.</span></span>

    <span data-ttu-id="31029-137">После выбора этого параметра, проверки согласованности резервного копирования будет выполняться hello DPM server tooavoid hello ввода-вывода трафика, создаваемого при выполнении hello **eseutil** команду на сервере Exchange hello.</span><span class="sxs-lookup"><span data-stu-id="31029-137">After you select this option, backup consistency checking will be run on hello DPM server tooavoid hello I/O traffic that’s generated by running hello **eseutil** command on hello Exchange server.</span></span>

   > [!NOTE]
   > <span data-ttu-id="31029-138">toouse этот параметр, необходимо скопировать hello Ese.dll и Eseutil.exe каталога C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin toohello файлов на сервере DPM hello.</span><span class="sxs-lookup"><span data-stu-id="31029-138">toouse this option, you must copy hello Ese.dll and Eseutil.exe files toohello C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin directory on hello DPM server.</span></span> <span data-ttu-id="31029-139">В противном случае запускается hello следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="31029-139">Otherwise, hello following error is triggered:</span></span>  
   > <span data-ttu-id="31029-140">![ошибка Eseutil](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span><span class="sxs-lookup"><span data-stu-id="31029-140">![eseutil error](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span></span>
   >
   >
8. <span data-ttu-id="31029-141">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="31029-141">Click **Next**.</span></span>
9. <span data-ttu-id="31029-142">Выберите hello базы данных для **резервного копирования**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="31029-142">Select hello database for **Copy Backup**, and then click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="31029-143">Если не выбрать «Полное резервное копирование» хотя бы для одной копии базы данных в группе обеспечения доступности баз данных, журналы не будут усечены.</span><span class="sxs-lookup"><span data-stu-id="31029-143">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span></span>
   >
   >
10. <span data-ttu-id="31029-144">Настройка цели hello для **краткосрочное резервное копирование**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="31029-144">Configure hello goals for **Short-Term backup**, and then click **Next**.</span></span>
11. <span data-ttu-id="31029-145">Просмотрите hello места на диске и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="31029-145">Review hello available disk space, and then click **Next**.</span></span>
12. <span data-ttu-id="31029-146">Выберите время hello в какой hello DPM сервер создаст hello начальной репликации и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="31029-146">Select hello time at which hello DPM server will create hello initial replication, and then click **Next**.</span></span>
13. <span data-ttu-id="31029-147">Выберите параметры проверки согласованности hello и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="31029-147">Select hello consistency check options, and then click **Next**.</span></span>
14. <span data-ttu-id="31029-148">Выберите базу данных hello требуется tooback копирование tooAzure и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="31029-148">Choose hello database that you want tooback up tooAzure, and then click **Next**.</span></span> <span data-ttu-id="31029-149">Например:</span><span class="sxs-lookup"><span data-stu-id="31029-149">For example:</span></span>

    ![Выбор оперативной защиты данных](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. <span data-ttu-id="31029-151">Определение расписания hello для **резервного копирования Azure**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="31029-151">Define hello schedule for **Azure Backup**, and then click **Next**.</span></span> <span data-ttu-id="31029-152">Например:</span><span class="sxs-lookup"><span data-stu-id="31029-152">For example:</span></span>

    ![Выбор расписания оперативного резервного копирования](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="31029-154">Обратите внимание, что точки оперативного восстановления создаются на основании точек быстрого полного восстановления.</span><span class="sxs-lookup"><span data-stu-id="31029-154">Note Online recovery points are based on express full recovery points.</span></span> <span data-ttu-id="31029-155">Таким образом, необходимо запланировать hello точку восстановления после hello времени, указанный для hello express точки полного восстановления.</span><span class="sxs-lookup"><span data-stu-id="31029-155">Therefore, you must schedule hello online recovery point after hello time that’s specified for hello express full recovery point.</span></span>
    >
    >
16. <span data-ttu-id="31029-156">Настроить политику хранения hello для **резервного копирования Azure**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="31029-156">Configure hello retention policy for **Azure Backup**, and then click **Next**.</span></span>
17. <span data-ttu-id="31029-157">Выберите параметр оперативной репликации и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="31029-157">Choose an online replication option and click **Next**.</span></span>

    <span data-ttu-id="31029-158">При наличии больших баз данных может занять много времени для резервного копирования toobe с начальной hello создания сети hello.</span><span class="sxs-lookup"><span data-stu-id="31029-158">If you have a large database, it could take a long time for hello initial backup toobe created over hello network.</span></span> <span data-ttu-id="31029-159">tooavoid эту проблему, можно создать автономный архив.</span><span class="sxs-lookup"><span data-stu-id="31029-159">tooavoid this issue, you can create an offline backup.</span></span>  

    ![Выбор политики оперативного хранения](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. <span data-ttu-id="31029-161">Подтверждение параметров hello и нажмите кнопку **создать группу**.</span><span class="sxs-lookup"><span data-stu-id="31029-161">Confirm hello settings, and then click **Create Group**.</span></span>
19. <span data-ttu-id="31029-162">Нажмите кнопку **Закрыть**</span><span class="sxs-lookup"><span data-stu-id="31029-162">Click **Close**.</span></span>

## <a name="recover-hello-exchange-database"></a><span data-ttu-id="31029-163">Восстановление базы данных Exchange hello</span><span class="sxs-lookup"><span data-stu-id="31029-163">Recover hello Exchange database</span></span>
1. <span data-ttu-id="31029-164">Нажмите кнопку toorecover базы данных Exchange, **восстановления** в консоли администратора DPM hello.</span><span class="sxs-lookup"><span data-stu-id="31029-164">toorecover an Exchange database, click **Recovery** in hello DPM Administrator Console.</span></span>
2. <span data-ttu-id="31029-165">Найдите hello базы данных Exchange, которые должны toorecover.</span><span class="sxs-lookup"><span data-stu-id="31029-165">Locate hello Exchange database that you want toorecover.</span></span>
3. <span data-ttu-id="31029-166">Выберите точку восстановления из hello *время восстановления* раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="31029-166">Select an online recovery point from hello *recovery time* drop-down list.</span></span>
4. <span data-ttu-id="31029-167">Нажмите кнопку **восстановить** toostart hello **мастер восстановления**.</span><span class="sxs-lookup"><span data-stu-id="31029-167">Click **Recover** toostart hello **Recovery Wizard**.</span></span>

<span data-ttu-id="31029-168">Для точек оперативного восстановления существует пять типов восстановления:</span><span class="sxs-lookup"><span data-stu-id="31029-168">For online recovery points, there are five recovery types:</span></span>

* <span data-ttu-id="31029-169">**Восстановить toooriginal расположение сервера Exchange:** hello данные будут восстановленные toohello исходного сервера Exchange.</span><span class="sxs-lookup"><span data-stu-id="31029-169">**Recover toooriginal Exchange Server location:** hello data will be recovered toohello original Exchange server.</span></span>
* <span data-ttu-id="31029-170">**Восстановление базы данных tooanother на сервере Exchange Server:** hello данные будут tooanother восстановленной базы данных на другой сервер Exchange server.</span><span class="sxs-lookup"><span data-stu-id="31029-170">**Recover tooanother database on an Exchange Server:** hello data will be recovered tooanother database on another Exchange server.</span></span>
* <span data-ttu-id="31029-171">**Восстановление базы данных восстановления tooa:** hello данные будут tooan восстановленной базы данных Exchange восстановления (RDB).</span><span class="sxs-lookup"><span data-stu-id="31029-171">**Recover tooa Recovery Database:** hello data will be recovered tooan Exchange Recovery Database (RDB).</span></span>
* <span data-ttu-id="31029-172">**Копирование tooa сетевой папки:** hello данные будут восстановленные tooa сетевую папку.</span><span class="sxs-lookup"><span data-stu-id="31029-172">**Copy tooa network folder:** hello data will be recovered tooa network folder.</span></span>
* <span data-ttu-id="31029-173">**Скопируйте tootape:** Если у вас есть ленточную библиотеку или изолированный ленточный накопитель hello присоединенных и не настроен на сервере DPM, hello точки восстановления будут скопированы tooa свободная лента.</span><span class="sxs-lookup"><span data-stu-id="31029-173">**Copy tootape:** If you have a tape library or a stand-alone tape drive attached and configured on hello DPM server, hello recovery point will be copied tooa free tape.</span></span>

    ![Выбор оперативной репликации](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a><span data-ttu-id="31029-175">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="31029-175">Next steps</span></span>
* [<span data-ttu-id="31029-176">Часто задаваемые вопросы о службе архивации Azure</span><span class="sxs-lookup"><span data-stu-id="31029-176">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
