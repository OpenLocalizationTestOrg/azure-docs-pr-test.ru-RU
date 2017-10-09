---
title: "aaaBack виртуальных машин Azure | Документы Microsoft"
description: "Обнаружение, регистрации и архивировать хранилище служб восстановления tooa виртуальных машин Azure."
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
ms.openlocfilehash: a204a42726450a7fd89b5563a786b5070578b113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-tooa-recovery-services-vault"></a><span data-ttu-id="8d5a4-104">Резервное копирование виртуальных машин Azure в хранилище служб восстановления tooa</span><span class="sxs-lookup"><span data-stu-id="8d5a4-104">Back up Azure virtual machines tooa Recovery Services vault</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8d5a4-105">Резервное копирование виртуальных машин tooRecovery служб хранилища</span><span class="sxs-lookup"><span data-stu-id="8d5a4-105">Back up VMs tooRecovery Services vault</span></span>](backup-azure-arm-vms.md)
> * [<span data-ttu-id="8d5a4-106">Резервное копирование виртуальных машин tooBackup хранилища</span><span class="sxs-lookup"><span data-stu-id="8d5a4-106">Back up VMs tooBackup vault</span></span>](backup-azure-vms.md)
>
>

<span data-ttu-id="8d5a4-107">В этой статье указаны как tooback копирование tooa виртуальных машинах Azure (развертывания диспетчера ресурсов и развернутые классический) служб восстановления хранилище.</span><span class="sxs-lookup"><span data-stu-id="8d5a4-107">This article details how tooback up Azure VMs (both Resource Manager-deployed and Classic-deployed) tooa Recovery Services vault.</span></span> <span data-ttu-id="8d5a4-108">Большая часть работы hello резервного копирования виртуальных машин — Подготовка hello.</span><span class="sxs-lookup"><span data-stu-id="8d5a4-108">Most of hello work for backing up VMs is hello preparation.</span></span> <span data-ttu-id="8d5a4-109">Прежде чем можно создать резервную копию или защиты виртуальной Машины, необходимо выполнить hello [необходимые компоненты](backup-azure-arm-vms-prepare.md) tooprepare среды для защиты виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="8d5a4-109">Before you can back up or protect a VM, you must complete hello [prerequisites](backup-azure-arm-vms-prepare.md) tooprepare your environment for protecting your VMs.</span></span> <span data-ttu-id="8d5a4-110">После выполнения необходимых компонентов hello может инициировать hello операции резервного копирования tootake моментальные снимки виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="8d5a4-110">Once you have completed hello prerequisites, then you can initiate hello backup operation tootake snapshots of your VM.</span></span>


[!INCLUDE [learn about backup deployment models](../../includes/backup-deployment-models.md)]

