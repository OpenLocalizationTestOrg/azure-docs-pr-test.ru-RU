---
title: "Архивация виртуальных машин Azure | Документация Майкрософт"
description: "Обнаружение, регистрация и архивация виртуальных машин Azure в хранилище служб восстановления."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "резервная копия виртуальной машины; архивация виртуальной машины; архивация и аварийное восстановление; архивация виртуальных машин ARM"
ms.assetid: 5c68481d-7be3-4e68-b87c-0961c267053e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: trinadhk;jimpark;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 40983a3de104238d09b976b5fcf2419da42c1bba
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="back-up-azure-virtual-machines-to-a-recovery-services-vault"></a><span data-ttu-id="d3235-104">Архивация виртуальных машин Azure в хранилище служб восстановления</span><span class="sxs-lookup"><span data-stu-id="d3235-104">Back up Azure virtual machines to a Recovery Services vault</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d3235-105">Резервное копирование виртуальных машин в хранилище служб восстановления</span><span class="sxs-lookup"><span data-stu-id="d3235-105">Back up VMs to Recovery Services vault</span></span>](backup-azure-arm-vms.md)
> * [<span data-ttu-id="d3235-106">Резервное копирование виртуальных машин в хранилище архивации</span><span class="sxs-lookup"><span data-stu-id="d3235-106">Back up VMs to Backup vault</span></span>](backup-azure-vms.md)
>
>

<span data-ttu-id="d3235-107">В этой статье описывается архивация виртуальных машин Azure (развернутых с помощью классической модели и модели Resource Manager) в хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="d3235-107">This article details how to back up Azure VMs (both Resource Manager-deployed and Classic-deployed) to a Recovery Services vault.</span></span> <span data-ttu-id="d3235-108">Большая часть работы, которую следует выполнить для архивации виртуальных машин, заключается в подготовке.</span><span class="sxs-lookup"><span data-stu-id="d3235-108">Most of the work for backing up VMs is the preparation.</span></span> <span data-ttu-id="d3235-109">Прежде чем начинать резервное копирование или защиту виртуальной машины, необходимо выполнить [предварительные требования](backup-azure-arm-vms-prepare.md) , чтобы подготовить среду.</span><span class="sxs-lookup"><span data-stu-id="d3235-109">Before you can back up or protect a VM, you must complete the [prerequisites](backup-azure-arm-vms-prepare.md) to prepare your environment for protecting your VMs.</span></span> <span data-ttu-id="d3235-110">После выполнения необходимых условий инициируйте операцию архивации для создания моментальных снимков виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d3235-110">Once you have completed the prerequisites, then you can initiate the backup operation to take snapshots of your VM.</span></span>


[!INCLUDE [learn about backup deployment models](../../includes/backup-deployment-models.md)]

