---
title: "aaaManage Azure recovery services хранилищ и серверов | Документы Microsoft"
description: "Используйте этот учебник toolearn как хранилищ служб восстановления Azure toomanage и серверы."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: 4eea984b-7ed6-4600-ac60-99d2e9cb6d8a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markgal
ms.openlocfilehash: b4c35c86faa0828b3c63a13b85c095c0cbaba50e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-recovery-services-vaults-and-servers-for-windows-machines"></a><span data-ttu-id="c6ab3-103">Мониторинг хранилищ и серверов служб восстановления Azure для компьютеров Windows и управление ими</span><span class="sxs-lookup"><span data-stu-id="c6ab3-103">Monitor and manage Azure recovery services vaults and servers for Windows machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c6ab3-104">Диспетчер ресурсов</span><span class="sxs-lookup"><span data-stu-id="c6ab3-104">Resource Manager</span></span>](backup-azure-manage-windows-server.md)
> * [<span data-ttu-id="c6ab3-105">Классический</span><span class="sxs-lookup"><span data-stu-id="c6ab3-105">Classic</span></span>](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="c6ab3-106">В этой статье вы найдете Обзор hello резервного копирования монитор и управления задачи, доступные через hello hello и портал Microsoft Azure агента резервного копирования Azure.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-106">In this article you'll find an overview of hello backup monitor and management tasks available through hello Azure portal and hello Microsoft Azure Backup agent.</span></span> <span data-ttu-id="c6ab3-107">В этой статье предполагается, что у вас уже есть подписка Azure и вы создали по крайней мере одно хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-107">This article assumes you already have an Azure subscription and have created at least one Recovery Services vault.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]


## <a name="open-a-recovery-services-vault"></a><span data-ttu-id="c6ab3-108">Открытие хранилища служб восстановления</span><span class="sxs-lookup"><span data-stu-id="c6ab3-108">Open a Recovery Services vault</span></span>

<span data-ttu-id="c6ab3-109">панель мониторинга хранилища служб восстановления Hello отображаются сведения hello или атрибуты хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-109">hello Recovery Services vault dashboard shows you hello details or attributes of a Recovery Services vault.</span></span>

