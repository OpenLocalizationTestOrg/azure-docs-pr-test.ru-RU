---
title: "Управление хранилищами и серверами служб восстановления Azure | Документация Майкрософт"
description: "Из этого руководства вы узнаете об управлении хранилищами и серверами служб восстановления Azure."
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
ms.openlocfilehash: 5922e308f5c205a07bd329c28322ae82cea0e1fa
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-and-manage-azure-recovery-services-vaults-and-servers-for-windows-machines"></a><span data-ttu-id="458e0-103">Мониторинг хранилищ и серверов служб восстановления Azure для компьютеров Windows и управление ими</span><span class="sxs-lookup"><span data-stu-id="458e0-103">Monitor and manage Azure recovery services vaults and servers for Windows machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="458e0-104">Диспетчер ресурсов</span><span class="sxs-lookup"><span data-stu-id="458e0-104">Resource Manager</span></span>](backup-azure-manage-windows-server.md)
> * [<span data-ttu-id="458e0-105">Классический</span><span class="sxs-lookup"><span data-stu-id="458e0-105">Classic</span></span>](backup-azure-manage-windows-server-classic.md)
>
>

<span data-ttu-id="458e0-106">В этой статье представлен обзор задач мониторинга архивации и управления ею, которые можно выполнять на портале Azure и с помощью агента службы архивации Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="458e0-106">In this article you'll find an overview of the backup monitor and management tasks available through the Azure portal and the Microsoft Azure Backup agent.</span></span> <span data-ttu-id="458e0-107">В этой статье предполагается, что у вас уже есть подписка Azure и вы создали по крайней мере одно хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="458e0-107">This article assumes you already have an Azure subscription and have created at least one Recovery Services vault.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]


## <a name="open-a-recovery-services-vault"></a><span data-ttu-id="458e0-108">Открытие хранилища служб восстановления</span><span class="sxs-lookup"><span data-stu-id="458e0-108">Open a Recovery Services vault</span></span>

<span data-ttu-id="458e0-109">Панель мониторинга хранилища служб восстановления содержит сведения о хранилище служб восстановления или его атрибуты.</span><span class="sxs-lookup"><span data-stu-id="458e0-109">The Recovery Services vault dashboard shows you the details or attributes of a Recovery Services vault.</span></span>