<span data-ttu-id="d3235-111">Дополнительные сведения см. в статьях [Планирование инфраструктуры резервного копирования виртуальных машин в Azure](backup-azure-vms-introduction.md) и [Документация по виртуальным машинам](https://azure.microsoft.com/documentation/services/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="d3235-111">For more information, see the articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span>

## <a name="triggering-the-backup-job"></a><span data-ttu-id="d3235-112">Активация задания архивации</span><span class="sxs-lookup"><span data-stu-id="d3235-112">Triggering the backup job</span></span>
<span data-ttu-id="d3235-113">Политика архивации, связанная с хранилищем служб восстановления, определяет частоту и время выполнения операции архивации.</span><span class="sxs-lookup"><span data-stu-id="d3235-113">The backup policy associated with the Recovery Services vault defines how often and when the backup operation runs.</span></span> <span data-ttu-id="d3235-114">По умолчанию начальным резервным копированием является первое запланированное резервное копирование.</span><span class="sxs-lookup"><span data-stu-id="d3235-114">By default, the first scheduled backup is the initial backup.</span></span> <span data-ttu-id="d3235-115">Пока начальное резервное копирование не будет выполнено, для последнего задания резервного копирования в колонке **Задания резервного копирования** будет отображаться состояние **Предупреждение (ожидание начальной архивации)**.</span><span class="sxs-lookup"><span data-stu-id="d3235-115">Until the initial backup occurs, the Last Backup Status on the **Backup Jobs** blade shows as **Warning(initial backup pending)**.</span></span>

![Статус "В ожидании резервного копирования"](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

<span data-ttu-id="d3235-117">Если начальное резервное копирование должно начаться не скоро, советуем воспользоваться командой **Выполнить моментальную архивацию**.</span><span class="sxs-lookup"><span data-stu-id="d3235-117">Unless your initial backup is due to begin soon, it is recommended that you run **Back up Now**.</span></span> <span data-ttu-id="d3235-118">Чтобы приступить к архивации, перейдите на панель мониторинга хранилища.</span><span class="sxs-lookup"><span data-stu-id="d3235-118">The following procedure starts from the vault dashboard.</span></span> <span data-ttu-id="d3235-119">Эта процедура требуется, чтобы запустить начальную архивацию после выполнения предварительных требований.</span><span class="sxs-lookup"><span data-stu-id="d3235-119">This procedure serves for running the initial backup job after you have completed all prerequisites.</span></span> <span data-ttu-id="d3235-120">Если начальная архивация уже выполнена, эта процедура будет недоступна.</span><span class="sxs-lookup"><span data-stu-id="d3235-120">If the initial backup job has already been run, this procedure is not available.</span></span> <span data-ttu-id="d3235-121">Связанная политика архивации определяет следующее задание архивации.</span><span class="sxs-lookup"><span data-stu-id="d3235-121">The associated backup policy determines the next backup job.</span></span>  

<span data-ttu-id="d3235-122">Чтобы выполнить начальную архивацию, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="d3235-122">To run the initial backup job:</span></span>

1. <span data-ttu-id="d3235-123">На панели мониторинга хранилища щелкните число в разделе **Элементы архивации** или выберите элемент **Элементы архивации**.</span><span class="sxs-lookup"><span data-stu-id="d3235-123">On the vault dashboard, click the number under **Backup Items**, or click the **Backup Items** tile.</span></span> <br/><span data-ttu-id="d3235-124">
  ![Значок "Параметры"](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span><span class="sxs-lookup"><span data-stu-id="d3235-124">
![Settings icon](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span></span>

  <span data-ttu-id="d3235-125">Откроется колонка **Элементы архивации** .</span><span class="sxs-lookup"><span data-stu-id="d3235-125">The **Backup Items** blade opens.</span></span>

  ![Элементы архивации](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. <span data-ttu-id="d3235-127">В колонке **Элементы архивации** выберите элемент.</span><span class="sxs-lookup"><span data-stu-id="d3235-127">On the **Backup Items** blade, select the item.</span></span>

  ![Значок "Параметры"](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  <span data-ttu-id="d3235-129">Откроется список **Элементы архивации**.</span><span class="sxs-lookup"><span data-stu-id="d3235-129">The **Backup Items** list opens.</span></span> <br/>

  ![Задание резервного копирования активировано](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. <span data-ttu-id="d3235-131">В списке **Элементы архивации** нажмите кнопку с многоточием **...**, чтобы открыть контекстное меню.</span><span class="sxs-lookup"><span data-stu-id="d3235-131">On the **Backup Items** list, click the ellipses **...** to open the Context menu.</span></span>

  ![Контекстное меню](./media/backup-azure-vms-first-look-arm/context-menu.png)

  <span data-ttu-id="d3235-133">Откроется контекстное меню.</span><span class="sxs-lookup"><span data-stu-id="d3235-133">The Context menu appears.</span></span>

  ![Контекстное меню](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. <span data-ttu-id="d3235-135">В контекстном меню выберите команду **Выполнить моментальную архивацию**.</span><span class="sxs-lookup"><span data-stu-id="d3235-135">On the Context menu, click **Backup now**.</span></span>

  ![Контекстное меню](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  <span data-ttu-id="d3235-137">Откроется колонка "Моментальная архивация".</span><span class="sxs-lookup"><span data-stu-id="d3235-137">The Backup Now blade opens.</span></span>

  ![Показана колонка "Моментальная архивация"](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. <span data-ttu-id="d3235-139">В колонке "Моментальная архивация" щелкните значок календаря и с помощью элементов управления календарем выберите последний день сохранения этой точки восстановления, а затем нажмите кнопку **Архивировать**.</span><span class="sxs-lookup"><span data-stu-id="d3235-139">On the Backup Now blade, click the calendar icon, use the calendar control to select the last day this recovery point is retained, and click **Backup**.</span></span>

  ![Установка последнего дня сохранения точки восстановления моментальной архивации](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  <span data-ttu-id="d3235-141">Уведомления о развертывании извещают о том, что задание архивации запущено и что ход его выполнения можно отслеживать на странице заданий архивации.</span><span class="sxs-lookup"><span data-stu-id="d3235-141">Deployment notifications let you know the backup job has been triggered, and that you can monitor the progress of the job on the Backup jobs page.</span></span> <span data-ttu-id="d3235-142">В зависимости от размера виртуальной машины создание начального архива может занять некоторое время.</span><span class="sxs-lookup"><span data-stu-id="d3235-142">Depending on the size of your VM, creating the initial backup may take a while.</span></span>

6. <span data-ttu-id="d3235-143">Чтобы проверить или отследить состояние начальной архивации, на панели мониторинга хранилища в элементе **Задания архивации** щелкните **Выполняется**.</span><span class="sxs-lookup"><span data-stu-id="d3235-143">To view or track the status of the initial backup, on the vault dashboard, on the **Backup Jobs** tile click **In progress**.</span></span>

  ![Элемент "Задания резервного копирования"](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  <span data-ttu-id="d3235-145">После этого откроется колонка "Задания резервного копирования".</span><span class="sxs-lookup"><span data-stu-id="d3235-145">The Backup Jobs blade opens.</span></span>

  ![Элемент "Задания резервного копирования"](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  <span data-ttu-id="d3235-147">В колонке **Задания архивации** можно просмотреть состояние всех заданий.</span><span class="sxs-lookup"><span data-stu-id="d3235-147">In the **Backup jobs** blade, you can see the status of all jobs.</span></span> <span data-ttu-id="d3235-148">Проверьте, выполняется ли еще ваше задание архивации для виртуальной машины или уже выполнено.</span><span class="sxs-lookup"><span data-stu-id="d3235-148">Check if the backup job for your VM is still in progress, or if it has finished.</span></span> <span data-ttu-id="d3235-149">Когда задание архивации выполнено, состояние меняется на *Завершено*.</span><span class="sxs-lookup"><span data-stu-id="d3235-149">When a backup job is finished, the status is *Completed*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="d3235-150">В ходе резервного копирования служба архивации Azure дает команду расширению для резервного копирования на каждой виртуальной машине сохранять на диск все данные операций записи и делать согласованный моментальный снимок.</span><span class="sxs-lookup"><span data-stu-id="d3235-150">As a part of the backup operation, the Azure Backup service issues a command to the backup extension in each VM to flush all writes and take a consistent snapshot.</span></span>
  >
  >

## <a name="troubleshooting-errors"></a><span data-ttu-id="d3235-151">Устранение ошибок</span><span class="sxs-lookup"><span data-stu-id="d3235-151">Troubleshooting errors</span></span>
<span data-ttu-id="d3235-152">Если во время архивации виртуальной машины возникнут проблемы, ознакомьтесь со [статьей об устранении неполадок виртуальной машины](backup-azure-vms-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="d3235-152">If you run into issues while backing up your virtual machine, see the [VM troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3235-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d3235-153">Next steps</span></span>
<span data-ttu-id="d3235-154">Теперь, когда вы защитили виртуальную машину, ознакомьтесь со следующими статьями, чтобы узнать о задачах управления виртуальными машинами и их восстановлении.</span><span class="sxs-lookup"><span data-stu-id="d3235-154">Now that you have protected your VM, see the following articles to learn about VM management tasks, and how to restore VMs.</span></span>

* [<span data-ttu-id="d3235-155">Мониторинг виртуальных машин и управление ими</span><span class="sxs-lookup"><span data-stu-id="d3235-155">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="d3235-156">Восстановление виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="d3235-156">Restore virtual machines</span></span>](backup-azure-arm-restore-vms.md)