1. <span data-ttu-id="c6ab3-110">Войдите в toohello [портала Azure](https://portal.azure.com/) с помощью вашей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-110">Sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="c6ab3-111">Hello концентратора меню **более служб**.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-111">On hello Hub menu, click **More Services**.</span></span>

    ![Открытие списка хранилищ служб восстановления — шаг 1](./media/backup-azure-manage-windows-server/open-rs-vault-list.png) <br/>

3. <span data-ttu-id="c6ab3-113">Вы хотите tooopen хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-113">You want tooopen a Recovery Services vault.</span></span> <span data-ttu-id="c6ab3-114">В диалоговом окне приветствия начните вводить **службы восстановления**.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-114">In hello dialog box, start typing **Recovery Services**.</span></span> <span data-ttu-id="c6ab3-115">Началом ввода hello список будет отфильтрован на основе ввода.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-115">As you begin typing, hello list will filter based on your input.</span></span> <span data-ttu-id="c6ab3-116">Нажмите кнопку **хранилищ служб восстановления** toodisplay hello список служб восстановления хранилищ в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-116">Click **Recovery Services vaults** toodisplay hello list of Recovery Services vaults in your subscription.</span></span>

    ![Создание хранилища служб восстановления — шаг 1](./media/backup-azure-manage-windows-server/browse-to-rs-vaults-2.png) <br/>

    <span data-ttu-id="c6ab3-118">Откроется список Hello хранилищами служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-118">hello list of Recovery Services vaults opens.</span></span>

    ![Создание хранилища служб восстановления — шаг 1](./media/backup-azure-manage-windows-server/list-of-rs-vaults.png) <br/>

4. <span data-ttu-id="c6ab3-120">Выберите из списка hello хранилищ имя hello hello требуется tooopen хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-120">From hello list of vaults, select hello name of hello Recovery Services vault you want tooopen.</span></span> <span data-ttu-id="c6ab3-121">Открывает колонку мониторинга хранилища служб восстановления Hello.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-121">hello Recovery Services vault dashboard blade opens.</span></span>

    ![Панель мониторинга хранилища служб восстановления](./media/backup-azure-manage-windows-server/rs-vault-blade.png) <br/>

    <span data-ttu-id="c6ab3-123">Теперь, когда вы открыли хранилище служб восстановления hello, попробуйте hello задач мониторинга и управления.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-123">Now that you have opened hello Recovery Services vault, try any of hello monitoring or management tasks.</span></span>

## <a name="monitor-backup-jobs-and-alerts"></a><span data-ttu-id="c6ab3-124">Мониторинг заданий и оповещений службы архивации</span><span class="sxs-lookup"><span data-stu-id="c6ab3-124">Monitor backup jobs and alerts</span></span>

<span data-ttu-id="c6ab3-125">Контроль заданий и предупреждений из hello служб восстановления хранилище панели мониторинга, где вы видите:</span><span class="sxs-lookup"><span data-stu-id="c6ab3-125">You monitor jobs and alerts from hello Recovery Services vault dashboard, where you see:</span></span>

* <span data-ttu-id="c6ab3-126">сведения об оповещениях, связанных с архивацией;</span><span class="sxs-lookup"><span data-stu-id="c6ab3-126">Backup alerts details</span></span>
* <span data-ttu-id="c6ab3-127">Файлы и папки, а также Azure виртуальные машины, защищенные в облаке hello</span><span class="sxs-lookup"><span data-stu-id="c6ab3-127">Files and folders, as well as Azure virtual machines protected in hello cloud</span></span>
* <span data-ttu-id="c6ab3-128">сведения об общем объеме занятого хранилища в Azure;</span><span class="sxs-lookup"><span data-stu-id="c6ab3-128">Total storage consumed in Azure</span></span>
* <span data-ttu-id="c6ab3-129">состояние задания архивации.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-129">Backup job status</span></span>

![Задачи панели мониторинга архивации](./media/backup-azure-manage-windows-server/dashboard-tiles.png)

<span data-ttu-id="c6ab3-131">Сведения о hello в каждом из этих плиток открывается колонка связанного hello, где вы управляете связанные задачи.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-131">Clicking hello information in each of these tiles will open hello associated blade where you manage related tasks.</span></span>

<span data-ttu-id="c6ab3-132">С помощью hello hello панели мониторинга:</span><span class="sxs-lookup"><span data-stu-id="c6ab3-132">From hello top of hello Dashboard:</span></span>

* <span data-ttu-id="c6ab3-133">"Параметры". Здесь содержатся доступные задачи архивации.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-133">Settings provides access available backup tasks.</span></span>
* <span data-ttu-id="c6ab3-134">Резервное копирование - помогает резервное копирование новых файлов и папок (или виртуальных машинах Azure) toohello восстановления службы хранилища.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-134">Backup - helps you back up new files and folders (or Azure VMs) toohello Recovery Services vault.</span></span>
* <span data-ttu-id="c6ab3-135">DELETE — Если хранилища служб восстановления больше не используется, ее можно удалить toofree места хранения.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-135">Delete - If a recovery services vault is no longer being used, you can delete it toofree up storage space.</span></span> <span data-ttu-id="c6ab3-136">Удаление доступна только после удаления всех защищенных серверах из хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-136">Delete is only enabled after all protected servers have been deleted from hello vault.</span></span>

![Задачи панели мониторинга архивации](./media/backup-azure-manage-windows-server/dashboard-tasks.png)

## <a name="alerts-for-backups-using-azure-backup-agent"></a><span data-ttu-id="c6ab3-138">Оповещения о резервном копировании с помощью агента службы архивации Azure</span><span class="sxs-lookup"><span data-stu-id="c6ab3-138">Alerts for backups using Azure backup agent:</span></span>
| <span data-ttu-id="c6ab3-139">Уровень оповещения</span><span class="sxs-lookup"><span data-stu-id="c6ab3-139">Alert Level</span></span> | <span data-ttu-id="c6ab3-140">Отправляемые оповещения</span><span class="sxs-lookup"><span data-stu-id="c6ab3-140">Alerts sent</span></span> |
| --- | --- |
| <span data-ttu-id="c6ab3-141">критические ошибки.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-141">Critical</span></span> |<span data-ttu-id="c6ab3-142">Сбой резервного копирования, сбой восстановления</span><span class="sxs-lookup"><span data-stu-id="c6ab3-142">Backup failure, recovery failure</span></span> |
| <span data-ttu-id="c6ab3-143">Предупреждение</span><span class="sxs-lookup"><span data-stu-id="c6ab3-143">Warning</span></span> |<span data-ttu-id="c6ab3-144">Резервное копирование завершено с предупреждениями (когда не более ста не резервное копирование файлов из-за проблем с toocorruption, а резервное копирование файлов более миллиона успешно)</span><span class="sxs-lookup"><span data-stu-id="c6ab3-144">Backup completed with warnings (when fewer than one hundred files are not backed up due toocorruption issues, and more than one million files are successfully backed up)</span></span> |
| <span data-ttu-id="c6ab3-145">Информация</span><span class="sxs-lookup"><span data-stu-id="c6ab3-145">Informational</span></span> |<span data-ttu-id="c6ab3-146">None</span><span class="sxs-lookup"><span data-stu-id="c6ab3-146">None</span></span> |

## <a name="manage-backup-alerts"></a><span data-ttu-id="c6ab3-147">Управление оповещениями, связанными с архивацией</span><span class="sxs-lookup"><span data-stu-id="c6ab3-147">Manage Backup alerts</span></span>
<span data-ttu-id="c6ab3-148">Щелкните hello **оповещения резервного копирования** плитки приветствия tooopen **оповещения резервного копирования** колонке оповещений и управление ими.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-148">Click hello **Backup Alerts** tile tooopen hello **Backup Alerts** blade and manage alerts.</span></span>

![Оповещения, связанные с архивацией](./media/backup-azure-manage-windows-server/manage-backup-alerts.png)

<span data-ttu-id="c6ab3-150">Оповещения резервного копирования Hello, отражает вы hello число:</span><span class="sxs-lookup"><span data-stu-id="c6ab3-150">hello Backup Alerts tile shows you hello number of:</span></span>

* <span data-ttu-id="c6ab3-151">критических оповещений, неразрешенных в течение последних 24 часов;</span><span class="sxs-lookup"><span data-stu-id="c6ab3-151">critical alerts unresolved in last 24 hours</span></span>
* <span data-ttu-id="c6ab3-152">оповещений с предупреждениями, неразрешенных в течение последних 24 часов.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-152">warning alerts unresolved in last 24 hours</span></span>

<span data-ttu-id="c6ab3-153">Щелкнув на каждом из этих ссылок можно перейти toohello **оповещения резервного копирования** колонка с отфильтрованное представление этих оповещений ("критический" или "Предупреждение").</span><span class="sxs-lookup"><span data-stu-id="c6ab3-153">Clicking on each of these links takes you toohello **Backup Alerts** blade with a filtered view of these alerts (critical or warning).</span></span>

<span data-ttu-id="c6ab3-154">Из колонки hello оповещения резервного копирования вы:</span><span class="sxs-lookup"><span data-stu-id="c6ab3-154">From hello Backup Alerts blade, you:</span></span>

* <span data-ttu-id="c6ab3-155">Выберите tooinclude hello соответствующую информацию с предупреждениями.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-155">Choose hello appropriate information tooinclude with your alerts.</span></span>

    ![Выбор столбцов](./media/backup-azure-manage-windows-server/choose-alerts-colunms.png)
* <span data-ttu-id="c6ab3-157">Отфильтровать оповещения по уровню серьезности, состоянию и времени начала и окончания.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-157">Filter alerts for severity, status and start/end times.</span></span>

    ![Фильтрация оповещений](./media/backup-azure-manage-windows-server/filter-alerts.png)
* <span data-ttu-id="c6ab3-159">Настроить уровень серьезности, частоту и получателей оповещений, а также выключить или включить их.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-159">Configure notifications for severity, frequency and recipients, as well as turn alerts on or off.</span></span>

    ![Фильтрация оповещений](./media/backup-azure-manage-windows-server/configure-notifications.png)

<span data-ttu-id="c6ab3-161">Если **каждого предупреждения** выбран в качестве hello **уведомления** частота происходит без группирования или сокращения в сообщениях электронной почты.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-161">If **Per Alert** is selected as hello **Notify** frequency no grouping or reduction in emails occurs.</span></span> <span data-ttu-id="c6ab3-162">Для каждого оповещения создается 1 уведомление.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-162">Every alert results in 1 notification.</span></span> <span data-ttu-id="c6ab3-163">Это параметр по умолчанию hello и электронной почты hello разрешение также отправляется немедленно.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-163">This is hello default setting and hello resolution email is also sent out immediately.</span></span>

<span data-ttu-id="c6ab3-164">Если **почасовой дайджест** выбран в качестве hello **уведомления** одно электронное письмо отправляется toohello пользователя, уведомляющее о том, что частота неразрешенных новые предупреждения, созданные в hello последний час.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-164">If **Hourly Digest** is selected as hello **Notify** frequency one email is sent toohello user telling them that there are unresolved new alerts generated in hello last hour.</span></span> <span data-ttu-id="c6ab3-165">Разрешение по электронной почте отправляется в конце hello hello час.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-165">A resolution email is sent out at hello end of hello hour.</span></span>

<span data-ttu-id="c6ab3-166">Оповещения могут отправляться для hello следующие уровни серьезности:</span><span class="sxs-lookup"><span data-stu-id="c6ab3-166">Alerts can be sent for hello following severity levels:</span></span>

* <span data-ttu-id="c6ab3-167">критические ошибки.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-167">critical</span></span>
* <span data-ttu-id="c6ab3-168">Предупреждение</span><span class="sxs-lookup"><span data-stu-id="c6ab3-168">warning</span></span>
* <span data-ttu-id="c6ab3-169">информационный.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-169">information</span></span>

<span data-ttu-id="c6ab3-170">Деактивировать предупреждения hello с hello **деактивировать** кнопку в колонке сведения задания hello.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-170">You inactivate hello alert with hello **inactivate** button in hello job details blade.</span></span> <span data-ttu-id="c6ab3-171">При нажатии этой кнопки можно создать заметки о разрешении.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-171">When you click inactivate, you can provide resolution notes.</span></span>

<span data-ttu-id="c6ab3-172">Выберите столбцы hello требуется tooappear как часть hello предупреждение с hello **выбрать столбцы** кнопки.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-172">You choose hello columns you want tooappear as part of hello alert with hello **Choose columns** button.</span></span>

> [!NOTE]
> <span data-ttu-id="c6ab3-173">Из hello **параметры** колонке управления оповещения резервного копирования, выбрав **мониторинг и отчеты > оповещения и события > оповещения резервного копирования** и выбрав **фильтра** или  **Настройка уведомлений**.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-173">From hello **Settings** blade, you manage backup alerts by selecting **Monitoring and Reports > Alerts and Events > Backup Alerts** and then clicking **Filter** or **Configure Notifications**.</span></span>
>
>

## <a name="manage-backup-items"></a><span data-ttu-id="c6ab3-174">Управление архивируемыми элементами</span><span class="sxs-lookup"><span data-stu-id="c6ab3-174">Manage Backup items</span></span>
<span data-ttu-id="c6ab3-175">Управление локальных резервных копий теперь доступен на портале управления hello.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-175">Managing on-premises backups is now available in hello management portal.</span></span> <span data-ttu-id="c6ab3-176">В разделе архивации hello мониторинга hello, hello **архивных элементов** отражает hello количество элементов архивации защищенного хранилища toohello.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-176">In hello Backup section of hello dashboard, hello **Backup Items** tile shows hello number of backup items protected toohello vault.</span></span>

<span data-ttu-id="c6ab3-177">Нажмите кнопку **папки файлов** в hello, резервное копирование элементов мозаики.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-177">Click **File-Folders** in hello Backup Items tile.</span></span>

![Элемент "Архивируемые элементы"](./media/backup-azure-manage-windows-server/backup-items-tile.png)

<span data-ttu-id="c6ab3-179">Элементы для архивации Hello открывается колонка с hello фильтра tooFile папку набора показывающий каждого конкретного резервного копирования элементов в списке.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-179">hello Backup Items blade opens with hello filter set tooFile-Folder where you see each specific backup item listed.</span></span>

![Архивные элементы](./media/backup-azure-manage-windows-server/backup-item-list.png)

<span data-ttu-id="c6ab3-181">При выборе определенного элемента резервного копирования из списка hello будут отображаться hello важные сведения для этого элемента.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-181">If you select a specific backup item from hello list, you see hello essential details for that item.</span></span>

> [!NOTE]
> <span data-ttu-id="c6ab3-182">Из hello **параметры** колонке управления файлами и папками, выбрав **защищенные элементы > резервное копирование элементов** и выбрав **папки файлов** из hello раскрывающемся меню.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-182">From hello **Settings** blade, you manage files and folders by selecting **Protected Items > Backup Items** and then selecting **File-Folders** from hello drop down menu.</span></span>
>
>

![Архивируемые элементы из параметров](./media/backup-azure-manage-windows-server/backup-files-and-folders.png)

## <a name="manage-backup-jobs"></a><span data-ttu-id="c6ab3-184">Управление заданиями архивации</span><span class="sxs-lookup"><span data-stu-id="c6ab3-184">Manage Backup jobs</span></span>
<span data-ttu-id="c6ab3-185">Задания резервного копирования для локального (когда hello локальный сервер выполняет резервное копирование tooAzure) и резервных копий в Azure, отображаются в панели мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-185">Backup jobs for both on-premises (when hello on-premises server is backing up tooAzure) and Azure backups are visible in hello dashboard.</span></span>

<span data-ttu-id="c6ab3-186">В hello разделе архивации hello панели мониторинга плитки задания резервного копирования hello показан hello количество заданий:</span><span class="sxs-lookup"><span data-stu-id="c6ab3-186">In hello Backup section of hello dashboard, hello Backup job tile shows hello number of jobs:</span></span>

* <span data-ttu-id="c6ab3-187">выполняется</span><span class="sxs-lookup"><span data-stu-id="c6ab3-187">in progress</span></span>
* <span data-ttu-id="c6ab3-188">не удалось hello последние 24 часа.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-188">failed in hello last 24 hours.</span></span>

<span data-ttu-id="c6ab3-189">toomanage заданиях резервного копирования, нажмите кнопку hello **заданий резервного копирования** плитки, который открывает колонку hello задания резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-189">toomanage your backup jobs, click hello **Backup Jobs** tile, which opens hello Backup Jobs blade.</span></span>

![Архивируемые элементы из параметров](./media/backup-azure-manage-windows-server/backup-jobs.png)

<span data-ttu-id="c6ab3-191">Изменение данных hello, доступных в колонке hello заданий резервного копирования с hello **выбрать столбцы** кнопку вверху hello страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-191">You modify hello information available in hello Backup Jobs blade with hello **Choose columns** button at hello top of hello page.</span></span>

<span data-ttu-id="c6ab3-192">Используйте hello **фильтра** tooselect кнопку между файлами и папками и архивация виртуальных машин Azure.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-192">Use hello **Filter** button tooselect between Files and folders and Azure virtual machine backup.</span></span>

<span data-ttu-id="c6ab3-193">Если вы не видите резервных копий файлов и папок, нажмите кнопку **фильтра** кнопку вверху hello страницу приветствия и выберите **файлы и папки** hello тип элемента меню.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-193">If you don't see your backed up files and folders, click **Filter** button at hello top of hello page and select **Files and folders** from hello Item Type menu.</span></span>

> [!NOTE]
> <span data-ttu-id="c6ab3-194">Из hello **параметры** колонке управления задания резервного копирования, выбрав **мониторинг и отчеты > задания > задания резервного копирования** и выбрав **папки файлов** раскрывающемся hello меню.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-194">From hello **Settings** blade, you manage backup jobs by selecting **Monitoring and Reports > Jobs > Backup Jobs** and then selecting **File-Folders** from hello drop down menu.</span></span>
>
>

## <a name="monitor-backup-usage"></a><span data-ttu-id="c6ab3-195">Мониторинг использования архивации</span><span class="sxs-lookup"><span data-stu-id="c6ab3-195">Monitor Backup usage</span></span>
<span data-ttu-id="c6ab3-196">В hello разделе архивации панели мониторинга hello hello использования резервной копии отражает hello занятого хранилища в Azure.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-196">In hello Backup section of hello dashboard, hello Backup Usage tile shows hello storage consumed in Azure.</span></span> <span data-ttu-id="c6ab3-197">Здесь представлены сведения об использовании:</span><span class="sxs-lookup"><span data-stu-id="c6ab3-197">Storage usage is provided for:</span></span>

* <span data-ttu-id="c6ab3-198">Связанный с хранилищем hello использования облачного хранилища LRS</span><span class="sxs-lookup"><span data-stu-id="c6ab3-198">Cloud LRS storage usage associated with hello vault</span></span>
* <span data-ttu-id="c6ab3-199">Связанный с хранилищем hello использования облачного хранилища GRS</span><span class="sxs-lookup"><span data-stu-id="c6ab3-199">Cloud GRS storage usage associated with hello vault</span></span>

## <a name="manage-your-production-servers"></a><span data-ttu-id="c6ab3-200">Управление рабочими серверами</span><span class="sxs-lookup"><span data-stu-id="c6ab3-200">Manage your production servers</span></span>
<span data-ttu-id="c6ab3-201">toomanage производственных серверов, щелкните **параметры**.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-201">toomanage your production servers, click **Settings**.</span></span>

<span data-ttu-id="c6ab3-202">В области "Управление" последовательно выберите **Инфраструктура резервного копирования > Рабочие серверы**.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-202">Under Manage click **Backup infrastructure > Production Servers**.</span></span>

<span data-ttu-id="c6ab3-203">Hello производственных серверах колонке списка всех доступных производственных серверах.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-203">hello Production Servers blade lists of all your available production servers.</span></span> <span data-ttu-id="c6ab3-204">Щелкните на сервере в сведения о сервере hello список tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-204">Click on a server in hello list tooopen hello server details.</span></span>

![Защищенные элементы](./media/backup-azure-manage-windows-server/production-server-list.png)


## <a name="open-hello-azure-backup-agent"></a><span data-ttu-id="c6ab3-206">Откройте hello Azure Backup agent</span><span class="sxs-lookup"><span data-stu-id="c6ab3-206">Open hello Azure Backup agent</span></span>
<span data-ttu-id="c6ab3-207">Откройте hello **агента службы архивации Microsoft Azure** (можно найти путем поиска свой компьютер и *архивации Microsoft Azure*).</span><span class="sxs-lookup"><span data-stu-id="c6ab3-207">Open hello **Microsoft Azure Backup agent** (you find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![Планирование архивации Windows Server](./media/backup-azure-manage-windows-server/snap-in-search.png)

<span data-ttu-id="c6ab3-209">Из hello **действия** найти по адресу hello правой части консоли hello резервного копирования выполнить следующие задачи по управлению hello:</span><span class="sxs-lookup"><span data-stu-id="c6ab3-209">From hello **Actions** available at hello right of hello backup agent console you perform hello following management tasks:</span></span>

* <span data-ttu-id="c6ab3-210">Регистрация сервера</span><span class="sxs-lookup"><span data-stu-id="c6ab3-210">Register Server</span></span>
* <span data-ttu-id="c6ab3-211">Создание расписания архивации</span><span class="sxs-lookup"><span data-stu-id="c6ab3-211">Schedule Backup</span></span>
* <span data-ttu-id="c6ab3-212">Выполнить архивацию сейчас</span><span class="sxs-lookup"><span data-stu-id="c6ab3-212">Back Up now</span></span>
* <span data-ttu-id="c6ab3-213">Изменить свойства</span><span class="sxs-lookup"><span data-stu-id="c6ab3-213">Change Properties</span></span>

![Действия в консоли агента службы архивации Microsoft Azure](./media/backup-azure-manage-windows-server/console-actions.png)

> [!NOTE]
> <span data-ttu-id="c6ab3-215">слишком**восстановить данные**, в разделе [восстановить файлы tooa Windows server или клиентским компьютером Windows](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="c6ab3-215">too**Recover Data**, see [Restore files tooa Windows server or Windows client machine](backup-azure-restore-windows-server.md).</span></span>
>
>

## <a name="modify-hello-backup-schedule"></a><span data-ttu-id="c6ab3-216">Изменение расписания резервного копирования hello</span><span class="sxs-lookup"><span data-stu-id="c6ab3-216">Modify hello backup schedule</span></span>
1. <span data-ttu-id="c6ab3-217">В агенте службы архивации Microsoft Azure hello щелкните **планирования резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-217">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Планирование архивации Windows Server](./media/backup-azure-manage-windows-server/schedule-backup.png)
2. <span data-ttu-id="c6ab3-219">В hello **мастер планирования резервного копирования** оставить hello **toobackup элементы или время изменения производятся** флажок и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-219">In hello **Schedule Backup Wizard** leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![Планирование архивации Windows Server](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="c6ab3-221">Если вы tooadd или изменить элементы на hello **tooBackup выбрать элементы** откройте **добавить элементы**.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-221">If you want tooadd or change items, on hello **Select Items tooBackup** screen click **Add Items**.</span></span>

    <span data-ttu-id="c6ab3-222">Можно также задать **параметры исключения** на этой странице приветствия мастера.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-222">You can also set **Exclusion Settings** from this page in hello wizard.</span></span> <span data-ttu-id="c6ab3-223">Если требуется tooexclude файлы или типы файлов hello процедура добавления [параметры исключения](#manage-exclusion-settings).</span><span class="sxs-lookup"><span data-stu-id="c6ab3-223">If you want tooexclude files or file types read hello procedure for adding [exclusion settings](#manage-exclusion-settings).</span></span>
4. <span data-ttu-id="c6ab3-224">Выберите hello файлы и папки tooback вверх и щелкните **хорошо**.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-224">Select hello files and folders you want tooback up and click **Okay**.</span></span>

    ![Планирование архивации Windows Server](./media/backup-azure-manage-windows-server/add-items-modify.png)
5. <span data-ttu-id="c6ab3-226">Укажите hello **расписание резервного копирования** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-226">Specify hello **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="c6ab3-227">Вы можете запланировать ежедневное (не более трех раз в день) или еженедельное резервное копирование.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-227">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![Элементы для архивации Windows Server](./media/backup-azure-manage-windows-server/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > <span data-ttu-id="c6ab3-229">Задание расписания резервного копирования hello подробно рассматривается в этом [статьи](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="c6ab3-229">Specifying hello backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).</span></span>
   >

6. <span data-ttu-id="c6ab3-230">Выберите hello **политики хранения** hello резервной копии и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-230">Select hello **Retention Policy** for hello backup copy and click **Next**.</span></span>

    ![Элементы для архивации Windows Server](./media/backup-azure-manage-windows-server/select-retention-policy-modify.png)
7. <span data-ttu-id="c6ab3-232">На hello **Подтверждение** экрана Просмотр сведений об hello и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-232">On hello **Confirmation** screen review hello information and click **Finish**.</span></span>
8. <span data-ttu-id="c6ab3-233">После завершения работы приветствия мастера создания hello **расписание резервного копирования**, нажмите кнопку **закрыть**.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-233">Once hello wizard finishes creating hello **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="c6ab3-234">После изменения защиты, можно проверить, правильно инициируют резервных копий с переходом toohello **заданий** вкладку и подтверждения того, что изменения отражаются в hello задания резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-234">After modifying protection, you can confirm that backups are triggering correctly by going toohello **Jobs** tab and confirming that changes are reflected in hello backup jobs.</span></span>

## <a name="enable-network-throttling"></a><span data-ttu-id="c6ab3-235">Включение регулирования сети</span><span class="sxs-lookup"><span data-stu-id="c6ab3-235">Enable Network Throttling</span></span>

<span data-ttu-id="c6ab3-236">агент Azure Backup Hello предоставляет вкладку регулирование, позволяющий toocontrol использование пропускной способности сети при передаче данных.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-236">hello Azure Backup agent provides a Throttling tab which allows you toocontrol how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="c6ab3-237">Этот элемент управления может пригодиться, если вам требуется tooback копирование данных в рабочее время, но не требуется toointerfere hello процесс резервного копирования с другими Интернет-трафика.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-237">This control can be helpful if you need tooback up data during work hours but do not want hello backup process toointerfere with other internet traffic.</span></span> <span data-ttu-id="c6ab3-238">Регулирование данных передачи применяется tooback копирование и восстановление действий.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-238">Throttling of data transfer applies tooback up and restore activities.</span></span>  

<span data-ttu-id="c6ab3-239">Регулирование tooenable:</span><span class="sxs-lookup"><span data-stu-id="c6ab3-239">tooenable throttling:</span></span>

1. <span data-ttu-id="c6ab3-240">В hello **агента резервного копирования**, нажмите кнопку **изменить свойства**.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-240">In hello **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="c6ab3-241">На hello ** регулирования вкладки, выберите **включить регулирования для операций резервного копирования использование пропускной способности Интернета**.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-241">On hello **Throttling tab, select **Enable internet bandwidth usage throttling for backup operations**.</span></span>

    ![Регулирование сети](./media/backup-azure-manage-windows-server/throttling-dialog.png)

    <span data-ttu-id="c6ab3-243">После включения регулирования, укажите допустимый пропускной способности, для передачи во время резервного копирования данных hello **рабочие часы** и **нерабочие часы**.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-243">Once you have enabled throttling, specify hello allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="c6ab3-244">значения Hello пропускной способности начинаются с 512 килобайт в секунду (Кбит/с) и можно перейти вверх too1023 мегабайт в секунду (Мбит/с).</span><span class="sxs-lookup"><span data-stu-id="c6ab3-244">hello bandwidth values begin at 512 kilobytes per second (Kbps) and can go up too1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="c6ab3-245">Можно также назначить hello начала и окончания для **рабочие часы**, и какие дни недели hello считаются рабочих дней.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-245">You can also designate hello start and finish for **Work hours**, and which days of hello week are considered Work days.</span></span> <span data-ttu-id="c6ab3-246">время Hello за пределами указанных рабочих часов hello — считаются toobe нерабочего времени.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-246">hello time outside of hello designated Work hours is considered toobe non-work hours.</span></span>
3. <span data-ttu-id="c6ab3-247">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-247">Click **OK**.</span></span>

## <a name="manage-exclusion-settings"></a><span data-ttu-id="c6ab3-248">Управление параметрами исключений</span><span class="sxs-lookup"><span data-stu-id="c6ab3-248">Manage exclusion settings</span></span>
1. <span data-ttu-id="c6ab3-249">Откройте hello **агента службы архивации Microsoft Azure** (его можно найти путем поиска свой компьютер и *архивации Microsoft Azure*).</span><span class="sxs-lookup"><span data-stu-id="c6ab3-249">Open hello **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![Планирование архивации Windows Server](./media/backup-azure-manage-windows-server/snap-in-search.png)
2. <span data-ttu-id="c6ab3-251">В агенте службы архивации Microsoft Azure hello щелкните **планирования резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-251">In hello Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Планирование архивации Windows Server](./media/backup-azure-manage-windows-server/schedule-backup.png)
3. <span data-ttu-id="c6ab3-253">В мастер планирования резервного копирования hello оставьте hello **toobackup элементы или время изменения производятся** флажок и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-253">In hello Schedule Backup Wizard leave hello **Make changes toobackup items or times** option selected and click **Next**.</span></span>

    ![Планирование архивации Windows Server](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="c6ab3-255">Щелкните **Параметры исключений**.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-255">Click **Exclusions Settings**.</span></span>

    ![Планирование архивации Windows Server](./media/backup-azure-manage-windows-server/exclusion-settings.png)
5. <span data-ttu-id="c6ab3-257">Щелкните **Добавить исключение**.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-257">Click **Add Exclusion**.</span></span>

    ![Планирование архивации Windows Server](./media/backup-azure-manage-windows-server/add-exclusion.png)
6. <span data-ttu-id="c6ab3-259">Выберите расположение hello и затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-259">Select hello location and then, click **OK**.</span></span>

    ![Планирование архивации Windows Server](./media/backup-azure-manage-windows-server/exclusion-location.png)
7. <span data-ttu-id="c6ab3-261">Добавлять расширение файла hello в hello **тип файла** поля.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-261">Add hello file extension in hello **File Type** field.</span></span>

    ![Планирование архивации Windows Server](./media/backup-azure-manage-windows-server/exclude-file-type.png)

    <span data-ttu-id="c6ab3-263">Добавление расширения .mp3</span><span class="sxs-lookup"><span data-stu-id="c6ab3-263">Adding an .mp3 extension</span></span>

    ![Планирование архивации Windows Server](./media/backup-azure-manage-windows-server/exclude-mp3.png)

    <span data-ttu-id="c6ab3-265">tooadd другое расширение, нажмите кнопку **Добавление исключаемых** и введите другое расширение имени файла (Добавление расширения .jpeg).</span><span class="sxs-lookup"><span data-stu-id="c6ab3-265">tooadd another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![Планирование архивации Windows Server](./media/backup-azure-manage-windows-server/exclude-jpg.png)
8. <span data-ttu-id="c6ab3-267">После добавления всех расширений hello, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-267">When you've added all hello extensions, click **OK**.</span></span>
9. <span data-ttu-id="c6ab3-268">Продолжайте hello мастер планирования резервного копирования, нажав кнопку **Далее** до hello **страница подтверждения**, нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-268">Continue through hello Schedule Backup Wizard by clicking **Next** until hello **Confirmation page**, then click **Finish**.</span></span>

    ![Планирование архивации Windows Server](./media/backup-azure-manage-windows-server/finish-exclusions.png)

## <a name="frequently-asked-questions"></a><span data-ttu-id="c6ab3-270">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="c6ab3-270">Frequently asked questions</span></span>
<span data-ttu-id="c6ab3-271">**Q1. состояние задания резервного копирования Hello показано, как завершенное во hello агента резервного копирования Azure, почему не его получить будут немедленно отражаться в портал?**</span><span class="sxs-lookup"><span data-stu-id="c6ab3-271">**Q1. hello backup job status shows as completed in hello Azure backup agent, why doesn't it get reflected immediately in portal?**</span></span>

<span data-ttu-id="c6ab3-272">ОТВЕТ 1.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-272">A1.</span></span> <span data-ttu-id="c6ab3-273">Существует по максимальной задержки 15 минут между состояние задания резервного копирования hello отражается в hello агента резервного копирования Azure и hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-273">There is at maximum delay of 15 mins between hello backup job status reflected in hello Azure backup agent and hello Azure portal.</span></span>

<span data-ttu-id="c6ab3-274">**Q.2 при сбое задания резервного копирования, как долго требуется tooraise оповещение?**</span><span class="sxs-lookup"><span data-stu-id="c6ab3-274">**Q.2 When a backup job fails, how long does it take tooraise an alert?**</span></span>

<span data-ttu-id="c6ab3-275">A.2 предупреждение возникает в течение 20 минут hello Azure сбоя резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-275">A.2 An alert is raised within 20 mins of hello Azure backup failure.</span></span>

<span data-ttu-id="c6ab3-276">**ВОПРОС 3. В каком случае сообщение электронной почты не будет отправлено, если уведомления настроены?**</span><span class="sxs-lookup"><span data-stu-id="c6ab3-276">**Q3. Is there a case where an email won’t be sent if notifications are configured?**</span></span>

<span data-ttu-id="c6ab3-277">ОТВЕТ 3.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-277">A3.</span></span> <span data-ttu-id="c6ab3-278">Ниже приведены случаи hello при hello уведомления не будут отправляться в лишних оповещений hello tooreduce заказа.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-278">Below are hello cases when hello notification will not be sent in order tooreduce hello alert noise:</span></span>

* <span data-ttu-id="c6ab3-279">Если настраиваются уведомления каждый час, и возникает предупреждение и разрешить в течение часа hello</span><span class="sxs-lookup"><span data-stu-id="c6ab3-279">If notifications are configured hourly and an alert is raised and resolved within hello hour</span></span>
* <span data-ttu-id="c6ab3-280">Задание отменено.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-280">Job is canceled.</span></span>
* <span data-ttu-id="c6ab3-281">Второе задание резервного копирования не удалось выполнить, так как выполняется первое задание резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-281">Second backup job failed because original backup job is in progress.</span></span>

## <a name="troubleshooting-monitoring-issues"></a><span data-ttu-id="c6ab3-282">Устранение неполадок мониторинга</span><span class="sxs-lookup"><span data-stu-id="c6ab3-282">Troubleshooting Monitoring Issues</span></span>
<span data-ttu-id="c6ab3-283">**Проблема:** заданий или предупреждения от hello Azure Backup agent не отображаются на портале hello.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-283">**Issue:** Jobs and/or alerts from hello Azure Backup agent do not appear in hello portal.</span></span>

<span data-ttu-id="c6ab3-284">**Действия по устранению неполадок:** hello процесса ```OBRecoveryServicesManagementAgent```, отправляет hello предупреждение и задания toohello данных службы архивации Azure.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-284">**Troubleshooting steps:** hello process, ```OBRecoveryServicesManagementAgent```, sends hello job and alert data toohello Azure Backup service.</span></span> <span data-ttu-id="c6ab3-285">Иногда этот процесс может зависнуть или завершить работу.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-285">Occasionally this process can become stuck or shutdown.</span></span>

1. <span data-ttu-id="c6ab3-286">tooverify hello процесс не запущен, откройте **диспетчер задач** и проверьте наличие hello ```OBRecoveryServicesManagementAgent``` выполняется процесс.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-286">tooverify hello process is not running, open **Task Manager** and check if hello ```OBRecoveryServicesManagementAgent``` process is running.</span></span>
2. <span data-ttu-id="c6ab3-287">Предположим, что hello процесс не запущен, откройте **панели управления** и просмотрите список hello служб.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-287">Assuming that hello process is not running, open **Control Panel** and browse hello list of services.</span></span> <span data-ttu-id="c6ab3-288">Запустите или перезапустите **агент управления службами восстановления Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="c6ab3-288">Start or restart **Microsoft Azure Recovery Services Management Agent**.</span></span>

    <span data-ttu-id="c6ab3-289">Для получения дополнительных сведений перейдите hello журналов по адресу:</span><span class="sxs-lookup"><span data-stu-id="c6ab3-289">For further information, browse hello logs at:</span></span><br/><span data-ttu-id="c6ab3-290">
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` Например:</span><span class="sxs-lookup"><span data-stu-id="c6ab3-290">
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` For example:</span></span><br/>
   `C:\Program Files\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider0.errlog`

## <a name="next-steps"></a><span data-ttu-id="c6ab3-291">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c6ab3-291">Next steps</span></span>
* [<span data-ttu-id="c6ab3-292">Восстановление Windows Server или клиента Windows из Azure</span><span class="sxs-lookup"><span data-stu-id="c6ab3-292">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="c6ab3-293">toolearn Дополнительные сведения об архивации Azure в разделе [Обзор резервного копирования Azure](backup-introduction-to-azure-backup.md)</span><span class="sxs-lookup"><span data-stu-id="c6ab3-293">toolearn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="c6ab3-294">Посетите hello [форуме резервного копирования Azure](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="c6ab3-294">Visit hello [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>
