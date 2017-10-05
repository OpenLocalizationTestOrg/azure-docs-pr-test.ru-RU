---
title: "Архивация Exchange Server в службу архивации Azure с помощью System Center 2012 R2 DPM | Документация Майкрософт"
description: "Узнайте, как выполнить резервное копирование Exchange Server в службу архивации Azure с помощью System Center 2012 R2 DPM"
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
ms.openlocfilehash: 2a0e416440e55cfde70cbd20d40c99fb29b4229c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-an-exchange-server-to-azure-backup-with-system-center-2012-r2-dpm"></a><span data-ttu-id="3ae8b-103">Резервное копирование Exchange Server в службу архивации Azure с помощью System Center 2012 R2 DPM</span><span class="sxs-lookup"><span data-stu-id="3ae8b-103">Back up an Exchange server to Azure Backup with System Center 2012 R2 DPM</span></span>
<span data-ttu-id="3ae8b-104">В этой статье описывается настройка сервера Data Protection Manager (DPM) в System Center 2012 R2 для резервного копирования Microsoft Exchange Server в службу архивации Azure.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-104">This article describes how to configure a System Center 2012 R2 Data Protection Manager (DPM) server to back up a Microsoft Exchange server to  Azure Backup.</span></span>  

## <a name="updates"></a><span data-ttu-id="3ae8b-105">Обновления</span><span class="sxs-lookup"><span data-stu-id="3ae8b-105">Updates</span></span>
<span data-ttu-id="3ae8b-106">Для успешной регистрации сервера DPM в службе архивации Azure вам потребуется установить последний накопительный пакет обновления для System Center 2012 R2 DPM и последнюю версию агента резервного копирования Azure.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-106">To successfully register the DPM server with Azure Backup, you must install the latest update rollup for System Center 2012 R2 DPM and the latest version of the Azure Backup Agent.</span></span> <span data-ttu-id="3ae8b-107">Скачать последний накопительный пакет обновления можно из [каталога Microsoft](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager).</span><span class="sxs-lookup"><span data-stu-id="3ae8b-107">Get the latest update rollup from the [Microsoft Catalog](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager).</span></span>

