---
title: "Управление хранилищами и серверами службы архивации Azure с помощью классической модели развертывания | Документация Майкрософт"
description: "Используйте этот учебник, чтобы узнать, как управлять хранилищами и серверами службы архивации Azure."
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
ms.openlocfilehash: 91451b2cdc42ed05ef7c1ba9c66ad5b4b45dd788
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-backup-vaults-and-servers-using-the-classic-deployment-model"></a><span data-ttu-id="f0df0-103">Управление хранилищами и серверами службы архивации Azure с помощью классической модели развертывания</span><span class="sxs-lookup"><span data-stu-id="f0df0-103">Manage Azure Backup vaults and servers using the classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f0df0-104">Диспетчер ресурсов</span><span class="sxs-lookup"><span data-stu-id="f0df0-104">Resource Manager</span></span>](backup-azure-manage-windows-server.md)
> * [<span data-ttu-id="f0df0-105">Классический</span><span class="sxs-lookup"><span data-stu-id="f0df0-105">Classic</span></span>](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="f0df0-106">В этой статье представлен обзор задач управления резервным копированием, которые можно выполнять на классическом портале Azure и с помощью агента службы архивации Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f0df0-106">In this article you'll find an overview of the backup management tasks available through the Azure classic portal and the Microsoft Azure Backup agent.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f0df0-107">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f0df0-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f0df0-108">В этой статье рассматривается использование классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="f0df0-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="f0df0-109">Для большинства новых развертываний Майкрософт рекомендует использовать модель диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f0df0-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f0df0-110">Теперь вы можете обновить свои резервные хранилища до хранилищ служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="f0df0-110">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="f0df0-111">См. дополнительные сведения об [обновлении резервного хранилища до хранилища служб восстановления](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="f0df0-111">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="f0df0-112">Корпорация Майкрософт рекомендует обновить резервные хранилища до хранилищ служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="f0df0-112">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="f0df0-113">После 15 октября 2017 года вы не сможете использовать PowerShell для создания резервных хранилищ.</span><span class="sxs-lookup"><span data-stu-id="f0df0-113">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="f0df0-114">**К 1 ноября 2017 года**:</span><span class="sxs-lookup"><span data-stu-id="f0df0-114">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="f0df0-115">Все остальные резервные хранилища будут автоматически обновлены до хранилищ служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="f0df0-115">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="f0df0-116">Вы не сможете получить доступ к данным резервных копий на классическом портале.</span><span class="sxs-lookup"><span data-stu-id="f0df0-116">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="f0df0-117">Вместо этого для доступа к данным резервных копий в хранилищах служб восстановления используйте портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f0df0-117">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="management-portal-tasks"></a><span data-ttu-id="f0df0-118">Задачи на портале управления</span><span class="sxs-lookup"><span data-stu-id="f0df0-118">Management portal tasks</span></span>
1. <span data-ttu-id="f0df0-119">Выполните вход на [Портал управления](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="f0df0-119">Sign in to the [Management Portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="f0df0-120">Щелкните **Службы восстановления**и выберите имя хранилища архивации, чтобы просмотреть соответствующую страницу «Быстрый запуск».</span><span class="sxs-lookup"><span data-stu-id="f0df0-120">Click **Recovery Services**, then click the name of backup vault to view the Quick Start page.</span></span>

    ![Службы восстановления](./media/backup-azure-manage-windows-server-classic/rs-left-nav.png)

<span data-ttu-id="f0df0-122">Выбирая параметры в верхней части страницы быстрого запуска, можно просмотреть доступные задачи управления.</span><span class="sxs-lookup"><span data-stu-id="f0df0-122">By selecting the options at the top of the Quick Start page, you can see the available management tasks.</span></span>

![Управление вкладками](./media/backup-azure-manage-windows-server-classic/qs-page.png)

### <a name="dashboard"></a><span data-ttu-id="f0df0-124">Панель мониторинга</span><span class="sxs-lookup"><span data-stu-id="f0df0-124">Dashboard</span></span>
<span data-ttu-id="f0df0-125">Щелкните **Панель мониторинга** , чтобы посмотреть обзор использования сервера.</span><span class="sxs-lookup"><span data-stu-id="f0df0-125">Select **Dashboard** to see the usage overview for the server.</span></span> <span data-ttu-id="f0df0-126">В разделе **Обзор использования** представлены следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="f0df0-126">The **usage overview** includes:</span></span>

* <span data-ttu-id="f0df0-127">Количество серверов Windows Server, зарегистрированных в облаке</span><span class="sxs-lookup"><span data-stu-id="f0df0-127">The number of Windows Servers registered to cloud</span></span>
* <span data-ttu-id="f0df0-128">Количество виртуальных машин Azure, защищенных в облаке</span><span class="sxs-lookup"><span data-stu-id="f0df0-128">The number of Azure virtual machines protected in cloud</span></span>
* <span data-ttu-id="f0df0-129">Общий объем занятого хранилища в Azure</span><span class="sxs-lookup"><span data-stu-id="f0df0-129">The total storage consumed in Azure</span></span>
* <span data-ttu-id="f0df0-130">Состояние последних заданий</span><span class="sxs-lookup"><span data-stu-id="f0df0-130">The status of recent jobs</span></span>

<span data-ttu-id="f0df0-131">Вот какие задачи можно выполнять в нижней части панели мониторинга:</span><span class="sxs-lookup"><span data-stu-id="f0df0-131">At the bottom of the Dashboard you can perform the following tasks:</span></span>

* <span data-ttu-id="f0df0-132">**Управление сертификатом** — если для регистрации сервера использовался сертификат, применяйте эту функцию для обновления сертификата.</span><span class="sxs-lookup"><span data-stu-id="f0df0-132">**Manage certificate** - If a certificate was used to register the server, then use this to update the certificate.</span></span> <span data-ttu-id="f0df0-133">При использовании учетных данных хранилища не используйте пункт **Управление сертификатом**.</span><span class="sxs-lookup"><span data-stu-id="f0df0-133">If you are using vault credentials, do not use **Manage certificate**.</span></span>
* <span data-ttu-id="f0df0-134">**Удаление** — удаляет текущее хранилище резервных копий.</span><span class="sxs-lookup"><span data-stu-id="f0df0-134">**Delete** - Deletes the current backup vault.</span></span> <span data-ttu-id="f0df0-135">Если хранилище архивации больше не используется, его можно удалить для освобождения места.</span><span class="sxs-lookup"><span data-stu-id="f0df0-135">If a backup vault is no longer being used, you can delete it to free up storage space.</span></span> <span data-ttu-id="f0df0-136">**Удаление** становится доступен только после удаления из хранилища всех зарегистрированных серверов.</span><span class="sxs-lookup"><span data-stu-id="f0df0-136">**Delete** is only enabled after all registered servers have been deleted from the vault.</span></span>

![Задачи панели мониторинга архивации](./media/backup-azure-manage-windows-server-classic/dashboard-tasks.png)

## <a name="registered-items"></a><span data-ttu-id="f0df0-138">Зарегистрированные элементы</span><span class="sxs-lookup"><span data-stu-id="f0df0-138">Registered items</span></span>
<span data-ttu-id="f0df0-139">Щелкните **Зарегистрированные элементы** для просмотра имен серверов, зарегистрированных в этом хранилище.</span><span class="sxs-lookup"><span data-stu-id="f0df0-139">Select **Registered Items** to view the names of the servers that are registered to this vault.</span></span>

![Зарегистрированные элементы](./media/backup-azure-manage-windows-server-classic/registered-items.png)

<span data-ttu-id="f0df0-141">Для фильтра **Тип** по умолчанию установлено значение "Виртуальная машина Azure".</span><span class="sxs-lookup"><span data-stu-id="f0df0-141">The **Type** filter defaults to Azure Virtual Machine.</span></span> <span data-ttu-id="f0df0-142">Для просмотра имен серверов, зарегистрированных в этом хранилище, из раскрывающегося меню выберите **Windows Server** .</span><span class="sxs-lookup"><span data-stu-id="f0df0-142">To view the names of the servers that are registered to this vault, select **Windows server** from the drop down menu.</span></span>

<span data-ttu-id="f0df0-143">Отсюда можно выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="f0df0-143">From here you can perform the following tasks:</span></span>

* <span data-ttu-id="f0df0-144">**Разрешить повторную регистрацию** — когда для сервера выбран этот параметр, можно воспользоваться **мастером регистрации**, доступным в локальном агенте службы архивации Microsoft Azure, чтобы зарегистрировать сервер в хранилище резервных копий во второй раз.</span><span class="sxs-lookup"><span data-stu-id="f0df0-144">**Allow Re-registration** - When this option is selected for a server you can use the **Registration Wizard** in the on-premises Microsoft Azure Backup agent to register the server with the backup vault a second time.</span></span> <span data-ttu-id="f0df0-145">Повторная регистрация может потребоваться из-за ошибки в сертификате или перестроения сервера.</span><span class="sxs-lookup"><span data-stu-id="f0df0-145">You might need to re-register due to an error in the certificate or if a server had to be rebuilt.</span></span>
* <span data-ttu-id="f0df0-146">**Удалить** — удаляет сервер из хранилища архивации.</span><span class="sxs-lookup"><span data-stu-id="f0df0-146">**Delete** - Deletes a server from the backup vault.</span></span> <span data-ttu-id="f0df0-147">Все сохраненные данные, связанные с этим сервером, сразу же удаляются.</span><span class="sxs-lookup"><span data-stu-id="f0df0-147">All of the stored data associated with the server is deleted immediately.</span></span>

    ![Задачи зарегистрированных элементов](./media/backup-azure-manage-windows-server-classic/registered-items-tasks.png)

## <a name="protected-items"></a><span data-ttu-id="f0df0-149">Защищенные элементы</span><span class="sxs-lookup"><span data-stu-id="f0df0-149">Protected items</span></span>
<span data-ttu-id="f0df0-150">Щелкните **Защищенные элементы** для просмотра элементов, заархивированных с серверов.</span><span class="sxs-lookup"><span data-stu-id="f0df0-150">Select **Protected Items** to view the items that have been backed up from the servers.</span></span>

![Защищенные элементы](./media/backup-azure-manage-windows-server-classic/protected-items.png)

## <a name="configure"></a><span data-ttu-id="f0df0-152">Настройка</span><span class="sxs-lookup"><span data-stu-id="f0df0-152">Configure</span></span>
<span data-ttu-id="f0df0-153">На вкладке **Настройка** можно задать соответствующие параметры избыточности хранилища.</span><span class="sxs-lookup"><span data-stu-id="f0df0-153">From the **Configure** tab you can select the appropriate storage redundancy option.</span></span> <span data-ttu-id="f0df0-154">Лучше выбирать параметры избыточности хранилища сразу после его создания и до регистрации в нем компьютеров.</span><span class="sxs-lookup"><span data-stu-id="f0df0-154">The best time to select the storage redundancy option is right after creating a vault and before any machines are registered to it.</span></span>

> [!WARNING]
> <span data-ttu-id="f0df0-155">После регистрации элемента в хранилище параметр избыточности хранилища блокируется и в последствии не может быть изменен.</span><span class="sxs-lookup"><span data-stu-id="f0df0-155">Once an item has been registered to the vault, the storage redundancy option is locked and cannot be modified.</span></span>
>
>

![Настройка](./media/backup-azure-manage-windows-server-classic/configure.png)

<span data-ttu-id="f0df0-157">Дополнительные сведения см. в статье об [избыточности хранилища](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="f0df0-157">See this article for more information about [storage redundancy](../storage/common/storage-redundancy.md).</span></span>

## <a name="microsoft-azure-backup-agent-tasks"></a><span data-ttu-id="f0df0-158">Задачи агента службы архивации Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="f0df0-158">Microsoft Azure Backup agent tasks</span></span>
### <a name="console"></a><span data-ttu-id="f0df0-159">Консоль</span><span class="sxs-lookup"><span data-stu-id="f0df0-159">Console</span></span>
<span data-ttu-id="f0df0-160">Откройте **агент службы архивации Microsoft Azure** (чтобы найти его, введите *Служба архивации Microsoft Azure*в строке поиска на своем компьютере).</span><span class="sxs-lookup"><span data-stu-id="f0df0-160">Open the **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![Агент службы архивации](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)

<span data-ttu-id="f0df0-162">В разделе **Действия** в правой части консоли агента службы архивации можно выполнять следующие задачи управления:</span><span class="sxs-lookup"><span data-stu-id="f0df0-162">From the **Actions** available at the right of the backup agent console you can perform the following management tasks:</span></span>

* <span data-ttu-id="f0df0-163">Регистрация сервера</span><span class="sxs-lookup"><span data-stu-id="f0df0-163">Register Server</span></span>
* <span data-ttu-id="f0df0-164">Создание расписания архивации</span><span class="sxs-lookup"><span data-stu-id="f0df0-164">Schedule Backup</span></span>
* <span data-ttu-id="f0df0-165">Выполнить архивацию сейчас</span><span class="sxs-lookup"><span data-stu-id="f0df0-165">Back Up now</span></span>
* <span data-ttu-id="f0df0-166">Изменить свойства</span><span class="sxs-lookup"><span data-stu-id="f0df0-166">Change Properties</span></span>

![Действия в консоли агента](./media/backup-azure-manage-windows-server-classic/console-actions.png)

> [!NOTE]
> <span data-ttu-id="f0df0-168">Чтобы **восстановить данные**, ознакомьтесь со статьей [Восстановление файлов на сервере Windows Server или клиентском компьютере Windows с помощью модели развертывания Resource Manager](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="f0df0-168">To **Recover Data**, see [Restore files to a Windows server or Windows client machine](backup-azure-restore-windows-server.md).</span></span>
>
>

### <a name="modify-an-existing-backup"></a><span data-ttu-id="f0df0-169">Изменение существующего архива</span><span class="sxs-lookup"><span data-stu-id="f0df0-169">Modify an existing backup</span></span>
1. <span data-ttu-id="f0df0-170">В агенте службы архивации Microsoft Azure щелкните **Создать расписание архивации**.</span><span class="sxs-lookup"><span data-stu-id="f0df0-170">In the Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Планирование архивации Windows Server](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
2. <span data-ttu-id="f0df0-172">В **мастере архивации по расписанию** оставьте флажок **Изменить архивные элементы или время архивации** установленным и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="f0df0-172">In the **Schedule Backup Wizard** leave the **Make changes to backup items or times** option selected and click **Next**.</span></span>

    ![Изменение расписания резервного копирования](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="f0df0-174">Если нужно добавить или изменить элементы, в окне **Выбор элементов для архивации** щелкните **Добавить элементы**.</span><span class="sxs-lookup"><span data-stu-id="f0df0-174">If you want to add or change items, on the **Select Items to Backup** screen click **Add Items**.</span></span>

    <span data-ttu-id="f0df0-175">На этой странице мастера также можно задать **параметры исключений** .</span><span class="sxs-lookup"><span data-stu-id="f0df0-175">You can also set **Exclusion Settings** from this page in the wizard.</span></span> <span data-ttu-id="f0df0-176">Если нужно исключить файлы или типы файлов, ознакомьтесь с процедурой добавления [параметров исключений](#exclusion-settings).</span><span class="sxs-lookup"><span data-stu-id="f0df0-176">If you want to exclude files or file types read the procedure for adding [exclusion settings](#exclusion-settings).</span></span>
4. <span data-ttu-id="f0df0-177">Выберите файлы и папки, для которых нужно создать резервные копии, и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f0df0-177">Select the files and folders you want to back up and click **Okay**.</span></span>

    ![Добавить элементы](./media/backup-azure-manage-windows-server-classic/add-items-modify.png)
5. <span data-ttu-id="f0df0-179">Настройте **расписание архивации** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="f0df0-179">Specify the **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="f0df0-180">Вы можете запланировать ежедневное (не более трех раз в день) или еженедельное резервное копирование.</span><span class="sxs-lookup"><span data-stu-id="f0df0-180">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![Выбор расписания резервного копирования](./media/backup-azure-manage-windows-server-classic/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > <span data-ttu-id="f0df0-182">Дополнительные сведения о настройке расписания архивации см. в [этой статье](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="f0df0-182">Specifying the backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >
6. <span data-ttu-id="f0df0-183">Выберите **политику хранения** для резервных копий и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="f0df0-183">Select the **Retention Policy** for the backup copy and click **Next**.</span></span>

    ![Определение политики хранения](./media/backup-azure-manage-windows-server-classic/select-retention-policy-modify.png)
7. <span data-ttu-id="f0df0-185">Проверьте сведения в окне **Подтверждение** и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="f0df0-185">On the **Confirmation** screen review the information and click **Finish**.</span></span>
8. <span data-ttu-id="f0df0-186">Когда мастер завершит создание **расписания архивации**, нажмите кнопку **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="f0df0-186">Once the wizard finishes creating the **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="f0df0-187">После изменения защиты можно проверить, своевременно ли запускается архивация. Для этого перейдите на вкладку **Задания** и убедитесь, что изменения отражаются в заданиях архивации.</span><span class="sxs-lookup"><span data-stu-id="f0df0-187">After modifying protection, you can confirm that backups are triggering correctly by going to the **Jobs** tab and confirming that changes are reflected in the backup jobs.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="f0df0-188">Включение регулирования сети</span><span class="sxs-lookup"><span data-stu-id="f0df0-188">Enable Network Throttling</span></span>
<span data-ttu-id="f0df0-189">В агенте службы архивации Azure есть вкладка "Регулирование", которая позволяет управлять использованием пропускной способности сети при передаче данных.</span><span class="sxs-lookup"><span data-stu-id="f0df0-189">The Azure Backup agent provides a Throttling tab which allows you to control how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="f0df0-190">Это полезно, если вам нужно выполнить архивацию в рабочее время так, чтобы операция копирования не мешала другим процессам, связанным с обработкой интернет-трафика.</span><span class="sxs-lookup"><span data-stu-id="f0df0-190">This control can be helpful if you need to back up data during work hours but do not want the backup process to interfere with other internet traffic.</span></span> <span data-ttu-id="f0df0-191">Регулирование передачи данных применяется при резервном копировании и восстановлении.</span><span class="sxs-lookup"><span data-stu-id="f0df0-191">Throttling of data transfer applies to back up and restore activities.</span></span>  

<span data-ttu-id="f0df0-192">Чтобы включить регулирование:</span><span class="sxs-lookup"><span data-stu-id="f0df0-192">To enable throttling:</span></span>

1. <span data-ttu-id="f0df0-193">В **агенте архивации** щелкните **Изменить свойства**.</span><span class="sxs-lookup"><span data-stu-id="f0df0-193">In the **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="f0df0-194">Установите флажок **Разрешить регулирование уровня использования пропускной способности канала для операций резервного копирования** .</span><span class="sxs-lookup"><span data-stu-id="f0df0-194">Select the **Enable internet bandwidth usage throttling for backup operations** checkbox.</span></span>

    ![Регулирование сети](./media/backup-azure-manage-windows-server-classic/throttling-dialog.png)
3. <span data-ttu-id="f0df0-196">После включения регулирования укажите допустимую пропускную способность для передачи данных во время архивации в **рабочее** и **нерабочее** время.</span><span class="sxs-lookup"><span data-stu-id="f0df0-196">Once you have enabled throttling, specify the allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="f0df0-197">Значения пропускной способности начинаются с 512 килобит в секунду (Кбит/с) и могут перейти до 1023 мегабит в секунду (Мбит/с).</span><span class="sxs-lookup"><span data-stu-id="f0df0-197">The bandwidth values begin at 512 kilobytes per second (Kbps) and can go up to 1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="f0df0-198">Можно также назначить время начала и окончания для **рабочих часов**и выбрать, какие дни недели считаются рабочими.</span><span class="sxs-lookup"><span data-stu-id="f0df0-198">You can also designate the start and finish for **Work hours**, and which days of the week are considered Work days.</span></span> <span data-ttu-id="f0df0-199">Время вне назначенных рабочих часов считается нерабочим.</span><span class="sxs-lookup"><span data-stu-id="f0df0-199">The time outside of the designated Work hours is considered to be non-work hours.</span></span>
4. <span data-ttu-id="f0df0-200">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f0df0-200">Click **OK**.</span></span>

## <a name="exclusion-settings"></a><span data-ttu-id="f0df0-201">параметры исключений</span><span class="sxs-lookup"><span data-stu-id="f0df0-201">Exclusion settings</span></span>
1. <span data-ttu-id="f0df0-202">Откройте **агент службы архивации Microsoft Azure** (чтобы найти его, введите *Служба архивации Microsoft Azure*в строке поиска на своем компьютере).</span><span class="sxs-lookup"><span data-stu-id="f0df0-202">Open the **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![Открытие агента службы архивации](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)
2. <span data-ttu-id="f0df0-204">В агенте службы архивации Microsoft Azure щелкните **Создать расписание архивации**.</span><span class="sxs-lookup"><span data-stu-id="f0df0-204">In the Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Планирование архивации Windows Server](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
3. <span data-ttu-id="f0df0-206">В мастере архивации по расписанию оставьте флажок **Изменить архивные элементы или время архивации** установленным и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="f0df0-206">In the Schedule Backup Wizard leave the **Make changes to backup items or times** option selected and click **Next**.</span></span>

    ![Изменение расписания](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="f0df0-208">Щелкните **Параметры исключений**.</span><span class="sxs-lookup"><span data-stu-id="f0df0-208">Click **Exclusions Settings**.</span></span>

    ![Выбор элементов для исключения](./media/backup-azure-manage-windows-server-classic/exclusion-settings.png)
5. <span data-ttu-id="f0df0-210">Щелкните **Добавить исключение**.</span><span class="sxs-lookup"><span data-stu-id="f0df0-210">Click **Add Exclusion**.</span></span>

    ![Добавление исключений](./media/backup-azure-manage-windows-server-classic/add-exclusion.png)
6. <span data-ttu-id="f0df0-212">Выберите расположение и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f0df0-212">Select the location and then, click **OK**.</span></span>

    ![Выбор расположения для исключения](./media/backup-azure-manage-windows-server-classic/exclusion-location.png)
7. <span data-ttu-id="f0df0-214">Добавьте расширение файла в поле **Тип файла** .</span><span class="sxs-lookup"><span data-stu-id="f0df0-214">Add the file extension in the **File Type** field.</span></span>

    ![Исключение по типу файлов](./media/backup-azure-manage-windows-server-classic/exclude-file-type.png)

    <span data-ttu-id="f0df0-216">Добавление расширения .mp3</span><span class="sxs-lookup"><span data-stu-id="f0df0-216">Adding an .mp3 extension</span></span>

    ![Пример типа файлов](./media/backup-azure-manage-windows-server-classic/exclude-mp3.png)

    <span data-ttu-id="f0df0-218">Чтобы добавить другое расширение, нажмите кнопку **Добавить исключение** и введите другое расширение имени файла (ниже показано добавление расширения JPEG).</span><span class="sxs-lookup"><span data-stu-id="f0df0-218">To add another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![Другой пример типа файла](./media/backup-azure-manage-windows-server-classic/exclude-jpg.png)
8. <span data-ttu-id="f0df0-220">После добавления всех расширений нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f0df0-220">When you've added all the extensions, click **OK**.</span></span>
9. <span data-ttu-id="f0df0-221">Продолжайте выполнять указания мастера архивации по расписанию, нажимая кнопку **Далее**, пока не откроется **страница подтверждения**. После этого нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="f0df0-221">Continue through the Schedule Backup Wizard by clicking **Next** until the **Confirmation page**, then click **Finish**.</span></span>

    ![Подтверждение исключения](./media/backup-azure-manage-windows-server-classic/finish-exclusions.png)

## <a name="next-steps"></a><span data-ttu-id="f0df0-223">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f0df0-223">Next steps</span></span>
* [<span data-ttu-id="f0df0-224">Восстановление Windows Server или клиента Windows из Azure</span><span class="sxs-lookup"><span data-stu-id="f0df0-224">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="f0df0-225">Дополнительную информацию о службе архивации Azure см. в статье [Обзор службы архивации Azure](backup-introduction-to-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="f0df0-225">To learn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="f0df0-226">Посетите [форум о службе архивации Azure](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="f0df0-226">Visit the [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>
