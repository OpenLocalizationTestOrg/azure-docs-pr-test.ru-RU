---
title: "монитор и aaaManage резервных копий виртуальной машины Azure | Документы Microsoft"
description: "Узнайте, как toomanage и монитор Azure виртуальные машины резервных копий"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 4372944e-d33a-4f6a-bd5f-d04af2842713
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: trinadhk;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cb95e0b3760c96f7fd563c42cb4c635553f48957
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-common-azure-backup-jobs-and-trigger-alerts-in-hello-classic-portal"></a><span data-ttu-id="6d8c0-103">Управление оповещения триггер hello классическом портале и Общие задания резервного копирования Azure</span><span class="sxs-lookup"><span data-stu-id="6d8c0-103">Manage common Azure Backup jobs and trigger alerts in hello classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6d8c0-104">Управление архивацией виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="6d8c0-104">Manage Azure VM backups</span></span>](backup-azure-manage-vms.md)
> * [<span data-ttu-id="6d8c0-105">Управление архивацией классических виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="6d8c0-105">Manage Classic VM backups</span></span>](backup-azure-manage-vms-classic.md)
>
>

<span data-ttu-id="6d8c0-106">В этой статье содержится информация об общих задачах управления и мониторинга для виртуальных машин классической модели, защищенных в Azure.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-106">This article provides information about common management and monitoring tasks for Classic-model virtual machines protected in Azure.</span></span>  

> [!NOTE]
> <span data-ttu-id="6d8c0-107">В Azure предусмотрены две модели развертывания, позволяющие создавать ресурсы и работать с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6d8c0-107">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6d8c0-108">В разделе [подготовки вашей среды tooback копирование виртуальных машин Azure](backup-azure-vms-prepare.md) подробные сведения по работе с развертыванием классической модели виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-108">See [Prepare your environment tooback up Azure virtual machines](backup-azure-vms-prepare.md) for details on working with Classic deployment model VMs.</span></span>
>
> [!IMPORTANT]
><span data-ttu-id="6d8c0-109">Запуск марта 2017 г., можно использовать больше не hello классического портала toocreate резервное копирование хранилищ.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-109">Starting March 2017, you can no longer use hello classic portal toocreate Backup vaults.</span></span>
>
> <span data-ttu-id="6d8c0-110">Теперь можно обновить вашими хранилищами служб tooRecovery хранилища резервной копии.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-110">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="6d8c0-111">Дополнительные сведения см. в статье hello [обновление tooa хранилища резервной копии, в хранилище служб восстановления](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="6d8c0-111">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="6d8c0-112">Корпорация Майкрософт рекомендует tooupgrade вашей резервных хранилищ tooRecovery хранилищами служб.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-112">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="6d8c0-113">После 15 октября 2017 г. нельзя использовать PowerShell toocreate резервное копирование хранилищ.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-113">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="6d8c0-114">**К 1 ноября 2017 года**:</span><span class="sxs-lookup"><span data-stu-id="6d8c0-114">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="6d8c0-115">Все оставшиеся хранилища резервной копии будет автоматически обновленные tooRecovery хранилищами служб.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-115">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="6d8c0-116">Вы не будет возможности tooaccess данные резервной копии hello классического портала.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-116">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="6d8c0-117">Вместо этого используйте hello Azure портала tooaccess резервного копирования данных в хранилищах службы восстановления.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-117">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>

## <a name="manage-protected-virtual-machines"></a><span data-ttu-id="6d8c0-118">Управление защищенными виртуальными машинами</span><span class="sxs-lookup"><span data-stu-id="6d8c0-118">Manage protected virtual machines</span></span>
<span data-ttu-id="6d8c0-119">toomanage защищенных виртуальных машин:</span><span class="sxs-lookup"><span data-stu-id="6d8c0-119">toomanage protected virtual machines:</span></span>

1. <span data-ttu-id="6d8c0-120">tooview и управление параметрами резервного копирования для виртуальной машины нажмите кнопку hello **защищенные элементы** вкладки.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-120">tooview and manage backup settings for a virtual machine click hello **Protected Items** tab.</span></span>
2. <span data-ttu-id="6d8c0-121">Щелкните имя hello hello защищенного элемента toosee **сведения об архивации** вкладки, которая позволяет получить сведения о последней резервной копии hello.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-121">Click on hello name of a protected item toosee hello **Backup Details** tab, which shows you information about hello last backup.</span></span>

    ![Резервное копирование виртуальной машины](./media/backup-azure-manage-vms/backup-vmdetails.png)