> [!NOTE]
> <span data-ttu-id="3ae8b-108">В примерах в этой статье установлен агент резервного копирования Azure версии 2.0.8719.0, а в System Center 2012 R2 DPM установлен накопительный пакет обновления 6.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-108">For the examples in this article, version 2.0.8719.0 of the Azure Backup Agent is installed, and Update Rollup 6 is installed on System Center 2012 R2 DPM.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="3ae8b-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3ae8b-109">Prerequisites</span></span>
<span data-ttu-id="3ae8b-110">Прежде чем продолжить, выполните все [предварительные требования](backup-azure-dpm-introduction.md#prerequisites) по использованию службы архивации Microsoft Azure для защиты рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-110">Before you continue, make sure that all the [prerequisites](backup-azure-dpm-introduction.md#prerequisites) for using Microsoft Azure Backup to protect workloads have been met.</span></span> <span data-ttu-id="3ae8b-111">Список предварительных требований:</span><span class="sxs-lookup"><span data-stu-id="3ae8b-111">These prerequisites include the following:</span></span>

* <span data-ttu-id="3ae8b-112">На сайте Azure должно быть создано хранилище службы архивации.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-112">A backup vault on the Azure site has been created.</span></span>
* <span data-ttu-id="3ae8b-113">Учетные данные агента и хранилища должны быть загружены на сервер DPM.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-113">Agent and vault credentials have been downloaded to the DPM server.</span></span>
* <span data-ttu-id="3ae8b-114">Агент должен быть установлен на сервере DPM.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-114">The agent is installed on the DPM server.</span></span>
* <span data-ttu-id="3ae8b-115">Для регистрации сервера DPM должны использоваться учетные данные хранилища.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-115">The vault credentials were used to register the DPM server.</span></span>
* <span data-ttu-id="3ae8b-116">Если необходимо защитить Exchange 2016, обновите Data Protection Manager до версии DPM 2012 R2 с накопительным пакетом 9 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-116">If you are protecting Exchange 2016, please upgrade to DPM 2012 R2 UR9 or later</span></span>

## <a name="dpm-protection-agent"></a><span data-ttu-id="3ae8b-117">Агент защиты DPM</span><span class="sxs-lookup"><span data-stu-id="3ae8b-117">DPM protection agent</span></span>
<span data-ttu-id="3ae8b-118">Чтобы установить агент защиты DPM на сервере Exchange, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-118">To install the DPM protection agent on the Exchange server, follow these steps:</span></span>

1. <span data-ttu-id="3ae8b-119">Убедитесь, что брандмауэры настроены правильно.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-119">Make sure that the firewalls are correctly configured.</span></span> <span data-ttu-id="3ae8b-120">Ознакомьтесь со статьей [Настройка исключений брандмауэра для агента](https://technet.microsoft.com/library/Hh758204.aspx).</span><span class="sxs-lookup"><span data-stu-id="3ae8b-120">See [Configure firewall exceptions for the agent](https://technet.microsoft.com/library/Hh758204.aspx).</span></span>
2. <span data-ttu-id="3ae8b-121">Установите агент на сервере Exchange, выбрав **Управление > Агенты > Установить** в консоли администратора DPM.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-121">Install the agent on the Exchange server by clicking **Management > Agents > Install** in DPM Administrator Console.</span></span> <span data-ttu-id="3ae8b-122">Подробные инструкции см. в статье [Установка агента защиты DPM](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396).</span><span class="sxs-lookup"><span data-stu-id="3ae8b-122">See [Install the DPM protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span></span>

## <a name="create-a-protection-group-for-the-exchange-server"></a><span data-ttu-id="3ae8b-123">Создание группы защиты для сервера Exchange Server</span><span class="sxs-lookup"><span data-stu-id="3ae8b-123">Create a protection group for the Exchange server</span></span>
1. <span data-ttu-id="3ae8b-124">В консоли администратора DPM щелкните **Защита** и на ленте инструментов нажмите кнопку **Создать**. Откроется **мастер создания групп защиты**.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-124">In the DPM Administrator Console, click **Protection**, and then click **New** on the tool ribbon to open the **Create New Protection Group** wizard.</span></span>
2. <span data-ttu-id="3ae8b-125">На экране **приветствия** щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-125">On the **Welcome** screen of the wizard click **Next**.</span></span>
3. <span data-ttu-id="3ae8b-126">На экране **Выбор типа группы защиты** выберите **Серверы** и щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-126">On the **Select protection group type** screen, select **Servers** and click **Next**.</span></span>
4. <span data-ttu-id="3ae8b-127">Выберите на сервере Exchange Server базу данных, которую требуется защитить, и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-127">Select the Exchange server database that you want to protect and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3ae8b-128">Если вы хотите защитить базу данных Exchange 2013, изучите [предварительные требования для Exchange 2013](https://technet.microsoft.com/library/dn751029.aspx).</span><span class="sxs-lookup"><span data-stu-id="3ae8b-128">If you are protecting Exchange 2013, check the [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span></span>
   >
   >

    <span data-ttu-id="3ae8b-129">В следующем примере выбрана база данных Exchange 2010.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-129">In the following example, the Exchange 2010 database is selected.</span></span>

    ![Выберите членов группы](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. <span data-ttu-id="3ae8b-131">Выберите способ защиты данных.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-131">Select the data protection method.</span></span>

    <span data-ttu-id="3ae8b-132">Укажите имя группы защиты и выберите оба следующих параметра:</span><span class="sxs-lookup"><span data-stu-id="3ae8b-132">Name the protection group, and then select both of the following options:</span></span>

   * <span data-ttu-id="3ae8b-133">«Мне нужна краткосрочная защита с использованием диска»;</span><span class="sxs-lookup"><span data-stu-id="3ae8b-133">I want short-term protection using Disk.</span></span>
   * <span data-ttu-id="3ae8b-134">«Мне нужна оперативная защита».</span><span class="sxs-lookup"><span data-stu-id="3ae8b-134">I want online protection.</span></span>
6. <span data-ttu-id="3ae8b-135">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-135">Click **Next**.</span></span>
7. <span data-ttu-id="3ae8b-136">Выберите параметр **Запустить программу Eseutil для проверки целостности данных** , чтобы проверить целостность баз данных Exchange Server.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-136">Select the **Run Eseutil to check data integrity** option if you want to check the integrity of the Exchange Server databases.</span></span>

    <span data-ttu-id="3ae8b-137">После этого проверка согласованности резервного копирования будет выполняться на сервере DPM, что позволит исключить операции ввода-вывода при выполнении команды **eseutil** на сервере Exchange.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-137">After you select this option, backup consistency checking will be run on the DPM server to avoid the I/O traffic that’s generated by running the **eseutil** command on the Exchange server.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3ae8b-138">Чтобы использовать этот параметр, скопируйте файлы Ese.dll и Eseutil.exe в каталог C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin на сервере DPM.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-138">To use this option, you must copy the Ese.dll and Eseutil.exe files to the C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin directory on the DPM server.</span></span> <span data-ttu-id="3ae8b-139">В противном случае возникнет следующая ошибка: </span><span class="sxs-lookup"><span data-stu-id="3ae8b-139">Otherwise, the following error is triggered:</span></span>  
   > <span data-ttu-id="3ae8b-140">![ошибка Eseutil](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span><span class="sxs-lookup"><span data-stu-id="3ae8b-140">![eseutil error](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span></span>
   >
   >
8. <span data-ttu-id="3ae8b-141">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-141">Click **Next**.</span></span>
9. <span data-ttu-id="3ae8b-142">Выберите базу данных для **копирующей архивации**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-142">Select the database for **Copy Backup**, and then click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3ae8b-143">Если не выбрать «Полное резервное копирование» хотя бы для одной копии базы данных в группе обеспечения доступности баз данных, журналы не будут усечены.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-143">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span></span>
   >
   >
10. <span data-ttu-id="3ae8b-144">Настройте цели **краткосрочного резервного копирования** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-144">Configure the goals for **Short-Term backup**, and then click **Next**.</span></span>
11. <span data-ttu-id="3ae8b-145">Проверьте, есть ли на диске свободное место, и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-145">Review the available disk space, and then click **Next**.</span></span>
12. <span data-ttu-id="3ae8b-146">Выберите время создания сервером DPM начальной репликации и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-146">Select the time at which the DPM server will create the initial replication, and then click **Next**.</span></span>
13. <span data-ttu-id="3ae8b-147">Выберите параметры проверки согласованности и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-147">Select the consistency check options, and then click **Next**.</span></span>
14. <span data-ttu-id="3ae8b-148">Выберите базу данных для резервного копирования в Azure и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-148">Choose the database that you want to back up to Azure, and then click **Next**.</span></span> <span data-ttu-id="3ae8b-149">Например:</span><span class="sxs-lookup"><span data-stu-id="3ae8b-149">For example:</span></span>

    ![Выбор оперативной защиты данных](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. <span data-ttu-id="3ae8b-151">Определите расписание для **службы архивации Azure** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-151">Define the schedule for **Azure Backup**, and then click **Next**.</span></span> <span data-ttu-id="3ae8b-152">Например:</span><span class="sxs-lookup"><span data-stu-id="3ae8b-152">For example:</span></span>

    ![Выбор расписания оперативного резервного копирования](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="3ae8b-154">Обратите внимание, что точки оперативного восстановления создаются на основании точек быстрого полного восстановления.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-154">Note Online recovery points are based on express full recovery points.</span></span> <span data-ttu-id="3ae8b-155">Таким образом, в расписании резервного копирования нужно указать, что точки оперативного восстановления должны создаваться после точек быстрого полного восстановления.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-155">Therefore, you must schedule the online recovery point after the time that’s specified for the express full recovery point.</span></span>
    >
    >
16. <span data-ttu-id="3ae8b-156">Настройте политику хранения для **службы архивации Azure** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-156">Configure the retention policy for **Azure Backup**, and then click **Next**.</span></span>
17. <span data-ttu-id="3ae8b-157">Выберите параметр оперативной репликации и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-157">Choose an online replication option and click **Next**.</span></span>

    <span data-ttu-id="3ae8b-158">Если база данных имеет большой размер, процедура создания первой резервной копии по сети может занять много времени.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-158">If you have a large database, it could take a long time for the initial backup to be created over the network.</span></span> <span data-ttu-id="3ae8b-159">Чтобы избежать этого, можно создать автономную резервную копию.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-159">To avoid this issue, you can create an offline backup.</span></span>  

    ![Выбор политики оперативного хранения](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. <span data-ttu-id="3ae8b-161">Проверьте параметры и щелкните **Создать группу**.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-161">Confirm the settings, and then click **Create Group**.</span></span>
19. <span data-ttu-id="3ae8b-162">Нажмите кнопку **Закрыть**</span><span class="sxs-lookup"><span data-stu-id="3ae8b-162">Click **Close**.</span></span>

## <a name="recover-the-exchange-database"></a><span data-ttu-id="3ae8b-163">Восстановление базы данных Exchange</span><span class="sxs-lookup"><span data-stu-id="3ae8b-163">Recover the Exchange database</span></span>
1. <span data-ttu-id="3ae8b-164">Чтобы восстановить базу данных Exchange, щелкните кнопку **Восстановление** на консоли администратора DPM.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-164">To recover an Exchange database, click **Recovery** in the DPM Administrator Console.</span></span>
2. <span data-ttu-id="3ae8b-165">Выберите базу данных Exchange, которую требуется восстановить.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-165">Locate the Exchange database that you want to recover.</span></span>
3. <span data-ttu-id="3ae8b-166">Выберите точку оперативного восстановления из раскрывающегося списка *Время восстановления* .</span><span class="sxs-lookup"><span data-stu-id="3ae8b-166">Select an online recovery point from the *recovery time* drop-down list.</span></span>
4. <span data-ttu-id="3ae8b-167">Щелкните **Восстановить**, чтобы запустить **мастер восстановления**.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-167">Click **Recover** to start the **Recovery Wizard**.</span></span>

<span data-ttu-id="3ae8b-168">Для точек оперативного восстановления существует пять типов восстановления:</span><span class="sxs-lookup"><span data-stu-id="3ae8b-168">For online recovery points, there are five recovery types:</span></span>

* <span data-ttu-id="3ae8b-169">**Восстановить в исходное расположение сервера Exchange.** Данные будут восстановлены на исходный сервер Exchange Server.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-169">**Recover to original Exchange Server location:** The data will be recovered to the original Exchange server.</span></span>
* <span data-ttu-id="3ae8b-170">**Восстановить в другую базу данных на сервере Exchange.** Данные будут восстановлены в другую базу данных на другом сервере Exchange Server.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-170">**Recover to another database on an Exchange Server:** The data will be recovered to another database on another Exchange server.</span></span>
* <span data-ttu-id="3ae8b-171">**Восстановить в базу данных восстановления.** Данные будут восстановлены в базу данных восстановления Exchange (RDB).</span><span class="sxs-lookup"><span data-stu-id="3ae8b-171">**Recover to a Recovery Database:** The data will be recovered to an Exchange Recovery Database (RDB).</span></span>
* <span data-ttu-id="3ae8b-172">**Копировать в сетевую папку.** Данные будут восстановлены в сетевую папку.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-172">**Copy to a network folder:** The data will be recovered to a network folder.</span></span>
* <span data-ttu-id="3ae8b-173">**Копировать на ленту.** Если у вас имеется ленточная библиотека или изолированный ленточный накопитель, подключенные и настроенные на сервере DPM, точка восстановления будет скопирована на свободную ленту.</span><span class="sxs-lookup"><span data-stu-id="3ae8b-173">**Copy to tape:** If you have a tape library or a stand-alone tape drive attached and configured on the DPM server, the recovery point will be copied to a free tape.</span></span>

    ![Выбор оперативной репликации](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a><span data-ttu-id="3ae8b-175">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3ae8b-175">Next steps</span></span>
* [<span data-ttu-id="3ae8b-176">Часто задаваемые вопросы о службе архивации Azure</span><span class="sxs-lookup"><span data-stu-id="3ae8b-176">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