1. <span data-ttu-id="458e0-110">Войдите на [портал Azure](https://portal.azure.com/) , используя свою подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="458e0-110">Sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="458e0-111">В главном меню выберите **Больше служб**.</span><span class="sxs-lookup"><span data-stu-id="458e0-111">On the Hub menu, click **More Services**.</span></span>

    ![Открытие списка хранилищ служб восстановления — шаг 1](./media/backup-azure-manage-windows-server/open-rs-vault-list.png) <br/>

3. <span data-ttu-id="458e0-113">Вам нужно открыть хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="458e0-113">You want to open a Recovery Services vault.</span></span> <span data-ttu-id="458e0-114">В диалоговом окне начните вводить **Recovery Services**.</span><span class="sxs-lookup"><span data-stu-id="458e0-114">In the dialog box, start typing **Recovery Services**.</span></span> <span data-ttu-id="458e0-115">Как только вы начнете вводить, список отфильтруется соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="458e0-115">As you begin typing, the list will filter based on your input.</span></span> <span data-ttu-id="458e0-116">Щелкните **Recovery Services vaults** (Хранилища служб восстановления), чтобы отобразить список хранилищ служб восстановления в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="458e0-116">Click **Recovery Services vaults** to display the list of Recovery Services vaults in your subscription.</span></span>

    ![Создание хранилища служб восстановления — шаг 1](./media/backup-azure-manage-windows-server/browse-to-rs-vaults-2.png) <br/>

    <span data-ttu-id="458e0-118">Отобразится список хранилищ служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="458e0-118">The list of Recovery Services vaults opens.</span></span>

    ![Создание хранилища служб восстановления — шаг 1](./media/backup-azure-manage-windows-server/list-of-rs-vaults.png) <br/>

4. <span data-ttu-id="458e0-120">Из списка хранилищ выберите имя хранилища служб восстановления, которое нужно открыть.</span><span class="sxs-lookup"><span data-stu-id="458e0-120">From the list of vaults, select the name of the Recovery Services vault you want to open.</span></span> <span data-ttu-id="458e0-121">Откроется колонка панели мониторинга хранилища служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="458e0-121">The Recovery Services vault dashboard blade opens.</span></span>

    ![Панель мониторинга хранилища служб восстановления](./media/backup-azure-manage-windows-server/rs-vault-blade.png) <br/>

    <span data-ttu-id="458e0-123">Теперь, когда вы открыли хранилище служб восстановления, попробуйте выполнить какую-либо из задач мониторинга или управления.</span><span class="sxs-lookup"><span data-stu-id="458e0-123">Now that you have opened the Recovery Services vault, try any of the monitoring or management tasks.</span></span>

## <a name="monitor-backup-jobs-and-alerts"></a><span data-ttu-id="458e0-124">Мониторинг заданий и оповещений службы архивации</span><span class="sxs-lookup"><span data-stu-id="458e0-124">Monitor backup jobs and alerts</span></span>

<span data-ttu-id="458e0-125">Мониторинг заданий и предупреждений можно выполнять на панели мониторинга хранилища служб восстановления. На этой панели содержится следующее:</span><span class="sxs-lookup"><span data-stu-id="458e0-125">You monitor jobs and alerts from the Recovery Services vault dashboard, where you see:</span></span>

* <span data-ttu-id="458e0-126">сведения об оповещениях, связанных с архивацией;</span><span class="sxs-lookup"><span data-stu-id="458e0-126">Backup alerts details</span></span>
* <span data-ttu-id="458e0-127">файлы и папки, а также виртуальные машины Azure, защищенные в облаке;</span><span class="sxs-lookup"><span data-stu-id="458e0-127">Files and folders, as well as Azure virtual machines protected in the cloud</span></span>
* <span data-ttu-id="458e0-128">сведения об общем объеме занятого хранилища в Azure;</span><span class="sxs-lookup"><span data-stu-id="458e0-128">Total storage consumed in Azure</span></span>
* <span data-ttu-id="458e0-129">состояние задания архивации.</span><span class="sxs-lookup"><span data-stu-id="458e0-129">Backup job status</span></span>

![Задачи панели мониторинга архивации](./media/backup-azure-manage-windows-server/dashboard-tiles.png)

<span data-ttu-id="458e0-131">Если выбрать сведения на каждой из этих плиток, откроется соответствующая колонка, в которой можно управлять связанными задачами.</span><span class="sxs-lookup"><span data-stu-id="458e0-131">Clicking the information in each of these tiles will open the associated blade where you manage related tasks.</span></span>

<span data-ttu-id="458e0-132">В верхней части панели мониторинга находятся следующие элементы интерфейса:</span><span class="sxs-lookup"><span data-stu-id="458e0-132">From the top of the Dashboard:</span></span>

* <span data-ttu-id="458e0-133">"Параметры". Здесь содержатся доступные задачи архивации.</span><span class="sxs-lookup"><span data-stu-id="458e0-133">Settings provides access available backup tasks.</span></span>
* <span data-ttu-id="458e0-134">"Архивация". Здесь можно создать резервные копии новых файлов и папок (или виртуальных машин Azure) в хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="458e0-134">Backup - helps you back up new files and folders (or Azure VMs) to the Recovery Services vault.</span></span>
* <span data-ttu-id="458e0-135">"Удалить". Если хранилище служб восстановления больше не используется, его можно удалить для освобождения места.</span><span class="sxs-lookup"><span data-stu-id="458e0-135">Delete - If a recovery services vault is no longer being used, you can delete it to free up storage space.</span></span> <span data-ttu-id="458e0-136">Элемент "Удалить" становится доступен только после удаления из хранилища всех защищенных серверов.</span><span class="sxs-lookup"><span data-stu-id="458e0-136">Delete is only enabled after all protected servers have been deleted from the vault.</span></span>

![Задачи панели мониторинга архивации](./media/backup-azure-manage-windows-server/dashboard-tasks.png)

## <a name="alerts-for-backups-using-azure-backup-agent"></a><span data-ttu-id="458e0-138">Оповещения о резервном копировании с помощью агента службы архивации Azure</span><span class="sxs-lookup"><span data-stu-id="458e0-138">Alerts for backups using Azure backup agent:</span></span>
| <span data-ttu-id="458e0-139">Уровень оповещения</span><span class="sxs-lookup"><span data-stu-id="458e0-139">Alert Level</span></span> | <span data-ttu-id="458e0-140">Отправляемые оповещения</span><span class="sxs-lookup"><span data-stu-id="458e0-140">Alerts sent</span></span> |
| --- | --- |
| <span data-ttu-id="458e0-141">критические ошибки.</span><span class="sxs-lookup"><span data-stu-id="458e0-141">Critical</span></span> |<span data-ttu-id="458e0-142">Сбой резервного копирования, сбой восстановления</span><span class="sxs-lookup"><span data-stu-id="458e0-142">Backup failure, recovery failure</span></span> |
| <span data-ttu-id="458e0-143">Предупреждение</span><span class="sxs-lookup"><span data-stu-id="458e0-143">Warning</span></span> |<span data-ttu-id="458e0-144">Резервное копирование завершено с предупреждениями (когда меньше ста файлов не скопировано из-за повреждений и более миллиона файлов скопировано успешно).</span><span class="sxs-lookup"><span data-stu-id="458e0-144">Backup completed with warnings (when fewer than one hundred files are not backed up due to corruption issues, and more than one million files are successfully backed up)</span></span> |
| <span data-ttu-id="458e0-145">Информация</span><span class="sxs-lookup"><span data-stu-id="458e0-145">Informational</span></span> |<span data-ttu-id="458e0-146">None</span><span class="sxs-lookup"><span data-stu-id="458e0-146">None</span></span> |

## <a name="manage-backup-alerts"></a><span data-ttu-id="458e0-147">Управление оповещениями, связанными с архивацией</span><span class="sxs-lookup"><span data-stu-id="458e0-147">Manage Backup alerts</span></span>
<span data-ttu-id="458e0-148">Щелкните элемент **Оповещения, связанные с архивацией**, чтобы открыть колонку **Оповещения, связанные с архивацией** и управлять оповещениями.</span><span class="sxs-lookup"><span data-stu-id="458e0-148">Click the **Backup Alerts** tile to open the **Backup Alerts** blade and manage alerts.</span></span>

![Оповещения, связанные с архивацией](./media/backup-azure-manage-windows-server/manage-backup-alerts.png)

<span data-ttu-id="458e0-150">На этой плитке отображаются сведения о количестве:</span><span class="sxs-lookup"><span data-stu-id="458e0-150">The Backup Alerts tile shows you the number of:</span></span>

* <span data-ttu-id="458e0-151">критических оповещений, неразрешенных в течение последних 24 часов;</span><span class="sxs-lookup"><span data-stu-id="458e0-151">critical alerts unresolved in last 24 hours</span></span>
* <span data-ttu-id="458e0-152">оповещений с предупреждениями, неразрешенных в течение последних 24 часов.</span><span class="sxs-lookup"><span data-stu-id="458e0-152">warning alerts unresolved in last 24 hours</span></span>

<span data-ttu-id="458e0-153">Если выбрать любую из этих ссылок, откроется колонка **Оповещения, связанные с архивацией** с отфильтрованным представлением, содержащим эти оповещения (критические или уровня предупреждения).</span><span class="sxs-lookup"><span data-stu-id="458e0-153">Clicking on each of these links takes you to the **Backup Alerts** blade with a filtered view of these alerts (critical or warning).</span></span>

<span data-ttu-id="458e0-154">В колонке "Оповещения, связанные с архивацией" можно выполнить следующее:</span><span class="sxs-lookup"><span data-stu-id="458e0-154">From the Backup Alerts blade, you:</span></span>

* <span data-ttu-id="458e0-155">Выбрать сведения, которые нужно добавлять в оповещения.</span><span class="sxs-lookup"><span data-stu-id="458e0-155">Choose the appropriate information to include with your alerts.</span></span>

    ![Выбор столбцов](./media/backup-azure-manage-windows-server/choose-alerts-colunms.png)
* <span data-ttu-id="458e0-157">Отфильтровать оповещения по уровню серьезности, состоянию и времени начала и окончания.</span><span class="sxs-lookup"><span data-stu-id="458e0-157">Filter alerts for severity, status and start/end times.</span></span>

    ![Фильтрация оповещений](./media/backup-azure-manage-windows-server/filter-alerts.png)
* <span data-ttu-id="458e0-159">Настроить уровень серьезности, частоту и получателей оповещений, а также выключить или включить их.</span><span class="sxs-lookup"><span data-stu-id="458e0-159">Configure notifications for severity, frequency and recipients, as well as turn alerts on or off.</span></span>

    ![Фильтрация оповещений](./media/backup-azure-manage-windows-server/configure-notifications.png)

<span data-ttu-id="458e0-161">Если в качестве частоты в области **Уведомлять** выбрано значение **Каждое оповещение**, то сведения не группируются и представляются полностью в сообщениях электронной почты.</span><span class="sxs-lookup"><span data-stu-id="458e0-161">If **Per Alert** is selected as the **Notify** frequency no grouping or reduction in emails occurs.</span></span> <span data-ttu-id="458e0-162">Для каждого оповещения создается 1 уведомление.</span><span class="sxs-lookup"><span data-stu-id="458e0-162">Every alert results in 1 notification.</span></span> <span data-ttu-id="458e0-163">Это параметр по умолчанию. Кроме того, сразу же отправляется электронное письмо со сведениями о разрешении.</span><span class="sxs-lookup"><span data-stu-id="458e0-163">This is the default setting and the resolution email is also sent out immediately.</span></span>

<span data-ttu-id="458e0-164">Если в качестве частоты в области **Уведомлять** выбрано значение **Почасовой дайджест**, то пользователю отправляется одно сообщение по электронной почте, уведомляющее о том, что за последний час получены новые неразрешенные оповещения.</span><span class="sxs-lookup"><span data-stu-id="458e0-164">If **Hourly Digest** is selected as the **Notify** frequency one email is sent to the user telling them that there are unresolved new alerts generated in the last hour.</span></span> <span data-ttu-id="458e0-165">Электронные сообщения со сведениями о разрешении отправляются в конце часа.</span><span class="sxs-lookup"><span data-stu-id="458e0-165">A resolution email is sent out at the end of the hour.</span></span>

<span data-ttu-id="458e0-166">Оповещения могут отправляться для следующих уровней серьезности:</span><span class="sxs-lookup"><span data-stu-id="458e0-166">Alerts can be sent for the following severity levels:</span></span>

* <span data-ttu-id="458e0-167">критические ошибки.</span><span class="sxs-lookup"><span data-stu-id="458e0-167">critical</span></span>
* <span data-ttu-id="458e0-168">Предупреждение</span><span class="sxs-lookup"><span data-stu-id="458e0-168">warning</span></span>
* <span data-ttu-id="458e0-169">информационный.</span><span class="sxs-lookup"><span data-stu-id="458e0-169">information</span></span>

<span data-ttu-id="458e0-170">Отключить оповещение можно с помощью кнопки **Отключить** в колонке сведений задания.</span><span class="sxs-lookup"><span data-stu-id="458e0-170">You inactivate the alert with the **inactivate** button in the job details blade.</span></span> <span data-ttu-id="458e0-171">При нажатии этой кнопки можно создать заметки о разрешении.</span><span class="sxs-lookup"><span data-stu-id="458e0-171">When you click inactivate, you can provide resolution notes.</span></span>

<span data-ttu-id="458e0-172">Чтобы выбрать столбцы, которые должны отображаться в оповещении, нажмите кнопку **Выбрать столбцы** .</span><span class="sxs-lookup"><span data-stu-id="458e0-172">You choose the columns you want to appear as part of the alert with the **Choose columns** button.</span></span>

> [!NOTE]
> <span data-ttu-id="458e0-173">В колонке **Параметры** осуществляется управление оповещениями, связанными с архивацией. Для этого нужно последовательно выбрать **Мониторинг и отчеты > Предупреждения и события > Оповещения, связанные с архивацией**, а затем щелкнуть **Фильтр** или **Настройка уведомлений**.</span><span class="sxs-lookup"><span data-stu-id="458e0-173">From the **Settings** blade, you manage backup alerts by selecting **Monitoring and Reports > Alerts and Events > Backup Alerts** and then clicking **Filter** or **Configure Notifications**.</span></span>
>
>

## <a name="manage-backup-items"></a><span data-ttu-id="458e0-174">Управление архивируемыми элементами</span><span class="sxs-lookup"><span data-stu-id="458e0-174">Manage Backup items</span></span>
<span data-ttu-id="458e0-175">Теперь на портале управления стало доступно управление локальными резервными копиями.</span><span class="sxs-lookup"><span data-stu-id="458e0-175">Managing on-premises backups is now available in the management portal.</span></span> <span data-ttu-id="458e0-176">На панели мониторинга в разделе "Архивация" на плитке **Архивные элементы** содержатся сведения о количестве архивных элементов, защищенных в хранилище.</span><span class="sxs-lookup"><span data-stu-id="458e0-176">In the Backup section of the dashboard, the **Backup Items** tile shows the number of backup items protected to the vault.</span></span>

<span data-ttu-id="458e0-177">Щелкните **Файлы и папки** на плитке "Архивные элементы".</span><span class="sxs-lookup"><span data-stu-id="458e0-177">Click **File-Folders** in the Backup Items tile.</span></span>

![Элемент "Архивируемые элементы"](./media/backup-azure-manage-windows-server/backup-items-tile.png)

<span data-ttu-id="458e0-179">Откроется колонка "Архивные элементы", содержащая архивные элементы, отфильтрованные по файлам и папкам.</span><span class="sxs-lookup"><span data-stu-id="458e0-179">The Backup Items blade opens with the filter set to File-Folder where you see each specific backup item listed.</span></span>

![Архивные элементы](./media/backup-azure-manage-windows-server/backup-item-list.png)

<span data-ttu-id="458e0-181">Если выбрать конкретный архивный элемент в списке, отобразятся важные сведения для этого элемента.</span><span class="sxs-lookup"><span data-stu-id="458e0-181">If you select a specific backup item from the list, you see the essential details for that item.</span></span>

> [!NOTE]
> <span data-ttu-id="458e0-182">В колонке **Параметры** можно управлять файлами и папками. Для этого нужно выбрать **Защищенные элементы > Архивные элементы**, а затем — пункт **Папки и файлы** в раскрывающемся меню.</span><span class="sxs-lookup"><span data-stu-id="458e0-182">From the **Settings** blade, you manage files and folders by selecting **Protected Items > Backup Items** and then selecting **File-Folders** from the drop down menu.</span></span>
>
>

![Архивируемые элементы из параметров](./media/backup-azure-manage-windows-server/backup-files-and-folders.png)

## <a name="manage-backup-jobs"></a><span data-ttu-id="458e0-184">Управление заданиями архивации</span><span class="sxs-lookup"><span data-stu-id="458e0-184">Manage Backup jobs</span></span>
<span data-ttu-id="458e0-185">На панели мониторинга отображаются задания для локальной архивации (при архивации локального сервера в среду Azure) и архивации в Azure.</span><span class="sxs-lookup"><span data-stu-id="458e0-185">Backup jobs for both on-premises (when the on-premises server is backing up to Azure) and Azure backups are visible in the dashboard.</span></span>

<span data-ttu-id="458e0-186">На панели мониторинга в разделе "Архивация" на плитке "Задания архивации" показано количество заданий:</span><span class="sxs-lookup"><span data-stu-id="458e0-186">In the Backup section of the dashboard, the Backup job tile shows the number of jobs:</span></span>

* <span data-ttu-id="458e0-187">выполняется</span><span class="sxs-lookup"><span data-stu-id="458e0-187">in progress</span></span>
* <span data-ttu-id="458e0-188">завершившихся сбоем за последние 24 часа.</span><span class="sxs-lookup"><span data-stu-id="458e0-188">failed in the last 24 hours.</span></span>

<span data-ttu-id="458e0-189">Для управления заданиями архивации щелкните элемент **Задания архивации**. После этого откроется колонка "Задания архивации".</span><span class="sxs-lookup"><span data-stu-id="458e0-189">To manage your backup jobs, click the **Backup Jobs** tile, which opens the Backup Jobs blade.</span></span>

![Архивируемые элементы из параметров](./media/backup-azure-manage-windows-server/backup-jobs.png)

<span data-ttu-id="458e0-191">Сведения, доступные в этой колонке, можно изменять с помощью кнопки **Выбрать столбцы** в верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="458e0-191">You modify the information available in the Backup Jobs blade with the **Choose columns** button at the top of the page.</span></span>

<span data-ttu-id="458e0-192">С помощью кнопки **Фильтр** можно выбрать резервные копии файлов и папок, а также резервные копии виртуальных машин Azure.</span><span class="sxs-lookup"><span data-stu-id="458e0-192">Use the **Filter** button to select between Files and folders and Azure virtual machine backup.</span></span>

<span data-ttu-id="458e0-193">Если резервные копии файлов и папок не отображаются, нажмите кнопку **Фильтр** в верхней части страницы и в меню "Тип элемента" выберите пункт **Файлы и папки**.</span><span class="sxs-lookup"><span data-stu-id="458e0-193">If you don't see your backed up files and folders, click **Filter** button at the top of the page and select **Files and folders** from the Item Type menu.</span></span>

> [!NOTE]
> <span data-ttu-id="458e0-194">В колонке **Параметры** можно управлять заданиями архивации. Для этого нужно выбрать **Мониторинг и отчеты > Задания > Задания архивации**, а затем — пункт **Папки и файлы** в раскрывающемся меню.</span><span class="sxs-lookup"><span data-stu-id="458e0-194">From the **Settings** blade, you manage backup jobs by selecting **Monitoring and Reports > Jobs > Backup Jobs** and then selecting **File-Folders** from the drop down menu.</span></span>
>
>

## <a name="monitor-backup-usage"></a><span data-ttu-id="458e0-195">Мониторинг использования архивации</span><span class="sxs-lookup"><span data-stu-id="458e0-195">Monitor Backup usage</span></span>
<span data-ttu-id="458e0-196">На панели мониторинга в разделе "Архивация" в элементе "Использование архивации" содержатся сведения об объеме хранилища, используемом в Azure.</span><span class="sxs-lookup"><span data-stu-id="458e0-196">In the Backup section of the dashboard, the Backup Usage tile shows the storage consumed in Azure.</span></span> <span data-ttu-id="458e0-197">Здесь представлены сведения об использовании:</span><span class="sxs-lookup"><span data-stu-id="458e0-197">Storage usage is provided for:</span></span>

* <span data-ttu-id="458e0-198">облачного хранилища LRS, связанного с хранилищем;</span><span class="sxs-lookup"><span data-stu-id="458e0-198">Cloud LRS storage usage associated with the vault</span></span>
* <span data-ttu-id="458e0-199">облачного хранилища GRS, связанного с хранилищем.</span><span class="sxs-lookup"><span data-stu-id="458e0-199">Cloud GRS storage usage associated with the vault</span></span>

## <a name="manage-your-production-servers"></a><span data-ttu-id="458e0-200">Управление рабочими серверами</span><span class="sxs-lookup"><span data-stu-id="458e0-200">Manage your production servers</span></span>
<span data-ttu-id="458e0-201">Для управления рабочими серверами щелкните **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="458e0-201">To manage your production servers, click **Settings**.</span></span>

<span data-ttu-id="458e0-202">В области "Управление" последовательно выберите **Инфраструктура резервного копирования > Рабочие серверы**.</span><span class="sxs-lookup"><span data-stu-id="458e0-202">Under Manage click **Backup infrastructure > Production Servers**.</span></span>

<span data-ttu-id="458e0-203">В колонке "Рабочие серверы" перечислены все доступные рабочие серверы.</span><span class="sxs-lookup"><span data-stu-id="458e0-203">The Production Servers blade lists of all your available production servers.</span></span> <span data-ttu-id="458e0-204">Щелкните сервер в списке, чтобы открыть сведения о нем.</span><span class="sxs-lookup"><span data-stu-id="458e0-204">Click on a server in the list to open the server details.</span></span>

![Защищенные элементы](./media/backup-azure-manage-windows-server/production-server-list.png)


## <a name="open-the-azure-backup-agent"></a><span data-ttu-id="458e0-206">Запуск агента службы архивации Azure</span><span class="sxs-lookup"><span data-stu-id="458e0-206">Open the Azure Backup agent</span></span>
<span data-ttu-id="458e0-207">Откройте **агент службы архивации Microsoft Azure** (чтобы найти его, введите *Служба архивации Microsoft Azure*в строке поиска на своем компьютере).</span><span class="sxs-lookup"><span data-stu-id="458e0-207">Open the **Microsoft Azure Backup agent** (you find it by searching your machine for *Microsoft Azure Backup*).</span></span>

![Планирование архивации Windows Server](./media/backup-azure-manage-windows-server/snap-in-search.png)

<span data-ttu-id="458e0-209">В разделе **Действия** в правой части консоли агента службы архивации можно выполнять следующие задачи управления:</span><span class="sxs-lookup"><span data-stu-id="458e0-209">From the **Actions** available at the right of the backup agent console you perform the following management tasks:</span></span>

* <span data-ttu-id="458e0-210">Регистрация сервера</span><span class="sxs-lookup"><span data-stu-id="458e0-210">Register Server</span></span>
* <span data-ttu-id="458e0-211">Создание расписания архивации</span><span class="sxs-lookup"><span data-stu-id="458e0-211">Schedule Backup</span></span>
* <span data-ttu-id="458e0-212">Выполнить архивацию сейчас</span><span class="sxs-lookup"><span data-stu-id="458e0-212">Back Up now</span></span>
* <span data-ttu-id="458e0-213">Изменить свойства</span><span class="sxs-lookup"><span data-stu-id="458e0-213">Change Properties</span></span>

![Действия в консоли агента службы архивации Microsoft Azure](./media/backup-azure-manage-windows-server/console-actions.png)

> [!NOTE]
> <span data-ttu-id="458e0-215">Чтобы **восстановить данные**, ознакомьтесь со статьей [Восстановление файлов на сервере Windows Server или клиентском компьютере Windows с помощью модели развертывания Resource Manager](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="458e0-215">To **Recover Data**, see [Restore files to a Windows server or Windows client machine](backup-azure-restore-windows-server.md).</span></span>
>
>

## <a name="modify-the-backup-schedule"></a><span data-ttu-id="458e0-216">Изменение расписания архивации</span><span class="sxs-lookup"><span data-stu-id="458e0-216">Modify the backup schedule</span></span>
1. <span data-ttu-id="458e0-217">В агенте службы архивации Microsoft Azure щелкните **Создать расписание архивации**.</span><span class="sxs-lookup"><span data-stu-id="458e0-217">In the Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Планирование архивации Windows Server](./media/backup-azure-manage-windows-server/schedule-backup.png)
2. <span data-ttu-id="458e0-219">В **мастере архивации по расписанию** оставьте флажок **Изменить архивные элементы или время архивации** установленным и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="458e0-219">In the **Schedule Backup Wizard** leave the **Make changes to backup items or times** option selected and click **Next**.</span></span>

    ![Планирование архивации Windows Server](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
3. <span data-ttu-id="458e0-221">Если нужно добавить или изменить элементы, в окне **Выбор элементов для архивации** щелкните **Добавить элементы**.</span><span class="sxs-lookup"><span data-stu-id="458e0-221">If you want to add or change items, on the **Select Items to Backup** screen click **Add Items**.</span></span>

    <span data-ttu-id="458e0-222">На этой странице мастера также можно задать **параметры исключений** .</span><span class="sxs-lookup"><span data-stu-id="458e0-222">You can also set **Exclusion Settings** from this page in the wizard.</span></span> <span data-ttu-id="458e0-223">Если нужно исключить файлы или типы файлов, ознакомьтесь с процедурой добавления [параметров исключений](#manage-exclusion-settings).</span><span class="sxs-lookup"><span data-stu-id="458e0-223">If you want to exclude files or file types read the procedure for adding [exclusion settings](#manage-exclusion-settings).</span></span>
4. <span data-ttu-id="458e0-224">Выберите файлы и папки, для которых нужно создать резервные копии, и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="458e0-224">Select the files and folders you want to back up and click **Okay**.</span></span>

    ![Планирование архивации Windows Server](./media/backup-azure-manage-windows-server/add-items-modify.png)
5. <span data-ttu-id="458e0-226">Настройте **расписание архивации** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="458e0-226">Specify the **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="458e0-227">Вы можете запланировать ежедневное (не более трех раз в день) или еженедельное резервное копирование.</span><span class="sxs-lookup"><span data-stu-id="458e0-227">You can schedule daily (at a maximum of 3 times per day) or weekly backups.</span></span>

    ![Элементы для архивации Windows Server](./media/backup-azure-manage-windows-server/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > <span data-ttu-id="458e0-229">Дополнительные сведения о настройке расписания архивации см. в [этой статье](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="458e0-229">Specifying the backup schedule is explained in detail in this [article](backup-azure-backup-cloud-as-tape.md).</span></span>
   >

6. <span data-ttu-id="458e0-230">Выберите **политику хранения** для резервных копий и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="458e0-230">Select the **Retention Policy** for the backup copy and click **Next**.</span></span>

    ![Элементы для архивации Windows Server](./media/backup-azure-manage-windows-server/select-retention-policy-modify.png)
7. <span data-ttu-id="458e0-232">Проверьте сведения в окне **Подтверждение** и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="458e0-232">On the **Confirmation** screen review the information and click **Finish**.</span></span>
8. <span data-ttu-id="458e0-233">Когда мастер завершит создание **расписания архивации**, нажмите кнопку **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="458e0-233">Once the wizard finishes creating the **backup schedule**, click **Close**.</span></span>

    <span data-ttu-id="458e0-234">После изменения защиты можно проверить, своевременно ли запускается архивация. Для этого перейдите на вкладку **Задания** и убедитесь, что изменения отражаются в заданиях архивации.</span><span class="sxs-lookup"><span data-stu-id="458e0-234">After modifying protection, you can confirm that backups are triggering correctly by going to the **Jobs** tab and confirming that changes are reflected in the backup jobs.</span></span>

## <a name="enable-network-throttling"></a><span data-ttu-id="458e0-235">Включение регулирования сети</span><span class="sxs-lookup"><span data-stu-id="458e0-235">Enable Network Throttling</span></span>

<span data-ttu-id="458e0-236">В агенте службы архивации Azure есть вкладка "Регулирование", которая позволяет управлять использованием пропускной способности сети при передаче данных.</span><span class="sxs-lookup"><span data-stu-id="458e0-236">The Azure Backup agent provides a Throttling tab which allows you to control how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="458e0-237">Это полезно, если вам нужно выполнить архивацию в рабочее время так, чтобы операция копирования не мешала другим процессам, связанным с обработкой интернет-трафика.</span><span class="sxs-lookup"><span data-stu-id="458e0-237">This control can be helpful if you need to back up data during work hours but do not want the backup process to interfere with other internet traffic.</span></span> <span data-ttu-id="458e0-238">Регулирование передачи данных применяется при резервном копировании и восстановлении.</span><span class="sxs-lookup"><span data-stu-id="458e0-238">Throttling of data transfer applies to back up and restore activities.</span></span>  

<span data-ttu-id="458e0-239">Чтобы включить регулирование:</span><span class="sxs-lookup"><span data-stu-id="458e0-239">To enable throttling:</span></span>

1. <span data-ttu-id="458e0-240">В **агенте архивации** щелкните **Изменить свойства**.</span><span class="sxs-lookup"><span data-stu-id="458e0-240">In the **Backup agent**, click **Change Properties**.</span></span>
2. <span data-ttu-id="458e0-241">На вкладке "Регулирование" установите флажок **Разрешить регулирование уровня использования пропускной способности канала для операций резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="458e0-241">On the **Throttling tab, select **Enable internet bandwidth usage throttling for backup operations**.</span></span>

    ![Регулирование сети](./media/backup-azure-manage-windows-server/throttling-dialog.png)

    <span data-ttu-id="458e0-243">После включения регулирования укажите допустимую пропускную способность для передачи данных во время архивации в **рабочее** и **нерабочее** время.</span><span class="sxs-lookup"><span data-stu-id="458e0-243">Once you have enabled throttling, specify the allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="458e0-244">Значения пропускной способности начинаются с 512 килобит в секунду (Кбит/с) и могут перейти до 1023 мегабит в секунду (Мбит/с).</span><span class="sxs-lookup"><span data-stu-id="458e0-244">The bandwidth values begin at 512 kilobytes per second (Kbps) and can go up to 1023 megabytes per second (Mbps).</span></span> <span data-ttu-id="458e0-245">Можно также назначить время начала и окончания для **рабочих часов**и выбрать, какие дни недели считаются рабочими.</span><span class="sxs-lookup"><span data-stu-id="458e0-245">You can also designate the start and finish for **Work hours**, and which days of the week are considered Work days.</span></span> <span data-ttu-id="458e0-246">Время вне назначенных рабочих часов считается нерабочим.</span><span class="sxs-lookup"><span data-stu-id="458e0-246">The time outside of the designated Work hours is considered to be non-work hours.</span></span>
3. <span data-ttu-id="458e0-247">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="458e0-247">Click **OK**.</span></span>

## <a name="manage-exclusion-settings"></a><span data-ttu-id="458e0-248">Управление параметрами исключений</span><span class="sxs-lookup"><span data-stu-id="458e0-248">Manage exclusion settings</span></span>
1. <span data-ttu-id="458e0-249">Откройте **агент службы архивации Microsoft Azure** (чтобы найти его, введите *Служба архивации Microsoft Azure*в строке поиска на своем компьютере).</span><span class="sxs-lookup"><span data-stu-id="458e0-249">Open the **Microsoft Azure Backup agent** (you can find it by searching your machine for *Microsoft Azure Backup*).</span></span>

    ![Планирование архивации Windows Server](./media/backup-azure-manage-windows-server/snap-in-search.png)
2. <span data-ttu-id="458e0-251">В агенте службы архивации Microsoft Azure щелкните **Создать расписание архивации**.</span><span class="sxs-lookup"><span data-stu-id="458e0-251">In the Microsoft Azure Backup agent click **Schedule Backup**.</span></span>

    ![Планирование архивации Windows Server](./media/backup-azure-manage-windows-server/schedule-backup.png)
3. <span data-ttu-id="458e0-253">В мастере архивации по расписанию оставьте флажок **Изменить архивные элементы или время архивации** установленным и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="458e0-253">In the Schedule Backup Wizard leave the **Make changes to backup items or times** option selected and click **Next**.</span></span>

    ![Планирование архивации Windows Server](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
4. <span data-ttu-id="458e0-255">Щелкните **Параметры исключений**.</span><span class="sxs-lookup"><span data-stu-id="458e0-255">Click **Exclusions Settings**.</span></span>

    ![Планирование архивации Windows Server](./media/backup-azure-manage-windows-server/exclusion-settings.png)
5. <span data-ttu-id="458e0-257">Щелкните **Добавить исключение**.</span><span class="sxs-lookup"><span data-stu-id="458e0-257">Click **Add Exclusion**.</span></span>

    ![Планирование архивации Windows Server](./media/backup-azure-manage-windows-server/add-exclusion.png)
6. <span data-ttu-id="458e0-259">Выберите расположение и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="458e0-259">Select the location and then, click **OK**.</span></span>

    ![Планирование архивации Windows Server](./media/backup-azure-manage-windows-server/exclusion-location.png)
7. <span data-ttu-id="458e0-261">Добавьте расширение файла в поле **Тип файла** .</span><span class="sxs-lookup"><span data-stu-id="458e0-261">Add the file extension in the **File Type** field.</span></span>

    ![Планирование архивации Windows Server](./media/backup-azure-manage-windows-server/exclude-file-type.png)

    <span data-ttu-id="458e0-263">Добавление расширения .mp3</span><span class="sxs-lookup"><span data-stu-id="458e0-263">Adding an .mp3 extension</span></span>

    ![Планирование архивации Windows Server](./media/backup-azure-manage-windows-server/exclude-mp3.png)

    <span data-ttu-id="458e0-265">Чтобы добавить другое расширение, нажмите кнопку **Добавить исключение** и введите другое расширение имени файла (ниже показано добавление расширения JPEG).</span><span class="sxs-lookup"><span data-stu-id="458e0-265">To add another extension, click **Add Exclusion** and enter another file type extension (adding a .jpeg extension).</span></span>

    ![Планирование архивации Windows Server](./media/backup-azure-manage-windows-server/exclude-jpg.png)
8. <span data-ttu-id="458e0-267">После добавления всех расширений нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="458e0-267">When you've added all the extensions, click **OK**.</span></span>
9. <span data-ttu-id="458e0-268">Продолжайте выполнять указания мастера архивации по расписанию, нажимая кнопку **Далее**, пока не откроется **страница подтверждения**. После этого нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="458e0-268">Continue through the Schedule Backup Wizard by clicking **Next** until the **Confirmation page**, then click **Finish**.</span></span>

    ![Планирование архивации Windows Server](./media/backup-azure-manage-windows-server/finish-exclusions.png)

## <a name="frequently-asked-questions"></a><span data-ttu-id="458e0-270">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="458e0-270">Frequently asked questions</span></span>
<span data-ttu-id="458e0-271">**ВОПРОС 1. В агенте службы архивации Azure для задания архивации отображается состояние "Завершено". Почему это сразу же не отражается на портале?**</span><span class="sxs-lookup"><span data-stu-id="458e0-271">**Q1. The backup job status shows as completed in the Azure backup agent, why doesn't it get reflected immediately in portal?**</span></span>

<span data-ttu-id="458e0-272">ОТВЕТ 1.</span><span class="sxs-lookup"><span data-stu-id="458e0-272">A1.</span></span> <span data-ttu-id="458e0-273">После завершения задания архивации в агенте службы архивации Azure может пройти максимум 15 минут, прежде чем это отразится на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="458e0-273">There is at maximum delay of 15 mins between the backup job status reflected in the Azure backup agent and the Azure portal.</span></span>

<span data-ttu-id="458e0-274">**Вопрос 2. Через какое время возникает оповещение при сбое задания архивации?**</span><span class="sxs-lookup"><span data-stu-id="458e0-274">**Q.2 When a backup job fails, how long does it take to raise an alert?**</span></span>

<span data-ttu-id="458e0-275">Ответ 2. Оповещение порождается в течение 20 минут после сбоя архивации в Azure.</span><span class="sxs-lookup"><span data-stu-id="458e0-275">A.2 An alert is raised within 20 mins of the Azure backup failure.</span></span>

<span data-ttu-id="458e0-276">**ВОПРОС 3. В каком случае сообщение электронной почты не будет отправлено, если уведомления настроены?**</span><span class="sxs-lookup"><span data-stu-id="458e0-276">**Q3. Is there a case where an email won’t be sent if notifications are configured?**</span></span>

<span data-ttu-id="458e0-277">ОТВЕТ 3.</span><span class="sxs-lookup"><span data-stu-id="458e0-277">A3.</span></span> <span data-ttu-id="458e0-278">Ниже приведены случаи, когда уведомления не будут отправляться, чтобы уменьшить количество лишних сообщений.</span><span class="sxs-lookup"><span data-stu-id="458e0-278">Below are the cases when the notification will not be sent in order to reduce the alert noise:</span></span>

* <span data-ttu-id="458e0-279">Настроена почасовая отправка уведомлений, а предупреждение возникает и устраняется в течение часа.</span><span class="sxs-lookup"><span data-stu-id="458e0-279">If notifications are configured hourly and an alert is raised and resolved within the hour</span></span>
* <span data-ttu-id="458e0-280">Задание отменено.</span><span class="sxs-lookup"><span data-stu-id="458e0-280">Job is canceled.</span></span>
* <span data-ttu-id="458e0-281">Второе задание резервного копирования не удалось выполнить, так как выполняется первое задание резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="458e0-281">Second backup job failed because original backup job is in progress.</span></span>

## <a name="troubleshooting-monitoring-issues"></a><span data-ttu-id="458e0-282">Устранение неполадок мониторинга</span><span class="sxs-lookup"><span data-stu-id="458e0-282">Troubleshooting Monitoring Issues</span></span>
<span data-ttu-id="458e0-283">**Проблема:** задания и/или оповещения от агента резервного копирования Azure не отображаются на портале.</span><span class="sxs-lookup"><span data-stu-id="458e0-283">**Issue:** Jobs and/or alerts from the Azure Backup agent do not appear in the portal.</span></span>

<span data-ttu-id="458e0-284">**Действия по устранению неполадок:** процесс ```OBRecoveryServicesManagementAgent``` отправляет данные задания и оповещение в службу архивации Azure.</span><span class="sxs-lookup"><span data-stu-id="458e0-284">**Troubleshooting steps:** The process, ```OBRecoveryServicesManagementAgent```, sends the job and alert data to the Azure Backup service.</span></span> <span data-ttu-id="458e0-285">Иногда этот процесс может зависнуть или завершить работу.</span><span class="sxs-lookup"><span data-stu-id="458e0-285">Occasionally this process can become stuck or shutdown.</span></span>

1. <span data-ttu-id="458e0-286">Чтобы убедиться, что процесс не запущен, откройте **диспетчер задач** и проверьте, работает ли процесс ```OBRecoveryServicesManagementAgent```.</span><span class="sxs-lookup"><span data-stu-id="458e0-286">To verify the process is not running, open **Task Manager** and check if the ```OBRecoveryServicesManagementAgent``` process is running.</span></span>
2. <span data-ttu-id="458e0-287">Предположим, процесс не запущен. Тогда откройте **панель управления** и просмотрите список служб.</span><span class="sxs-lookup"><span data-stu-id="458e0-287">Assuming that the process is not running, open **Control Panel** and browse the list of services.</span></span> <span data-ttu-id="458e0-288">Запустите или перезапустите **агент управления службами восстановления Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="458e0-288">Start or restart **Microsoft Azure Recovery Services Management Agent**.</span></span>

    <span data-ttu-id="458e0-289">Для получения дополнительных сведений просмотрите журналы по адресу:</span><span class="sxs-lookup"><span data-stu-id="458e0-289">For further information, browse the logs at:</span></span><br/><span data-ttu-id="458e0-290">
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` Например:</span><span class="sxs-lookup"><span data-stu-id="458e0-290">
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` For example:</span></span><br/>
   `C:\Program Files\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider0.errlog`

## <a name="next-steps"></a><span data-ttu-id="458e0-291">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="458e0-291">Next steps</span></span>
* [<span data-ttu-id="458e0-292">Восстановление Windows Server или клиента Windows из Azure</span><span class="sxs-lookup"><span data-stu-id="458e0-292">Restore Windows Server or Windows Client from Azure</span></span>](backup-azure-restore-windows-server.md)
* <span data-ttu-id="458e0-293">Дополнительную информацию о службе архивации Azure см. в статье [Обзор службы архивации Azure](backup-introduction-to-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="458e0-293">To learn more about Azure Backup, see [Azure Backup Overview](backup-introduction-to-azure-backup.md)</span></span>
* <span data-ttu-id="458e0-294">Посетите [форум о службе архивации Azure](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span><span class="sxs-lookup"><span data-stu-id="458e0-294">Visit the [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933)</span></span>
