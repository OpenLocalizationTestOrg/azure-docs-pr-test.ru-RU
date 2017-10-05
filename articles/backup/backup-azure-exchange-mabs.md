---
title: "Архивация сервера Exchange Server в службу архивации Azure с помощью Сервера резервного копирования Azure | Документация Майкрософт"
description: "Узнайте, как выполнить архивацию сервера Exchange Server в службу архивации Azure с помощью Сервера резервного копирования Azure."
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
ms.openlocfilehash: 60b784fd00013c2b9504f8635c6b5c4c592563be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-an-exchange-server-to-azure-backup-with-azure-backup-server"></a><span data-ttu-id="3b7c0-103">Архивация сервера Exchange Server в службу архивации Azure с помощью Сервера резервного копирования Azure</span><span class="sxs-lookup"><span data-stu-id="3b7c0-103">Back up an Exchange server to Azure Backup with Azure Backup Server</span></span>
<span data-ttu-id="3b7c0-104">В этой статье описывается, как настроить Сервер резервного копирования Microsoft Azure (MABS) для архивации сервера Microsoft Exchange Server в Azure.</span><span class="sxs-lookup"><span data-stu-id="3b7c0-104">This article describes how to configure Microsoft Azure Backup Server (MABS) to back up a Microsoft Exchange server to Azure.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="3b7c0-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3b7c0-105">Prerequisites</span></span>
<span data-ttu-id="3b7c0-106">Прежде чем продолжить, убедитесь, что Сервер резервного копирования Azure [установлен и подготовлен](backup-azure-microsoft-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="3b7c0-106">Before you continue, make sure that Azure Backup Server is [installed and prepared](backup-azure-microsoft-azure-backup.md).</span></span>

## <a name="mabs-protection-agent"></a><span data-ttu-id="3b7c0-107">Агент защиты MABS</span><span class="sxs-lookup"><span data-stu-id="3b7c0-107">MABS protection agent</span></span>
<span data-ttu-id="3b7c0-108">Чтобы установить агент защиты MABS на сервер Exchange Server, выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="3b7c0-108">To install the MABS protection agent on the Exchange server, follow these steps:</span></span>

1. <span data-ttu-id="3b7c0-109">Убедитесь, что брандмауэры настроены правильно.</span><span class="sxs-lookup"><span data-stu-id="3b7c0-109">Make sure that the firewalls are correctly configured.</span></span> <span data-ttu-id="3b7c0-110">Ознакомьтесь со статьей [Настройка исключений брандмауэра для агента](https://technet.microsoft.com/library/Hh758204.aspx).</span><span class="sxs-lookup"><span data-stu-id="3b7c0-110">See [Configure firewall exceptions for the agent](https://technet.microsoft.com/library/Hh758204.aspx).</span></span>
2. <span data-ttu-id="3b7c0-111">Установите агент на сервере Exchange Server, выбрав **Управление > Агенты > Установить** в консоли администратора MABS.</span><span class="sxs-lookup"><span data-stu-id="3b7c0-111">Install the agent on the Exchange server by clicking **Management > Agents > Install** in MABS Administrator Console.</span></span> <span data-ttu-id="3b7c0-112">Подробные инструкции см. в статье [Установка агента защиты DPM](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396).</span><span class="sxs-lookup"><span data-stu-id="3b7c0-112">See [Install the MABS protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span></span>

## <a name="create-a-protection-group-for-the-exchange-server"></a><span data-ttu-id="3b7c0-113">Создание группы защиты для сервера Exchange Server</span><span class="sxs-lookup"><span data-stu-id="3b7c0-113">Create a protection group for the Exchange server</span></span>
1. <span data-ttu-id="3b7c0-114">В консоли администратора MABS щелкните **Защита**, затем на ленте инструментов нажмите кнопку **Создать**. Откроется **мастер создания групп защиты**.</span><span class="sxs-lookup"><span data-stu-id="3b7c0-114">In the MABS Administrator Console, click **Protection**, and then click **New** on the tool ribbon to open the **Create New Protection Group** wizard.</span></span>
2. <span data-ttu-id="3b7c0-115">На экране **приветствия** щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3b7c0-115">On the **Welcome** screen of the wizard click **Next**.</span></span>
3. <span data-ttu-id="3b7c0-116">На экране **Выбор типа группы защиты** выберите **Серверы** и щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3b7c0-116">On the **Select protection group type** screen, select **Servers** and click **Next**.</span></span>
4. <span data-ttu-id="3b7c0-117">Выберите на сервере Exchange Server базу данных, которую требуется защитить, и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3b7c0-117">Select the Exchange server database that you want to protect and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3b7c0-118">Если вы хотите защитить базу данных Exchange 2013, изучите [предварительные требования для Exchange 2013](https://technet.microsoft.com/library/dn751029.aspx).</span><span class="sxs-lookup"><span data-stu-id="3b7c0-118">If you are protecting Exchange 2013, check the [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span></span>
   >
   >

    <span data-ttu-id="3b7c0-119">В следующем примере выбрана база данных Exchange 2010.</span><span class="sxs-lookup"><span data-stu-id="3b7c0-119">In the following example, the Exchange 2010 database is selected.</span></span>

    ![Выберите членов группы](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. <span data-ttu-id="3b7c0-121">Выберите способ защиты данных.</span><span class="sxs-lookup"><span data-stu-id="3b7c0-121">Select the data protection method.</span></span>

    <span data-ttu-id="3b7c0-122">Укажите имя группы защиты и выберите оба следующих параметра:</span><span class="sxs-lookup"><span data-stu-id="3b7c0-122">Name the protection group, and then select both of the following options:</span></span>

   * <span data-ttu-id="3b7c0-123">«Мне нужна краткосрочная защита с использованием диска»;</span><span class="sxs-lookup"><span data-stu-id="3b7c0-123">I want short-term protection using Disk.</span></span>
   * <span data-ttu-id="3b7c0-124">«Мне нужна оперативная защита».</span><span class="sxs-lookup"><span data-stu-id="3b7c0-124">I want online protection.</span></span>
6. <span data-ttu-id="3b7c0-125">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3b7c0-125">Click **Next**.</span></span>
7. <span data-ttu-id="3b7c0-126">Выберите параметр **Запустить программу Eseutil для проверки целостности данных** , чтобы проверить целостность баз данных Exchange Server.</span><span class="sxs-lookup"><span data-stu-id="3b7c0-126">Select the **Run Eseutil to check data integrity** option if you want to check the integrity of the Exchange Server databases.</span></span>

    <span data-ttu-id="3b7c0-127">После этого проверка согласованности резервных копий будет выполняться на сервере MABS, что позволит исключить операции ввода-вывода при выполнении команды **eseutil** на сервере Exchange Server.</span><span class="sxs-lookup"><span data-stu-id="3b7c0-127">After you select this option, backup consistency checking will be run on MABS to avoid the I/O traffic that’s generated by running the **eseutil** command on the Exchange server.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3b7c0-128">Чтобы использовать этот параметр, скопируйте файлы Ese.dll и Eseutil.exe в каталог C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin на сервере MABS.</span><span class="sxs-lookup"><span data-stu-id="3b7c0-128">To use this option, you must copy the Ese.dll and Eseutil.exe files to the C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin directory on the MAB server.</span></span> <span data-ttu-id="3b7c0-129">В противном случае возникнет следующая ошибка: </span><span class="sxs-lookup"><span data-stu-id="3b7c0-129">Otherwise, the following error is triggered:</span></span>  
   > <span data-ttu-id="3b7c0-130">![ошибка Eseutil](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span><span class="sxs-lookup"><span data-stu-id="3b7c0-130">![eseutil error](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span></span>
   >
   >
8. <span data-ttu-id="3b7c0-131">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3b7c0-131">Click **Next**.</span></span>
9. <span data-ttu-id="3b7c0-132">Выберите базу данных для **копирующей архивации**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3b7c0-132">Select the database for **Copy Backup**, and then click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3b7c0-133">Если не выбрать «Полное резервное копирование» хотя бы для одной копии базы данных в группе обеспечения доступности баз данных, журналы не будут усечены.</span><span class="sxs-lookup"><span data-stu-id="3b7c0-133">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span></span>
   >
   >
10. <span data-ttu-id="3b7c0-134">Настройте цели **краткосрочного резервного копирования** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3b7c0-134">Configure the goals for **Short-Term backup**, and then click **Next**.</span></span>
11. <span data-ttu-id="3b7c0-135">Проверьте, есть ли на диске свободное место, и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3b7c0-135">Review the available disk space, and then click **Next**.</span></span>
12. <span data-ttu-id="3b7c0-136">Выберите время создания сервером MABS начальной репликации и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3b7c0-136">Select the time at which the MAB Server will create the initial replication, and then click **Next**.</span></span>
13. <span data-ttu-id="3b7c0-137">Выберите параметры проверки согласованности и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3b7c0-137">Select the consistency check options, and then click **Next**.</span></span>
14. <span data-ttu-id="3b7c0-138">Выберите базу данных для резервного копирования в Azure и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3b7c0-138">Choose the database that you want to back up to Azure, and then click **Next**.</span></span> <span data-ttu-id="3b7c0-139">Например:</span><span class="sxs-lookup"><span data-stu-id="3b7c0-139">For example:</span></span>

    ![Выбор оперативной защиты данных](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. <span data-ttu-id="3b7c0-141">Определите расписание для **службы архивации Azure** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3b7c0-141">Define the schedule for **Azure Backup**, and then click **Next**.</span></span> <span data-ttu-id="3b7c0-142">Например:</span><span class="sxs-lookup"><span data-stu-id="3b7c0-142">For example:</span></span>

    ![Выбор расписания оперативного резервного копирования](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="3b7c0-144">Обратите внимание, что точки оперативного восстановления создаются на основании точек быстрого полного восстановления.</span><span class="sxs-lookup"><span data-stu-id="3b7c0-144">Note Online recovery points are based on express full recovery points.</span></span> <span data-ttu-id="3b7c0-145">Таким образом, в расписании резервного копирования нужно указать, что точки оперативного восстановления должны создаваться после точек быстрого полного восстановления.</span><span class="sxs-lookup"><span data-stu-id="3b7c0-145">Therefore, you must schedule the online recovery point after the time that’s specified for the express full recovery point.</span></span>
    >
    >
16. <span data-ttu-id="3b7c0-146">Настройте политику хранения для **службы архивации Azure** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3b7c0-146">Configure the retention policy for **Azure Backup**, and then click **Next**.</span></span>
17. <span data-ttu-id="3b7c0-147">Выберите параметр оперативной репликации и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3b7c0-147">Choose an online replication option and click **Next**.</span></span>

    <span data-ttu-id="3b7c0-148">Если база данных имеет большой размер, процедура создания первой резервной копии по сети может занять много времени.</span><span class="sxs-lookup"><span data-stu-id="3b7c0-148">If you have a large database, it could take a long time for the initial backup to be created over the network.</span></span> <span data-ttu-id="3b7c0-149">Чтобы избежать этого, можно создать автономную резервную копию.</span><span class="sxs-lookup"><span data-stu-id="3b7c0-149">To avoid this issue, you can create an offline backup.</span></span>  

    ![Выбор политики оперативного хранения](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. <span data-ttu-id="3b7c0-151">Проверьте параметры и щелкните **Создать группу**.</span><span class="sxs-lookup"><span data-stu-id="3b7c0-151">Confirm the settings, and then click **Create Group**.</span></span>
19. <span data-ttu-id="3b7c0-152">Нажмите кнопку **Закрыть**</span><span class="sxs-lookup"><span data-stu-id="3b7c0-152">Click **Close**.</span></span>

## <a name="recover-the-exchange-database"></a><span data-ttu-id="3b7c0-153">Восстановление базы данных Exchange</span><span class="sxs-lookup"><span data-stu-id="3b7c0-153">Recover the Exchange database</span></span>
1. <span data-ttu-id="3b7c0-154">Чтобы восстановить базу данных Exchange, щелкните **Восстановление** в консоли администратора MABS.</span><span class="sxs-lookup"><span data-stu-id="3b7c0-154">To recover an Exchange database, click **Recovery** in the MABS Administrator Console.</span></span>
2. <span data-ttu-id="3b7c0-155">Выберите базу данных Exchange, которую требуется восстановить.</span><span class="sxs-lookup"><span data-stu-id="3b7c0-155">Locate the Exchange database that you want to recover.</span></span>
3. <span data-ttu-id="3b7c0-156">Выберите точку оперативного восстановления из раскрывающегося списка *Время восстановления* .</span><span class="sxs-lookup"><span data-stu-id="3b7c0-156">Select an online recovery point from the *recovery time* drop-down list.</span></span>
4. <span data-ttu-id="3b7c0-157">Щелкните **Восстановить**, чтобы запустить **мастер восстановления**.</span><span class="sxs-lookup"><span data-stu-id="3b7c0-157">Click **Recover** to start the **Recovery Wizard**.</span></span>

<span data-ttu-id="3b7c0-158">Для точек оперативного восстановления существует пять типов восстановления:</span><span class="sxs-lookup"><span data-stu-id="3b7c0-158">For online recovery points, there are five recovery types:</span></span>

* <span data-ttu-id="3b7c0-159">**Восстановить в исходное расположение сервера Exchange.** Данные будут восстановлены на исходный сервер Exchange Server.</span><span class="sxs-lookup"><span data-stu-id="3b7c0-159">**Recover to original Exchange Server location:** The data will be recovered to the original Exchange server.</span></span>
* <span data-ttu-id="3b7c0-160">**Восстановить в другую базу данных на сервере Exchange.** Данные будут восстановлены в другую базу данных на другом сервере Exchange Server.</span><span class="sxs-lookup"><span data-stu-id="3b7c0-160">**Recover to another database on an Exchange Server:** The data will be recovered to another database on another Exchange server.</span></span>
* <span data-ttu-id="3b7c0-161">**Восстановить в базу данных восстановления.** Данные будут восстановлены в базу данных восстановления Exchange (RDB).</span><span class="sxs-lookup"><span data-stu-id="3b7c0-161">**Recover to a Recovery Database:** The data will be recovered to an Exchange Recovery Database (RDB).</span></span>
* <span data-ttu-id="3b7c0-162">**Копировать в сетевую папку.** Данные будут восстановлены в сетевую папку.</span><span class="sxs-lookup"><span data-stu-id="3b7c0-162">**Copy to a network folder:** The data will be recovered to a network folder.</span></span>
* <span data-ttu-id="3b7c0-163">**Копировать на ленту.** Если на сервере MABS подключена и настроена ленточная библиотека или изолированный ленточный накопитель, то точка восстановления будет скопирована на свободную ленту.</span><span class="sxs-lookup"><span data-stu-id="3b7c0-163">**Copy to tape:** If you have a tape library or a stand-alone tape drive attached and configured on MABS, the recovery point will be copied to a free tape.</span></span>

    ![Выбор оперативной репликации](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a><span data-ttu-id="3b7c0-165">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3b7c0-165">Next steps</span></span>
* [<span data-ttu-id="3b7c0-166">Часто задаваемые вопросы о службе архивации Azure</span><span class="sxs-lookup"><span data-stu-id="3b7c0-166">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