<span data-ttu-id="8d5a4-111">Дополнительные сведения см. в статьях hello на [планирование инфраструктуры резервного копирования виртуальной Машины в Azure](backup-azure-vms-introduction.md) и [виртуальных машин Azure](https://azure.microsoft.com/documentation/services/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="8d5a4-111">For more information, see hello articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span>

## <a name="triggering-hello-backup-job"></a><span data-ttu-id="8d5a4-112">Идет запуск задания резервного копирования hello</span><span class="sxs-lookup"><span data-stu-id="8d5a4-112">Triggering hello backup job</span></span>
<span data-ttu-id="8d5a4-113">политики резервного копирования Hello, связанной с hello в хранилище служб восстановления определяет, как часто и когда выполняется операция резервного копирования hello.</span><span class="sxs-lookup"><span data-stu-id="8d5a4-113">hello backup policy associated with hello Recovery Services vault defines how often and when hello backup operation runs.</span></span> <span data-ttu-id="8d5a4-114">По умолчанию hello первого запланированного резервного копирования является hello начальной резервной копии.</span><span class="sxs-lookup"><span data-stu-id="8d5a4-114">By default, hello first scheduled backup is hello initial backup.</span></span> <span data-ttu-id="8d5a4-115">Пока не будет выполнена hello начальной резервной копии, hello состояние последнего резервного копирования на hello **заданий резервного копирования** колонке показано, как **предупреждение (начальной резервной копии ожидающих)**.</span><span class="sxs-lookup"><span data-stu-id="8d5a4-115">Until hello initial backup occurs, hello Last Backup Status on hello **Backup Jobs** blade shows as **Warning(initial backup pending)**.</span></span>

![Статус "В ожидании резервного копирования"](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

<span data-ttu-id="8d5a4-117">Если причиной является начальной резервной копии toobegin скоро, рекомендуется запускать **создать резервную копию**.</span><span class="sxs-lookup"><span data-stu-id="8d5a4-117">Unless your initial backup is due toobegin soon, it is recommended that you run **Back up Now**.</span></span> <span data-ttu-id="8d5a4-118">Hello следующая процедура начинается с hello мониторинга хранилища.</span><span class="sxs-lookup"><span data-stu-id="8d5a4-118">hello following procedure starts from hello vault dashboard.</span></span> <span data-ttu-id="8d5a4-119">Эта процедура служит для запуска задания резервного копирования начальной hello после завершения всех необходимых компонентов.</span><span class="sxs-lookup"><span data-stu-id="8d5a4-119">This procedure serves for running hello initial backup job after you have completed all prerequisites.</span></span> <span data-ttu-id="8d5a4-120">Если исходное задание резервного копирования hello уже запущена, эта процедура не доступна.</span><span class="sxs-lookup"><span data-stu-id="8d5a4-120">If hello initial backup job has already been run, this procedure is not available.</span></span> <span data-ttu-id="8d5a4-121">Hello связанные политики резервного копирования определяет hello следующего задания резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="8d5a4-121">hello associated backup policy determines hello next backup job.</span></span>  

<span data-ttu-id="8d5a4-122">toorun hello начального задания резервного копирования:</span><span class="sxs-lookup"><span data-stu-id="8d5a4-122">toorun hello initial backup job:</span></span>

1. <span data-ttu-id="8d5a4-123">На панель мониторинга хранилища hello, щелкните номер hello в **резервное копирование элементов**, или нажмите кнопку hello **резервное копирование элементов** плитки.</span><span class="sxs-lookup"><span data-stu-id="8d5a4-123">On hello vault dashboard, click hello number under **Backup Items**, or click hello **Backup Items** tile.</span></span> <br/><span data-ttu-id="8d5a4-124">
  ![Значок "Параметры"](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span><span class="sxs-lookup"><span data-stu-id="8d5a4-124">
![Settings icon](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span></span>

  <span data-ttu-id="8d5a4-125">Hello **резервное копирование элементов** открывает колонку.</span><span class="sxs-lookup"><span data-stu-id="8d5a4-125">hello **Backup Items** blade opens.</span></span>

  ![Элементы архивации](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. <span data-ttu-id="8d5a4-127">На hello **резервное копирование элементов** колонки, выберите hello элемента.</span><span class="sxs-lookup"><span data-stu-id="8d5a4-127">On hello **Backup Items** blade, select hello item.</span></span>

  ![Значок "Параметры"](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  <span data-ttu-id="8d5a4-129">Hello **резервное копирование элементов** откроется список.</span><span class="sxs-lookup"><span data-stu-id="8d5a4-129">hello **Backup Items** list opens.</span></span> <br/>

  ![Задание резервного копирования активировано](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. <span data-ttu-id="8d5a4-131">На hello **резервное копирование элементов** щелкните многоточие hello **...**  tooopen hello контекстного меню.</span><span class="sxs-lookup"><span data-stu-id="8d5a4-131">On hello **Backup Items** list, click hello ellipses **...** tooopen hello Context menu.</span></span>

  ![Контекстное меню](./media/backup-azure-vms-first-look-arm/context-menu.png)

  <span data-ttu-id="8d5a4-133">Появится контекстное меню Hello.</span><span class="sxs-lookup"><span data-stu-id="8d5a4-133">hello Context menu appears.</span></span>

  ![Контекстное меню](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. <span data-ttu-id="8d5a4-135">Hello контекстного меню, выберите команду **Архивировать сейчас**.</span><span class="sxs-lookup"><span data-stu-id="8d5a4-135">On hello Context menu, click **Backup now**.</span></span>

  ![Контекстное меню](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  <span data-ttu-id="8d5a4-137">Открывает Hello колонке создать резервную копию.</span><span class="sxs-lookup"><span data-stu-id="8d5a4-137">hello Backup Now blade opens.</span></span>

  ![Показывает, создать резервную копию колонке hello](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. <span data-ttu-id="8d5a4-139">Щелкните значок календаря hello hello резервной копии теперь колонке, используйте hello календаря управления tooselect hello последний день этой точки восстановления сохраняется и нажмите кнопку **резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="8d5a4-139">On hello Backup Now blade, click hello calendar icon, use hello calendar control tooselect hello last day this recovery point is retained, and click **Backup**.</span></span>

  ![Задайте hello последний день hello теперь резервной копии хранятся точки восстановления](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  <span data-ttu-id="8d5a4-141">Развертывание уведомлений позволяют понять, было запущено задание резервного копирования hello и отслеживать ход выполнения hello hello задания на странице заданий резервного копирования hello.</span><span class="sxs-lookup"><span data-stu-id="8d5a4-141">Deployment notifications let you know hello backup job has been triggered, and that you can monitor hello progress of hello job on hello Backup jobs page.</span></span> <span data-ttu-id="8d5a4-142">В зависимости от размера ВМ hello Создание hello начальной резервной копии может занять некоторое время.</span><span class="sxs-lookup"><span data-stu-id="8d5a4-142">Depending on hello size of your VM, creating hello initial backup may take a while.</span></span>

6. <span data-ttu-id="8d5a4-143">tooview или отслеживания hello состояние hello начальной операции резервного копирования, на панель мониторинга хранилища hello на hello **заданий резервного копирования** щелкните плитку **выполняется**.</span><span class="sxs-lookup"><span data-stu-id="8d5a4-143">tooview or track hello status of hello initial backup, on hello vault dashboard, on hello **Backup Jobs** tile click **In progress**.</span></span>

  ![Элемент "Задания резервного копирования"](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  <span data-ttu-id="8d5a4-145">Открывает колонку Hello задания резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="8d5a4-145">hello Backup Jobs blade opens.</span></span>

  ![Элемент "Задания резервного копирования"](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  <span data-ttu-id="8d5a4-147">В hello **заданий резервного копирования** колонку, вы можете просматривать состояние hello всех заданий.</span><span class="sxs-lookup"><span data-stu-id="8d5a4-147">In hello **Backup jobs** blade, you can see hello status of all jobs.</span></span> <span data-ttu-id="8d5a4-148">Если задание резервного копирования hello для ВМ по-прежнему выполняется или завершена, проверьте.</span><span class="sxs-lookup"><span data-stu-id="8d5a4-148">Check if hello backup job for your VM is still in progress, or if it has finished.</span></span> <span data-ttu-id="8d5a4-149">После завершения задания резервного копирования находится в состоянии hello *завершено*.</span><span class="sxs-lookup"><span data-stu-id="8d5a4-149">When a backup job is finished, hello status is *Completed*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="8d5a4-150">В рамках операции резервного копирования hello hello службы резервного копирования Azure выдает резервного копирования расширение toohello команды в каждой виртуальной Машины tooflush все записывает и занять согласованный моментальный снимок.</span><span class="sxs-lookup"><span data-stu-id="8d5a4-150">As a part of hello backup operation, hello Azure Backup service issues a command toohello backup extension in each VM tooflush all writes and take a consistent snapshot.</span></span>
  >
  >

## <a name="troubleshooting-errors"></a><span data-ttu-id="8d5a4-151">Устранение ошибок</span><span class="sxs-lookup"><span data-stu-id="8d5a4-151">Troubleshooting errors</span></span>
<span data-ttu-id="8d5a4-152">Если возникли проблемы во время резервного копирования виртуальной машины в разделе hello [статьи по устранению неполадок виртуальной Машины](backup-azure-vms-troubleshoot.md) для справки.</span><span class="sxs-lookup"><span data-stu-id="8d5a4-152">If you run into issues while backing up your virtual machine, see hello [VM troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d5a4-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8d5a4-153">Next steps</span></span>
<span data-ttu-id="8d5a4-154">Вы защитили ВМ, см. статью hello, следуя toolearn статьи о задачах управления виртуальной Машины и как toorestore виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="8d5a4-154">Now that you have protected your VM, see hello following articles toolearn about VM management tasks, and how toorestore VMs.</span></span>

* [<span data-ttu-id="8d5a4-155">Мониторинг виртуальных машин и управление ими</span><span class="sxs-lookup"><span data-stu-id="8d5a4-155">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="8d5a4-156">Восстановление виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="8d5a4-156">Restore virtual machines</span></span>](backup-azure-arm-restore-vms.md)