3. <span data-ttu-id="6d8c0-123">tooview и управления ими параметры политики резервного копирования для виртуальной машины нажмите кнопку hello **политики** вкладки.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-123">tooview and manage backup policy settings for a virtual machine click hello **Policies** tab.</span></span>

    ![Политика резервного копирования виртуальных машин](./media/backup-azure-manage-vms/manage-policy-settings.png)

    <span data-ttu-id="6d8c0-125">Hello **политики резервного копирования** вкладке показана hello существующую политику.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-125">hello **Backup Policies** tab shows you hello existing policy.</span></span> <span data-ttu-id="6d8c0-126">Ее параметры можно изменить при необходимости.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-126">You can modify as needed.</span></span> <span data-ttu-id="6d8c0-127">Если требуется toocreate новой политики нажмите кнопку **создать** на hello **политики** страницы.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-127">If you need toocreate a new policy click **Create** on hello **Policies** page.</span></span> <span data-ttu-id="6d8c0-128">Обратите внимание, что если требуется tooremove политику его не следует все виртуальные машины, связанные с ним.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-128">Note that if you want tooremove a policy it shouldn't have any virtual machines associated with it.</span></span>

    ![Политика резервного копирования виртуальных машин](./media/backup-azure-manage-vms/backup-vmpolicy.png)
4. <span data-ttu-id="6d8c0-130">Можно получить дополнительные сведения о действия и состояние для виртуальной машины на hello **заданий** страницы.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-130">You can get more information about actions or status for a virtual machine on hello **Jobs** page.</span></span> <span data-ttu-id="6d8c0-131">Дополнительную информацию или фильтрации заданий для конкретной виртуальной машины, выберите задание в списке tooget hello.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-131">Click a job in hello list tooget more details, or filter jobs for a specific virtual machine.</span></span>

    ![Задания](./media/backup-azure-manage-vms/backup-job.png)

## <a name="on-demand-backup-of-a-virtual-machine"></a><span data-ttu-id="6d8c0-133">Резервное копирование виртуальной машины по запросу</span><span class="sxs-lookup"><span data-stu-id="6d8c0-133">On-demand backup of a virtual machine</span></span>
<span data-ttu-id="6d8c0-134">Резервное копирование виртуальной машины по запросу можно выполнять, когда для нее настроена защита.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-134">You can take an on-demand backup of a virtual machine once it is configured for protection.</span></span> <span data-ttu-id="6d8c0-135">Если ожидается hello начальной резервной копии для hello виртуальной машины, резервное копирование по требованию создаст полная копия виртуальной машины hello в резервное хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-135">If hello initial backup is pending for hello virtual machine, on-demand backup will create a full copy of hello virtual machine in Azure backup vault.</span></span> <span data-ttu-id="6d8c0-136">Если после завершения первой резервной копии по требованию резервного копирования будет только для отправки изменений из предыдущей резервной копии для резервного копирования tooAzure хранилище т. е. он всегда является последовательным.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-136">If first backup is completed, on-demand backup will only send changes from previous backup tooAzure backup vault i.e. it is always incremental.</span></span>

> [!NOTE]
> <span data-ttu-id="6d8c0-137">Диапазон хранения данных из резервной копии по требованию устанавливается значение tooretention ежедневное сохранение в соответствующий toohello политику резервного копирования виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-137">Retention range of an on-demand backup is set tooretention value specified for Daily retention in backup policy corresponding toohello VM.</span></span>  
>
>

<span data-ttu-id="6d8c0-138">резервное копирование по требованию tootake виртуальной машины:</span><span class="sxs-lookup"><span data-stu-id="6d8c0-138">tootake an on-demand backup of a virtual machine:</span></span>

