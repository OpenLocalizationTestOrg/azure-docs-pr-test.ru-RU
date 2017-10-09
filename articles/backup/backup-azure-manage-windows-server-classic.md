---
title: "aaaManage Azure резервных хранилищ и серверов Azure с помощью hello классической модели развертывания | Документы Microsoft"
description: "Используйте этот учебник toolearn как хранилищ toomanage резервного копирования Azure и серверы."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: f175eb12-0905-437f-91fd-eaee03ab6e81
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: markgal;
ms.openlocfilehash: 6c38b04f4a76604bfd639a9b2d58237ce44e2386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-backup-vaults-and-servers-using-hello-classic-deployment-model"></a><span data-ttu-id="24706-103">Управление хранилищами резервного копирования Azure и серверами с помощью hello классической модели развертывания</span><span class="sxs-lookup"><span data-stu-id="24706-103">Manage Azure Backup vaults and servers using hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="24706-104">Диспетчер ресурсов</span><span class="sxs-lookup"><span data-stu-id="24706-104">Resource Manager</span></span>](backup-azure-manage-windows-server.md)
> * [<span data-ttu-id="24706-105">Классический</span><span class="sxs-lookup"><span data-stu-id="24706-105">Classic</span></span>](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="24706-106">В этой статье вы найдете Обзор задачи управления резервным копированием hello, доступные через hello классический портал Azure и агент службы архивации Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="24706-106">In this article you'll find an overview of hello backup management tasks available through hello Azure classic portal and hello Microsoft Azure Backup agent.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="24706-107">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="24706-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="24706-108">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="24706-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="24706-109">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="24706-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="24706-110">Теперь можно обновить вашими хранилищами служб tooRecovery хранилища резервной копии.</span><span class="sxs-lookup"><span data-stu-id="24706-110">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="24706-111">Дополнительные сведения см. в статье hello [обновление tooa хранилища резервной копии, в хранилище служб восстановления](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="24706-111">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="24706-112">Корпорация Майкрософт рекомендует tooupgrade вашей резервных хранилищ tooRecovery хранилищами служб.</span><span class="sxs-lookup"><span data-stu-id="24706-112">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="24706-113">После 15 октября 2017 г. нельзя использовать PowerShell toocreate резервное копирование хранилищ.</span><span class="sxs-lookup"><span data-stu-id="24706-113">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="24706-114">**К 1 ноября 2017 года**:</span><span class="sxs-lookup"><span data-stu-id="24706-114">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="24706-115">Все оставшиеся хранилища резервной копии будет автоматически обновленные tooRecovery хранилищами служб.</span><span class="sxs-lookup"><span data-stu-id="24706-115">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="24706-116">Вы не будет возможности tooaccess данные резервной копии hello классического портала.</span><span class="sxs-lookup"><span data-stu-id="24706-116">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="24706-117">Вместо этого используйте hello Azure портала tooaccess резервного копирования данных в хранилищах службы восстановления.</span><span class="sxs-lookup"><span data-stu-id="24706-117">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="management-portal-tasks"></a><span data-ttu-id="24706-118">Задачи на портале управления</span><span class="sxs-lookup"><span data-stu-id="24706-118">Management portal tasks</span></span>
1. <span data-ttu-id="24706-119">Войдите в toohello [портала управления](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="24706-119">Sign in toohello [Management Portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="24706-120">Нажмите кнопку **службы восстановления**, затем щелкните имя hello страницы быстрый запуск резервного хранилища tooview hello.</span><span class="sxs-lookup"><span data-stu-id="24706-120">Click **Recovery Services**, then click hello name of backup vault tooview hello Quick Start page.</span></span>

    ![Службы восстановления](./media/backup-azure-manage-windows-server-classic/rs-left-nav.png)

<span data-ttu-id="24706-122">Выбрав параметры hello hello верхней части страницы быстрого запуска hello, вы увидите hello доступных задач управления.</span><span class="sxs-lookup"><span data-stu-id="24706-122">By selecting hello options at hello top of hello Quick Start page, you can see hello available management tasks.</span></span>

![Управление вкладками](./media/backup-azure-manage-windows-server-classic/qs-page.png)

### <a name="dashboard"></a><span data-ttu-id="24706-124">Панель мониторинга</span><span class="sxs-lookup"><span data-stu-id="24706-124">Dashboard</span></span>
<span data-ttu-id="24706-125">Выберите **мониторинга** toosee hello Общие сведения об использовании для сервера hello.</span><span class="sxs-lookup"><span data-stu-id="24706-125">Select **Dashboard** toosee hello usage overview for hello server.</span></span> <span data-ttu-id="24706-126">Hello **Общие сведения об использовании** включает в себя:</span><span class="sxs-lookup"><span data-stu-id="24706-126">hello **usage overview** includes:</span></span>

* <span data-ttu-id="24706-127">toocloud зарегистрировано Hello количество серверов Windows</span><span class="sxs-lookup"><span data-stu-id="24706-127">hello number of Windows Servers registered toocloud</span></span>
* <span data-ttu-id="24706-128">число Hello Azure виртуальные машины, защищенные в облаке</span><span class="sxs-lookup"><span data-stu-id="24706-128">hello number of Azure virtual machines protected in cloud</span></span>
* <span data-ttu-id="24706-129">Hello общее занятого хранилища в Azure</span><span class="sxs-lookup"><span data-stu-id="24706-129">hello total storage consumed in Azure</span></span>
* <span data-ttu-id="24706-130">состояние последних заданий Hello</span><span class="sxs-lookup"><span data-stu-id="24706-130">hello status of recent jobs</span></span>

<span data-ttu-id="24706-131">Внизу hello hello панели мониторинга можно выполнять следующие задачи hello:</span><span class="sxs-lookup"><span data-stu-id="24706-131">At hello bottom of hello Dashboard you can perform hello following tasks:</span></span>

* <span data-ttu-id="24706-132">**Управление сертификатами** — Если сертификат был сервером используется tooregister hello, а затем использовать этот сертификат tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="24706-132">**Manage certificate** - If a certificate was used tooregister hello server, then use this tooupdate hello certificate.</span></span> <span data-ttu-id="24706-133">При использовании учетных данных хранилища не используйте пункт **Управление сертификатом**.</span><span class="sxs-lookup"><span data-stu-id="24706-133">If you are using vault credentials, do not use **Manage certificate**.</span></span>
* <span data-ttu-id="24706-134">**Удалить** -удалений hello текущего резервного хранилища.</span><span class="sxs-lookup"><span data-stu-id="24706-134">**Delete** - Deletes hello current backup vault.</span></span> <span data-ttu-id="24706-135">Если резервное хранилище больше не используется, ее можно удалить toofree места хранения.</span><span class="sxs-lookup"><span data-stu-id="24706-135">If a backup vault is no longer being used, you can delete it toofree up storage space.</span></span> <span data-ttu-id="24706-136">**Удалить** доступна только после удаления из хранилища hello все зарегистрированные серверы.</span><span class="sxs-lookup"><span data-stu-id="24706-136">**Delete** is only enabled after all registered servers have been deleted from hello vault.</span></span>

![Задачи панели мониторинга архивации](./media/backup-azure-manage-windows-server-classic/dashboard-tasks.png)

## <a name="registered-items"></a><span data-ttu-id="24706-138">Зарегистрированные элементы</span><span class="sxs-lookup"><span data-stu-id="24706-138">Registered items</span></span>
<span data-ttu-id="24706-139">Выберите **зарегистрированные элементы** зарегистрировать имена hello tooview hello серверов, которые являются toothis хранилища.</span><span class="sxs-lookup"><span data-stu-id="24706-139">Select **Registered Items** tooview hello names of hello servers that are registered toothis vault.</span></span>

![Зарегистрированные элементы](./media/backup-azure-manage-windows-server-classic/registered-items.png)

<span data-ttu-id="24706-141">Hello **тип** фильтра по умолчанию tooAzure виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="24706-141">hello **Type** filter defaults tooAzure Virtual Machine.</span></span> <span data-ttu-id="24706-142">Выберите имена hello tooview hello серверов, которые являются хранилище зарегистрированного toothis **Windows server** из hello раскрывающемся меню.</span><span class="sxs-lookup"><span data-stu-id="24706-142">tooview hello names of hello servers that are registered toothis vault, select **Windows server** from hello drop down menu.</span></span>

<span data-ttu-id="24706-143">Здесь можно выполнять следующие задачи hello.</span><span class="sxs-lookup"><span data-stu-id="24706-143">From here you can perform hello following tasks:</span></span>

* <span data-ttu-id="24706-144">**Разрешить повторную регистрацию** — при выборе этого параметра для сервера, можно использовать hello **мастер регистрации** hello локальной службы архивации Microsoft Azure агента tooregister hello Server с резервным хранилищем hello еще раз .</span><span class="sxs-lookup"><span data-stu-id="24706-144">**Allow Re-registration** - When this option is selected for a server you can use hello **Registration Wizard** in hello on-premises Microsoft Azure Backup agent tooregister hello server with hello backup vault a second time.</span></span> <span data-ttu-id="24706-145">Может потребоваться toore регистрацию из-за ошибки tooan в hello сертификата или если сервер имеет toobe перестроен.</span><span class="sxs-lookup"><span data-stu-id="24706-145">You might need toore-register due tooan error in hello certificate or if a server had toobe rebuilt.</span></span>
* <span data-ttu-id="24706-146">**Удалить** -удаляет сервер из резервного хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="24706-146">**Delete** - Deletes a server from hello backup vault.</span></span> <span data-ttu-id="24706-147">Немедленное удаление всех hello хранимых данных, связанных с сервером hello.</span><span class="sxs-lookup"><span data-stu-id="24706-147">All of hello stored data associated with hello server is deleted immediately.</span></span>

    ![Задачи зарегистрированных элементов](./media/backup-azure-manage-windows-server-classic/registered-items-tasks.png)

## <a name="protected-items"></a><span data-ttu-id="24706-149">Защищенные элементы</span><span class="sxs-lookup"><span data-stu-id="24706-149">Protected items</span></span>
<span data-ttu-id="24706-150">Выберите **защищенные элементы** tooview hello элементы, которые были скопированы с серверов hello.</span><span class="sxs-lookup"><span data-stu-id="24706-150">Select **Protected Items** tooview hello items that have been backed up from hello servers.</span></span>

![Защищенные элементы](./media/backup-azure-manage-windows-server-classic/protected-items.png)

## <a name="configure"></a><span data-ttu-id="24706-152">Настройка</span><span class="sxs-lookup"><span data-stu-id="24706-152">Configure</span></span>
<span data-ttu-id="24706-153">Из hello **Настройка** вкладку, можно выбрать параметр избыточности хранилища соответствующие hello.</span><span class="sxs-lookup"><span data-stu-id="24706-153">From hello **Configure** tab you can select hello appropriate storage redundancy option.</span></span> <span data-ttu-id="24706-154">Hello время tooselect hello хранилища избыточности лучше сразу же после создания хранилища, а также перед любой машин, зарегистрированных tooit.</span><span class="sxs-lookup"><span data-stu-id="24706-154">hello best time tooselect hello storage redundancy option is right after creating a vault and before any machines are registered tooit.</span></span>

> [!WARNING]
> <span data-ttu-id="24706-155">После элемента хранилища зарегистрированных toohello, параметр избыточности хранилища hello заблокирован и не может быть изменено.</span><span class="sxs-lookup"><span data-stu-id="24706-155">Once an item has been registered toohello vault, hello storage redundancy option is locked and cannot be modified.</span></span>
>
>

![Настройка](./media/backup-azure-manage-windows-server-classic/configure.png)

<span data-ttu-id="24706-157">Дополнительные сведения см. в статье об [избыточности хранилища](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="24706-157">See this article for more information about [storage redundancy](../storage/common/storage-redundancy.md).</span></span>

## <a name="microsoft-azure-backup-agent-tasks"></a><span data-ttu-id="24706-158">Задачи агента службы архивации Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="24706-158">Microsoft Azure Backup agent tasks</span></span>
### <a name="console"></a><span data-ttu-id="24706-159">Консоль</span><span class="sxs-lookup"><span data-stu-id="24706-159">Console</span></span>
<span data-ttu-id="24706-160">Откройте hello **агента службы архивации Microsoft Azure** (его можно найти путем поиска свой компьютер и *архивации Microsoft Azure*).</span><span class="sxs-lookup"><span data-stu-id="24706-160">Open hello **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![Агент службы архивации](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)

<span data-ttu-id="24706-162">Из hello **действия** найти по адресу hello правой части консоли hello резервного копирования можно выполнять следующие задачи по управлению hello:</span><span class="sxs-lookup"><span data-stu-id="24706-162">From hello **Actions** available at hello right of hello backup agent console you can perform hello following management tasks:</span></span>

* <span data-ttu-id="24706-163">Регистрация сервера</span><span class="sxs-lookup"><span data-stu-id="24706-163">Register Server</span></span>
* <span data-ttu-id="24706-164">Создание расписания архивации</span><span class="sxs-lookup"><span data-stu-id="24706-164">Schedule Backup</span></span>
* <span data-ttu-id="24706-165">Выполнить архивацию сейчас</span><span class="sxs-lookup"><span data-stu-id="24706-165">Back Up now</span></span>
* <span data-ttu-id="24706-166">Изменить свойства</span><span class="sxs-lookup"><span data-stu-id="24706-166">Change Properties</span></span>

![Действия в консоли агента](./media/backup-azure-manage-windows-server-classic/console-actions.png)

> [!NOTE]
> <span data-ttu-id="24706-168">слишком**восстановить данные**, в разделе [восстановить файлы tooa Windows server или клиентским компьютером Windows](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="24706-168">too**Recover Data**, see [Restore files tooa Windows server or Windows client machine](backup-azure-restore-windows-server.md).</span></span>
>
>

### <a name="modify-an-existing-backup"></a><span data-ttu-id="24706-169">Изменение существующего архива</span><span class="sxs-lookup"><span data-stu-id="24706-169">Modify an existing backup</span></span>
1. <span data-ttu-id="24706-170">В агенте службы архивации Microsoft Azure hello щелкните **планирования резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="24706-170">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Планирование архивации Windows Server](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
2. <span data-ttu-id="24706-172">В hello **мастер планирования резервного копирования** оставить hello **toobackup элементы или время изменения производятся** флажок и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="24706-172">In hello **Schedule Backup Wizard** leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![Изменение расписания резервного копирования](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="24706-174">Если вы tooadd или изменить элементы на hello **tooBackup выбрать элементы** откройте **добавить элементы**.</span><span class="sxs-lookup"><span data-stu-id="24706-174">If you want tooadd or change items, on hello **Select Items tooBackup** screen click **Add Items**.</span></span>

    <span data-ttu-id="24706-175">Можно также задать **параметры исключения** на этой странице приветствия мастера.</span><span class="sxs-lookup"><span data-stu-id="24706-175">You can also set **Exclusion Settings** from this page in hello wizard.</span></span> <span data-ttu-id="24706-176">Если требуется tooexclude файлы или типы файлов hello процедура добавления [параметры исключения](#exclusion-settings).</span><span class="sxs-lookup"><span data-stu-id="24706-176">If you want tooexclude files or file types read hello procedure for adding [exclusion settings](#exclusion-settings).</span></span>
4. <span data-ttu-id="24706-177">Выберите hello файлы и папки tooback вверх и щелкните **хорошо**.</span><span class="sxs-lookup"><span data-stu-id="24706-177">Select hello files and folders you want tooback up and click **Okay**.</span></span>

    ![Добавить элементы](./media/backup-azure-manage-windows-server-classic/add-items-modify.png)
5. <span data-ttu-id="24706-179">Укажите hello **расписание резервного копирования** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="24706-179">Specify hello **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="24706-180">Вы можете запланировать ежедневное (не более трех раз в день) или еженедельное резервное копирование.</span><span class="sxs-lookup"><span data-stu-id="24706-180">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![Выбор расписания резервного копирования](./media/backup-azure-manage-windows-server-classic/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > <span data-ttu-id="24706-182">Задание расписания резервного копирования hello подробно рассматривается в этом [статьи](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="24706-182">Specifying hello backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >
6. <span data-ttu-id="24706-183">Выберите hello **политики хранения** hello резервной копии и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="24706-183">Select hello **Retention Policy** for hello backup copy and click **Next**.</span></span>

    ![Определение политики хранения](./media/backup-azure-manage-windows-server-classic/select-retention-policy-modify.png)
7. <span data-ttu-id="24706-185">На hello **Подтверждение** экрана Просмотр сведений об hello и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="24706-185">On hello **Confirmation** screen review hello information and click **Finish**.</span></span>
8. <span data-ttu-id="24706-186">После завершения работы приветствия мастера создания hello **расписание резервного копирования**, нажмите кнопку **закрыть**.</span><span class="sxs-lookup"><span data-stu-id="24706-186">Once hello wizard finishes creating hello **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="24706-187">После изменения защиты, можно проверить, правильно инициируют резервных копий с переходом toohello **заданий** вкладку и подтверждения того, что изменения отражаются в hello задания резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="24706-187">After modifying protection, you can confirm that backups are triggering correctly by going toohello **Jobs** tab and confirming that changes are reflected in hello backup jobs.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="24706-188">Включение регулирования сети</span><span class="sxs-lookup"><span data-stu-id="24706-188">Enable Network Throttling</span></span>
<span data-ttu-id="24706-189">агент Azure Backup Hello предоставляет вкладку регулирование, позволяющий toocontrol использование пропускной способности сети при передаче данных.</span><span class="sxs-lookup"><span data-stu-id="24706-189">hello Azure Backup agent provides a Throttling tab which allows you toocontrol how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="24706-190">Этот элемент управления может пригодиться, если вам требуется tooback копирование данных в рабочее время, но не требуется toointerfere hello процесс резервного копирования с другими Интернет-трафика.</span><span class="sxs-lookup"><span data-stu-id="24706-190">This control can be helpful if you need tooback up data during work hours but do not want hello backup process toointerfere with other internet traffic.</span></span> <span data-ttu-id="24706-191">Регулирование данных передачи применяется tooback копирование и восстановление действий.</span><span class="sxs-lookup"><span data-stu-id="24706-191">Throttling of data transfer applies tooback up and restore activities.</span></span>  

<span data-ttu-id="24706-192">Регулирование tooenable:</span><span class="sxs-lookup"><span data-stu-id="24706-192">tooenable throttling:</span></span>

1. <span data-ttu-id="24706-193">В hello **агента резервного копирования**, нажмите кнопку **изменить свойства**.</span><span class="sxs-lookup"><span data-stu-id="24706-193">In hello **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="24706-194">Выберите hello **включить регулирования для операций резервного копирования использование пропускной способности Интернета** флажок.</span><span class="sxs-lookup"><span data-stu-id="24706-194">Select hello **Enable internet bandwidth usage throttling for backup operations** checkbox.</span></span>

    ![Регулирование сети](./media/backup-azure-manage-windows-server-classic/throttling-dialog.png)
3. <span data-ttu-id="24706-196">После включения регулирования, укажите допустимый пропускной способности, для передачи во время резервного копирования данных hello **рабочие часы** и **нерабочие часы**.</span><span class="sxs-lookup"><span data-stu-id="24706-196">Once you have enabled throttling, specify hello allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="24706-197">значения Hello пропускной способности начинаются с 512 килобайт в секунду (Кбит/с) и можно перейти вверх too1023 мегабайт в секунду (Мбит/с).</span><span class="sxs-lookup"><span data-stu-id="24706-197">hello bandwidth values begin at 512 kilobytes per second (Kbps) and can go up too1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="24706-198">Можно также назначить hello начала и окончания для **рабочие часы**, и какие дни недели hello считаются рабочих дней.</span><span class="sxs-lookup"><span data-stu-id="24706-198">You can also designate hello start and finish for **Work hours**, and which days of hello week are considered Work days.</span></span> <span data-ttu-id="24706-199">время Hello за пределами указанных рабочих часов hello — считаются toobe нерабочего времени.</span><span class="sxs-lookup"><span data-stu-id="24706-199">hello time outside of hello designated Work hours is considered toobe non-work hours.</span></span>
4. <span data-ttu-id="24706-200">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="24706-200">Click **OK**.</span></span>

## <a name="exclusion-settings"></a><span data-ttu-id="24706-201">параметры исключений</span><span class="sxs-lookup"><span data-stu-id="24706-201">Exclusion settings</span></span>
1. <span data-ttu-id="24706-202">Откройте hello **агента службы архивации Microsoft Azure** (его можно найти путем поиска свой компьютер и *архивации Microsoft Azure*).</span><span class="sxs-lookup"><span data-stu-id="24706-202">Open hello **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![Открытие агента службы архивации](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)
2. <span data-ttu-id="24706-204">В агенте службы архивации Microsoft Azure hello щелкните **планирования резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="24706-204">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Планирование архивации Windows Server](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
3. <span data-ttu-id="24706-206">В мастер планирования резервного копирования hello оставьте hello **toobackup элементы или время изменения производятся** флажок и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="24706-206">In hello Schedule Backup Wizard leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![Изменение расписания](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="24706-208">Щелкните **Параметры исключений**.</span><span class="sxs-lookup"><span data-stu-id="24706-208">Click **Exclusions Settings**.</span></span>

    ![Выберите элементы tooexclude](./media/backup-azure-manage-windows-server-classic/exclusion-settings.png)
5. <span data-ttu-id="24706-210">Щелкните **Добавить исключение**.</span><span class="sxs-lookup"><span data-stu-id="24706-210">Click **Add Exclusion**.</span></span>

    ![Добавление исключений](./media/backup-azure-manage-windows-server-classic/add-exclusion.png)
6. <span data-ttu-id="24706-212">Выберите расположение hello и затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="24706-212">Select hello location and then, click **OK**.</span></span>

    ![Выбор расположения для исключения](./media/backup-azure-manage-windows-server-classic/exclusion-location.png)
7. <span data-ttu-id="24706-214">Добавлять расширение файла hello в hello **тип файла** поля.</span><span class="sxs-lookup"><span data-stu-id="24706-214">Add hello file extension in hello **File Type** field.</span></span>

    ![Исключение по типу файлов](./media/backup-azure-manage-windows-server-classic/exclude-file-type.png)

    <span data-ttu-id="24706-216">Добавление расширения .mp3</span><span class="sxs-lookup"><span data-stu-id="24706-216">Adding an .mp3 extension</span></span>

    ![Пример типа файлов](./media/backup-azure-manage-windows-server-classic/exclude-mp3.png)

    <span data-ttu-id="24706-218">tooadd другое расширение, нажмите кнопку **Добавление исключаемых** и введите другое расширение имени файла (Добавление расширения .jpeg).</span><span class="sxs-lookup"><span data-stu-id="24706-218">tooadd another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![Другой пример типа файла](./media/backup-azure-manage-windows-server-classic/exclude-jpg.png)
8. <span data-ttu-id="24706-220">После добавления всех расширений hello, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="24706-220">When you've added all hello extensions, click **OK**.</span></span>
9. <span data-ttu-id="24706-221">Продолжайте hello мастер планирования резервного копирования, нажав кнопку **Далее** до hello **страница подтверждения**, нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="24706-221">Continue through hello Schedule Backup Wizard by clicking **Next** until hello **Confirmation page**, then click **Finish**.</span></span>

    ![Подтверждение исключения](./media/backup-azure-manage-windows-server-classic/finish-exclusions.png)

## <a name="next-steps"></a><span data-ttu-id="24706-223">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="24706-223">Next steps</span></span>
* [<span data-ttu-id="24706-224">Восстановление Windows Server или клиента Windows из Azure</span><span class="sxs-lookup"><span data-stu-id="24706-224">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="24706-225">toolearn Дополнительные сведения об архивации Azure в разделе [Обзор резервного копирования Azure](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="24706-225">toolearn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="24706-226">Посетите hello [форуме резервного копирования Azure](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="24706-226">Visit hello [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>