1. <span data-ttu-id="6d8c0-139">Перейдите toohello **защищенные элементы** и выберите **виртуальной машине Azure** как **тип** (если он еще не выбран) и нажмите кнопку **выберите**кнопки.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-139">Navigate toohello **Protected Items** page and select **Azure Virtual Machine** as **Type** (if not already selected) and click on **Select** button.</span></span>

    ![Тип виртуальной машины](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="6d8c0-141">Выберите hello виртуальную машину, на котором tootake по требованию резервного копирования и щелкните на **создать резервную копию сейчас** кнопку внизу hello страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-141">Select hello virtual machine on which you want tootake an on-demand backup and click on **Backup Now** button at hello bottom of hello page.</span></span>

    ![Создать резервную копию](./media/backup-azure-manage-vms/backup-now.png)

    <span data-ttu-id="6d8c0-143">Задание резервного копирования создается в hello выбранной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-143">This will create a backup job on hello selected virtual machine.</span></span> <span data-ttu-id="6d8c0-144">Диапазон хранения точки восстановления, созданные с помощью этого задания будет совпадает с указанным в политике hello, связанных с виртуальной машиной hello.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-144">Retention range of recovery point created through this job will be same as that specified in hello policy associated with hello virtual machine.</span></span>

    ![Создание задания резервного копирования](./media/backup-azure-manage-vms/creating-job.png)

   > [!NOTE]
   > <span data-ttu-id="6d8c0-146">tooview hello политики, связанные с виртуальной машиной, переход вниз к виртуальной машине в hello **защищенные элементы** страницы и последовательно выберите toobackup вкладка политики.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-146">tooview hello policy associated with a virtual machine, drill down into virtual machine in hello **Protected Items** page and go toobackup policy tab.</span></span>
   >
   >
3. <span data-ttu-id="6d8c0-147">После создания задания hello, можно щелкнуть **просмотреть задание** кнопку в hello всплывающие панели toosee hello соответствующее задание на странице приветствия заданий.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-147">Once hello job is created, you can click on **View job** button in hello toast bar toosee hello corresponding job in hello jobs page.</span></span>

    ![Задание резервного копирования создано](./media/backup-azure-manage-vms/created-job.png)
4. <span data-ttu-id="6d8c0-149">После успешного завершения задания hello точка восстановления создается которого производится toorestore hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-149">After successful completion of hello job, a recovery point will be created which you can use toorestore hello virtual machine.</span></span> <span data-ttu-id="6d8c0-150">Это также увеличивает значение столбца точки восстановления hello на 1 в **защищенные элементы** страницы.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-150">This will also increment hello recovery point column value by 1 in **Protected Items** page.</span></span>

## <a name="stop-protecting-virtual-machines"></a><span data-ttu-id="6d8c0-151">Отключение защиты виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="6d8c0-151">Stop protecting virtual machines</span></span>
<span data-ttu-id="6d8c0-152">Вы можете toostop hello следующие операции резервного копирования виртуальной машины с hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="6d8c0-152">You can choose toostop hello future backups of a virtual machine with hello following options:</span></span>

* <span data-ttu-id="6d8c0-153">Сохранить резервную копию данных, связанную с виртуальной машиной, в хранилище службы архивации Azure.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-153">Retain backup data associated with virtual machine in Azure Backup vault</span></span>
* <span data-ttu-id="6d8c0-154">Удалить резервную копию данных, связанную с виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-154">Delete backup data associated with virtual machine</span></span>

<span data-ttu-id="6d8c0-155">При выборе tooretain резервных копий данных, связанных с виртуальной машиной, можно использовать hello резервного копирования данных toorestore hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-155">If you have selected tooretain backup data associated with virtual machine, you can use hello backup data toorestore hello virtual machine.</span></span> <span data-ttu-id="6d8c0-156">Для получения дополнительных сведений о ценах для таких виртуальных машин щелкните [здесь](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="6d8c0-156">For pricing details for such virtual machines, click [here](https://azure.microsoft.com/pricing/details/backup/).</span></span>

<span data-ttu-id="6d8c0-157">tooStop защиты для виртуальной машины:</span><span class="sxs-lookup"><span data-stu-id="6d8c0-157">tooStop protection for a virtual machine:</span></span>

1. <span data-ttu-id="6d8c0-158">Перейдите слишком**защищенные элементы** и выберите **виртуальной машины Azure** hello тип фильтра (если он еще не выбран) и нажмите на **выберите** кнопки.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-158">Navigate too**Protected Items** page and select **Azure virtual machine** as hello filter type (if not already selected) and click on **Select** button.</span></span>

    ![Тип виртуальной машины](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="6d8c0-160">Выделите hello виртуальной машины и выберите команду **остановить защиту** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-160">Select hello virtual machine and click on **Stop Protection** at hello bottom of hello page.</span></span>

    ![остановка защиты;](./media/backup-azure-manage-vms/stop-protection.png)
3. <span data-ttu-id="6d8c0-162">По умолчанию Azure Backup не удаляет hello резервных копий данных, связанных с виртуальной машиной hello.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-162">By default, Azure Backup doesn’t delete hello backup data associated with hello virtual machine.</span></span>

    ![Подтверждение остановки защиты](./media/backup-azure-manage-vms/confirm-stop-protection.png)

    <span data-ttu-id="6d8c0-164">Если вы хотите toodelete резервного копирования данные, установите флажок hello.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-164">If you want toodelete backup data, select hello check box.</span></span>

    ![Флажок](./media/backup-azure-manage-vms/checkbox.png)

    <span data-ttu-id="6d8c0-166">Выберите причину остановки hello резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-166">Please select a reason for stopping hello backup.</span></span> <span data-ttu-id="6d8c0-167">Хотя это необязательно, предоставления причины способствуют toowork резервного копирования Azure на отзывах hello и определять их приоритеты hello клиентских сценариев.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-167">While this is optional, providing a reason will help Azure Backup toowork on hello feedback and prioritize hello customer scenarios.</span></span>
4. <span data-ttu-id="6d8c0-168">Щелкните **отправить** hello toosubmit кнопку **остановить защиту** задания.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-168">Click on **Submit** button toosubmit hello **Stop protection** job.</span></span> <span data-ttu-id="6d8c0-169">Щелкните **просмотреть задание** toosee hello соответствующее задание hello в **заданий** страницы.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-169">Click on **View Job** toosee hello corresponding hello job in **Jobs** page.</span></span>

    ![остановка защиты;](./media/backup-azure-manage-vms/stop-protect-success.png)

    <span data-ttu-id="6d8c0-171">Если вы не выбрали **удаление связанных архивируемых данных** во время **остановить защиту** защиты мастера, а затем post завершения задания, состояние изменяется слишком**защита останавливается**.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-171">If you have not selected **Delete associated backup data** option during **Stop Protection** wizard, then post job completion, protection status changes too**Protection Stopped**.</span></span> <span data-ttu-id="6d8c0-172">Hello данные остаются в службе архивации Azure, пока будет явно удален.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-172">hello data remains with Azure Backup until it is explicitly deleted.</span></span> <span data-ttu-id="6d8c0-173">Hello данных всегда можно удалить, выбрав hello виртуальной машины в hello **защищенные элементы** странице и нажав кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-173">You can always delete hello data by selecting hello virtual machine in hello **Protected Items** page and clicking **Delete**.</span></span>

    ![Защита остановлена](./media/backup-azure-manage-vms/protection-stopped-status.png)

    <span data-ttu-id="6d8c0-175">Если вы выбрали hello **удаление связанных архивируемых данных** , то hello виртуальной машины не будет частью hello **защищенные элементы** страницы.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-175">If you have selected hello **Delete associated backup data** option, hello virtual machine won’t be part of hello **Protected Items** page.</span></span>

## <a name="re-protect-virtual-machine"></a><span data-ttu-id="6d8c0-176">Повторное включение защиты для виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="6d8c0-176">Re-protect Virtual machine</span></span>
<span data-ttu-id="6d8c0-177">Если вы не выбрали hello **связан резервного копирования данных для удаления** в диалоговом окне **остановить защиту**, можно повторно защитить hello виртуальной машины, следуя hello toobacking аналогичные шаги вверх зарегистрированные виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-177">If you have not selected hello **Delete associate backup data** option in **Stop Protection**, you can re-protect hello virtual machine by following hello steps similar toobacking up registered virtual machines.</span></span> <span data-ttu-id="6d8c0-178">После защищен, эта виртуальная машина резервного копирования данных, остающихся предыдущих toostop защита будет и точки восстановления, созданные после защиты.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-178">Once protected, this virtual machine will have backup data retained prior toostop protection and recovery points created after re-protect.</span></span>

<span data-ttu-id="6d8c0-179">После снова включить защиту, будет изменять состояние защиты виртуальной машины hello слишком**Protected** при наличии точки восстановления предыдущих слишком**остановить защиту**.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-179">After re-protect, hello virtual machine’s protection status will be changed too**Protected** if there are recovery points prior too**Stop Protection**.</span></span>

  ![Виртуальная машина защищена повторно](./media/backup-azure-manage-vms/reprotected-status.png)

> [!NOTE]
> <span data-ttu-id="6d8c0-181">При повторная защита виртуальной машины hello, можно выбрать различные политики, чем политика hello, с которой изначально было защиту виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-181">When re-protecting hello virtual machine, you can choose a different policy than hello policy with which virtual machine was protected initially.</span></span>
>
>

## <a name="unregister-virtual-machines"></a><span data-ttu-id="6d8c0-182">Отмена регистрации виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="6d8c0-182">Unregister virtual machines</span></span>
<span data-ttu-id="6d8c0-183">Если нужно tooremove hello виртуальной машины из резервного хранилища hello:</span><span class="sxs-lookup"><span data-stu-id="6d8c0-183">If you want tooremove hello virtual machine from hello backup vault:</span></span>

1. <span data-ttu-id="6d8c0-184">Щелкните hello **UNREGISTER** кнопку внизу hello страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-184">Click on hello **UNREGISTER** button at hello bottom of hello page.</span></span>

    ![Отключение защиты](./media/backup-azure-manage-vms/unregister-button.png)

    <span data-ttu-id="6d8c0-186">Всплывающее уведомление будет отображаться в hello нижней части экрана приветствия, запрос на подтверждение.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-186">A toast notification will appear at hello bottom of hello screen requesting confirmation.</span></span> <span data-ttu-id="6d8c0-187">Нажмите кнопку **Да** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-187">Click **YES** toocontinue.</span></span>

    ![Отключение защиты](./media/backup-azure-manage-vms/confirm-unregister.png)

## <a name="delete-backup-data"></a><span data-ttu-id="6d8c0-189">Удаление данных резервных копий</span><span class="sxs-lookup"><span data-stu-id="6d8c0-189">Delete Backup data</span></span>
<span data-ttu-id="6d8c0-190">Можно удалить hello резервных копий данных, связанных с виртуальной машиной, как:</span><span class="sxs-lookup"><span data-stu-id="6d8c0-190">You can delete hello backup data associated with a virtual machine, either:</span></span>

* <span data-ttu-id="6d8c0-191">либо во время выполнения задания остановки защиты,</span><span class="sxs-lookup"><span data-stu-id="6d8c0-191">During Stop Protection Job</span></span>
* <span data-ttu-id="6d8c0-192">либо по окончании данного задания на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-192">After a stop protection job is completed on a virtual machine</span></span>

<span data-ttu-id="6d8c0-193">toodelete резервного копирования данных на виртуальной машине, расположенной в hello *защита останавливается* состояние учета успешного завершения **остановка резервного копирования** задания:</span><span class="sxs-lookup"><span data-stu-id="6d8c0-193">toodelete backup data on a virtual machine, which is in hello *Protection Stopped* state post successful completion of a **Stop Backup** job:</span></span>

1. <span data-ttu-id="6d8c0-194">Перейдите toohello **защищенные элементы** и выберите **виртуальной машине Azure** как *тип* и нажмите кнопку hello **выберите** кнопки.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-194">Navigate toohello **Protected Items** page and select **Azure Virtual Machine** as *type* and click hello **Select** button.</span></span>

    ![Тип виртуальной машины](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="6d8c0-196">Выберите виртуальную машину hello.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-196">Select hello virtual machine.</span></span> <span data-ttu-id="6d8c0-197">Hello виртуальная машина будет в **защита останавливается** состояния.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-197">hello virtual machine will be in **Protection Stopped** state.</span></span>

    ![Защита остановлена](./media/backup-azure-manage-vms/protection-stopped-b.png)
3. <span data-ttu-id="6d8c0-199">Нажмите кнопку hello **удалить** кнопку внизу hello страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-199">Click hello **DELETE** button at hello bottom of hello page.</span></span>

    ![Удаление резервных копий](./media/backup-azure-manage-vms/delete-backup.png)
4. <span data-ttu-id="6d8c0-201">В hello **удаления архивируемых данных** мастера выберите причину удаления резервного копирования данных (настоятельно рекомендуется) и нажмите кнопку **отправить**.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-201">In hello **Delete backup data** wizard, select a reason for deleting backup data (highly recommended) and click **Submit**.</span></span>

    ![удаление резервных копий;](./media/backup-azure-manage-vms/delete-backup-data.png)
5. <span data-ttu-id="6d8c0-203">Будет создано задание toodelete архивируемых данных выбранной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-203">This will create a job toodelete backup data of selected virtual machine.</span></span> <span data-ttu-id="6d8c0-204">Нажмите кнопку **просмотреть задание** toosee соответствующее задание на странице заданий.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-204">Click **View job** toosee corresponding job in Jobs page.</span></span>

    ![Удаление данных выполнено](./media/backup-azure-manage-vms/delete-data-success.png)

    <span data-ttu-id="6d8c0-206">После завершения задания hello hello запись, соответствующая виртуальная машина toohello будут удалены из **защищенные элементы** страницы.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-206">Once hello job is completed, hello entry corresponding toohello virtual machine will be removed from **Protected items** page.</span></span>

## <a name="dashboard"></a><span data-ttu-id="6d8c0-207">Панель мониторинга</span><span class="sxs-lookup"><span data-stu-id="6d8c0-207">Dashboard</span></span>
<span data-ttu-id="6d8c0-208">На hello **мониторинга** страницы, можно просмотреть сведения о виртуальных машинах Azure, хранилища и задания, связанные с ними hello последние 24 часа.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-208">On hello **Dashboard** page you can review information about Azure virtual machines, their storage, and jobs associated with them in hello last 24 hours.</span></span> <span data-ttu-id="6d8c0-209">Здесь также можно просмотреть состояние резервного копирования и все связанные с ним ошибки.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-209">You can view backup status and any associated backup errors.</span></span>

![Панель мониторинга](./media/backup-azure-manage-vms/dashboard-protectedvms.png)

> [!NOTE]
> <span data-ttu-id="6d8c0-211">Значения в панель мониторинга hello обновляются каждые 24 часа.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-211">Values in hello dashboard are refreshed once every 24 hours.</span></span>
>
>

## <a name="auditing-operations"></a><span data-ttu-id="6d8c0-212">Аудит операций</span><span class="sxs-lookup"><span data-stu-id="6d8c0-212">Auditing Operations</span></span>
<span data-ttu-id="6d8c0-213">Резервное копирование Azure предоставляет обзор hello «журналы операций» операции резервного копирования вызвано hello клиента, что позволяет легко toosee точно какие операции управления проводились hello резервного хранилища.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-213">Azure backup provides review of hello "operation logs" of backup operations triggered by hello customer making it easy toosee exactly what management operations were performed on hello backup vault.</span></span> <span data-ttu-id="6d8c0-214">Журналы операций включить значительные после неустранимого и аудита для операций резервного копирования hello.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-214">Operations logs enable great post-mortem and audit support for hello backup operations.</span></span>

<span data-ttu-id="6d8c0-215">следующие операции Hello регистрируются в журналах операций:</span><span class="sxs-lookup"><span data-stu-id="6d8c0-215">hello following operations are logged in Operation logs:</span></span>

* <span data-ttu-id="6d8c0-216">регистрация;</span><span class="sxs-lookup"><span data-stu-id="6d8c0-216">Register</span></span>
* <span data-ttu-id="6d8c0-217">Unregister; </span><span class="sxs-lookup"><span data-stu-id="6d8c0-217">Unregister</span></span>
* <span data-ttu-id="6d8c0-218">настройка защиты;</span><span class="sxs-lookup"><span data-stu-id="6d8c0-218">Configure protection</span></span>
* <span data-ttu-id="6d8c0-219">резервное копирование (как запланированное, так и запущенное по запросу с помощью кнопки «Моментальная архивация»);</span><span class="sxs-lookup"><span data-stu-id="6d8c0-219">Backup ( Both scheduled as well as on-demand backup through BackupNow)</span></span>
* <span data-ttu-id="6d8c0-220">восстановление;</span><span class="sxs-lookup"><span data-stu-id="6d8c0-220">Restore</span></span>
* <span data-ttu-id="6d8c0-221">остановка защиты;</span><span class="sxs-lookup"><span data-stu-id="6d8c0-221">Stop protection</span></span>
* <span data-ttu-id="6d8c0-222">удаление резервных копий;</span><span class="sxs-lookup"><span data-stu-id="6d8c0-222">Delete backup data</span></span>
* <span data-ttu-id="6d8c0-223">добавление политики;</span><span class="sxs-lookup"><span data-stu-id="6d8c0-223">Add policy</span></span>
* <span data-ttu-id="6d8c0-224">удаление политики;</span><span class="sxs-lookup"><span data-stu-id="6d8c0-224">Delete policy</span></span>
* <span data-ttu-id="6d8c0-225">изменение политики;</span><span class="sxs-lookup"><span data-stu-id="6d8c0-225">Update policy</span></span>
* <span data-ttu-id="6d8c0-226">отмена задания.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-226">Cancel job</span></span>

<span data-ttu-id="6d8c0-227">Операция tooview регистрирует соответствующего резервного хранилища tooa:</span><span class="sxs-lookup"><span data-stu-id="6d8c0-227">tooview operation logs corresponding tooa backup vault:</span></span>

1. <span data-ttu-id="6d8c0-228">Перейдите в слишком**службы управления** на портале Azure и нажмите кнопку hello **журналы операций** вкладку.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-228">Navigate too**Management services** in Azure portal, and then click hello **Operation Logs** tab.</span></span>

    ![Журналы операций](./media/backup-azure-manage-vms/ops-logs.png)
2. <span data-ttu-id="6d8c0-230">В фильтрах hello выберите **резервного копирования** как *тип* и укажите имя резервного хранилища hello в *имя службы* и выберите команду **отправить**.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-230">In hello filters, select **Backup** as *Type* and specify hello backup vault name in *service name* and click on **Submit**.</span></span>

    ![Фильтр журналов операций](./media/backup-azure-manage-vms/ops-logs-filter.png)
3. <span data-ttu-id="6d8c0-232">В журналах операций hello, выберите любой операции и нажмите кнопку **сведения** toosee сведения о соответствующей операции tooan.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-232">In hello operations logs, select any operation and click  **Details** toosee details corresponding tooan operation.</span></span>

    ![Сведения о выборке из журналов операций](./media/backup-azure-manage-vms/ops-logs-details.png)

    <span data-ttu-id="6d8c0-234">Hello **сведения о мастере** содержит сведения об активации операции hello задание с ИД ресурса, на котором эта операция, а также время начала операции hello.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-234">hello **Details wizard** contains information about hello operation triggered, job Id, resource on which this operation is triggered, and start time of hello operation.</span></span>

    ![Сведения об операции](./media/backup-azure-manage-vms/ops-logs-details-window.png)

## <a name="alert-notifications"></a><span data-ttu-id="6d8c0-236">Оповещения</span><span class="sxs-lookup"><span data-stu-id="6d8c0-236">Alert notifications</span></span>
<span data-ttu-id="6d8c0-237">Пользовательские уведомления о предупреждениях для hello заданий можно получить на портале.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-237">You can get custom alert notifications for hello jobs in portal.</span></span> <span data-ttu-id="6d8c0-238">Для этого в PowerShell нужно определить правила оповещений для событий журналов операций.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-238">This is achieved by defining PowerShell-based alert rules on operational logs events.</span></span> <span data-ttu-id="6d8c0-239">Мы рекомендуем использовать *PowerShell версии 1.3.0 или более поздней*.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-239">We recommend using *PowerShell version 1.3.0 or above*.</span></span>

<span data-ttu-id="6d8c0-240">Пример команды toodefine tooalert настраиваемое уведомление наличие ошибок резервного копирования, будет выглядеть как:</span><span class="sxs-lookup"><span data-stu-id="6d8c0-240">toodefine a custom notification tooalert for backup failures, a sample command will look like:</span></span>

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.Backup/backupVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/microsoft.backupbvtd2/BackupVault/trinadhVault -Actions $actionEmail
```

<span data-ttu-id="6d8c0-241">**ResourceId**. Этот параметр можно получить во всплывающем окне "Журналы операций", как описано в разделе выше.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-241">**ResourceId**: You can get this from Operations Logs popup as described in above section.</span></span> <span data-ttu-id="6d8c0-242">ResourceUri в всплывающем окне сведения об операции является toobe ResourceId hello, предоставленный для этого командлета.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-242">ResourceUri in details popup window of an operation is hello ResourceId toobe supplied for this cmdlet.</span></span>

<span data-ttu-id="6d8c0-243">**Имя_операции**: это будет hello формата «Microsoft.Backup/backupvault/<EventName>» где EventName — это одна из регистра, отменить регистрацию, ConfigureProtection, резервное копирование, восстановление, StopProtection, DeleteBackupData, UpdateProtectionPolicy CreateProtectionPolicy DeleteProtectionPolicy,</span><span class="sxs-lookup"><span data-stu-id="6d8c0-243">**OperationName**: This will be of hello format "Microsoft.Backup/backupvault/<EventName>" where EventName is one of Register,Unregister,ConfigureProtection,Backup,Restore,StopProtection,DeleteBackupData,CreateProtectionPolicy,DeleteProtectionPolicy,UpdateProtectionPolicy</span></span>

<span data-ttu-id="6d8c0-244">**Status**. Поддерживаемые значения: Started, Succeeded и Failed.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-244">**Status**: Supported values are- Started, Succeeded and Failed.</span></span>

<span data-ttu-id="6d8c0-245">**Группа ресурсов**: группа ресурсов hello ресурса, на котором будет запущено.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-245">**ResourceGroup**:ResourceGroup of hello resource on which operation is triggered.</span></span> <span data-ttu-id="6d8c0-246">Это значение можно получить из значения ResourceId.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-246">You can obtain this from ResourceId value.</span></span> <span data-ttu-id="6d8c0-247">Значение между полями */resourceGroups/* и */providers/* в ResourceId значение является значением hello группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-247">Value between fields */resourceGroups/* and */providers/* in ResourceId value is hello value for ResourceGroup.</span></span>

<span data-ttu-id="6d8c0-248">**Имя**: имя hello правило оповещения.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-248">**Name**: Name of hello Alert Rule.</span></span>

<span data-ttu-id="6d8c0-249">**CustomEmail**: укажите hello настраиваемый электронный адрес toowhich требуется toosend уведомления о предупреждении</span><span class="sxs-lookup"><span data-stu-id="6d8c0-249">**CustomEmail**: Specify hello custom email address toowhich you want toosend alert notification</span></span>

<span data-ttu-id="6d8c0-250">**SendToServiceOwners**: этот параметр отправляет уведомления о предупреждении tooall администраторов и администраторов подписки hello.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-250">**SendToServiceOwners**: This option sends alert notification tooall administrators and co-administrators of hello subscription.</span></span> <span data-ttu-id="6d8c0-251">Кроме того, его можно использовать в командлете **New-AzureRmAlertRuleEmail**.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-251">It can be used in **New-AzureRmAlertRuleEmail** cmdlet</span></span>

### <a name="limitations-on-alerts"></a><span data-ttu-id="6d8c0-252">Связанные с оповещениями ограничения</span><span class="sxs-lookup"><span data-stu-id="6d8c0-252">Limitations on Alerts</span></span>
<span data-ttu-id="6d8c0-253">Оповещения на основе событий, которое подвергается toohello следующие ограничения:</span><span class="sxs-lookup"><span data-stu-id="6d8c0-253">Event-based alerts are subjected toohello following limitations:</span></span>

1. <span data-ttu-id="6d8c0-254">Оповещений на всех виртуальных машин в хранилище архивации hello.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-254">Alerts are triggered on all virtual machines in hello backup vault.</span></span> <span data-ttu-id="6d8c0-255">Нельзя настраивать его tooget предупреждения для конкретного набора виртуальных машин в резервное хранилище.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-255">You cannot customize it tooget alerts for specific set of virtual machines in a backup vault.</span></span>
2. <span data-ttu-id="6d8c0-256">Эта функция предоставляется в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-256">This feature is in Preview.</span></span> [<span data-ttu-id="6d8c0-257">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="6d8c0-257">Learn more</span></span>](../monitoring-and-diagnostics/insights-powershell-samples.md#create-metric-alerts)
3. <span data-ttu-id="6d8c0-258">Вы получите оповещения с адреса alerts-noreply@mail.windowsazure.com.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-258">You will receive alerts from "alerts-noreply@mail.windowsazure.com".</span></span> <span data-ttu-id="6d8c0-259">В настоящее время невозможно изменить hello электронной почты отправителя.</span><span class="sxs-lookup"><span data-stu-id="6d8c0-259">Currently you can't modify hello email sender.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d8c0-260">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6d8c0-260">Next steps</span></span>
* [<span data-ttu-id="6d8c0-261">Восстановление виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="6d8c0-261">Restore Azure VMs</span></span>](backup-azure-restore-vms.md)
