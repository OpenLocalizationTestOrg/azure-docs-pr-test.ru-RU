---
title: "aaaBack копирование резервного хранилища tooa классическом развертывании виртуальных машин Azure | Документы Microsoft"
description: "В этой статье приведены процедуры обнаружения, регистрации и резервного копирования виртуальных машин Azure."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "резервное копирование виртуальных машин; резервное копирование виртуальной машины; резервное копирование и аварийное восстановление; резервное копирование VM"
ms.assetid: c0ab5469-65fd-4af5-ae9b-f5d183f82ce8
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 048e32d9b2bd5bdd7a125225a71a6d805bb4fbd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-classic-portal"></a><span data-ttu-id="80290-104">Архивация виртуальных машин Azure (классический портал)</span><span class="sxs-lookup"><span data-stu-id="80290-104">Back up Azure virtual machines (classic portal)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="80290-105">Резервное копирование виртуальных машин tooRecovery служб хранилища</span><span class="sxs-lookup"><span data-stu-id="80290-105">Back up VMs tooRecovery Services vault</span></span>](backup-azure-arm-vms.md)
> * [<span data-ttu-id="80290-106">Резервное копирование виртуальных машин tooBackup хранилища</span><span class="sxs-lookup"><span data-stu-id="80290-106">Back up VMs tooBackup vault</span></span>](backup-azure-vms.md)
>
>

<span data-ttu-id="80290-107">В этой статье описаны процедуры hello резервное копирование хранилища архивации tooa классическом развертывании Azure виртуальной машины (VM).</span><span class="sxs-lookup"><span data-stu-id="80290-107">This article provides hello procedures for backing up a Classic-deployed Azure virtual machine (VM) tooa Backup vault.</span></span> <span data-ttu-id="80290-108">Существует несколько задач, tootake следит прежде можно выполнять резервное копирование виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="80290-108">There are a few tasks you need tootake care of before you can back up an Azure virtual machine.</span></span> <span data-ttu-id="80290-109">Если вы еще не сделали так, полные hello [необходимые компоненты](backup-azure-vms-prepare.md) tooprepare среды для резервного копирования виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="80290-109">If you haven't already done so, complete hello [prerequisites](backup-azure-vms-prepare.md) tooprepare your environment for backing up your VMs.</span></span>

<span data-ttu-id="80290-110">Дополнительные сведения см. в статьях hello на [планирование инфраструктуры резервного копирования виртуальной Машины в Azure](backup-azure-vms-introduction.md) и [виртуальных машин Azure](https://azure.microsoft.com/documentation/services/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="80290-110">For additional information, see hello articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span>

> [!NOTE]
> <span data-ttu-id="80290-111">В Azure предусмотрены две модели развертывания, позволяющие создавать ресурсы и работать с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="80290-111">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="80290-112">Хранилище архивации может защитить только виртуальные машины, которые были развернуты с использованием классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="80290-112">A Backup vault can only protect Classic-deployed VMs.</span></span> <span data-ttu-id="80290-113">С помощью хранилища архивации невозможно защитить виртуальные машины, развернутые с использованием модели Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="80290-113">You cannot protect Resource Manager-deployed VMs with a Backup vault.</span></span> <span data-ttu-id="80290-114">В разделе [резервное копирование виртуальных машин хранилище служб tooRecovery](backup-azure-arm-vms.md) сведения о работе со службами восстановления хранилищ.</span><span class="sxs-lookup"><span data-stu-id="80290-114">See [Back up VMs tooRecovery Services vault](backup-azure-arm-vms.md) for details on working with Recovery Services vaults.</span></span>
>
>

<span data-ttu-id="80290-115">Резервное копирование виртуальных машин Azure состоит из трех основных шагов.</span><span class="sxs-lookup"><span data-stu-id="80290-115">Backing up Azure virtual machines involves three key steps:</span></span>

![Три шага tooback копирование ВМ IaaS Azure](./media/backup-azure-vms/3-steps-for-backup.png)

> [!NOTE]
> <span data-ttu-id="80290-117">Резервное копирование виртуальных машин — локальный процесс.</span><span class="sxs-lookup"><span data-stu-id="80290-117">Backing up virtual machines is a local process.</span></span> <span data-ttu-id="80290-118">Не удается резервное копирование виртуальных машин в одной области tooa хранилище резервных копий в другом регионе.</span><span class="sxs-lookup"><span data-stu-id="80290-118">You cannot back up virtual machines in one region tooa backup vault in another region.</span></span> <span data-ttu-id="80290-119">Поэтому необходимо создать хранилище архивации в каждом регионе Azure, в котором есть виртуальные машины, которые будут архивироваться.</span><span class="sxs-lookup"><span data-stu-id="80290-119">So, you must create a backup vault in each Azure region, where there are VMs that will be backed up.</span></span>
>
> [!IMPORTANT]
> <span data-ttu-id="80290-120">Запуск марта 2017 г., можно использовать больше не hello классического портала toocreate резервное копирование хранилищ.</span><span class="sxs-lookup"><span data-stu-id="80290-120">Starting March 2017, you can no longer use hello classic portal toocreate Backup vaults.</span></span>
> <span data-ttu-id="80290-121">Теперь можно обновить вашими хранилищами служб tooRecovery хранилища резервной копии.</span><span class="sxs-lookup"><span data-stu-id="80290-121">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="80290-122">Дополнительные сведения см. в статье hello [обновление tooa хранилища резервной копии, в хранилище служб восстановления](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="80290-122">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="80290-123">Корпорация Майкрософт рекомендует tooupgrade вашей резервных хранилищ tooRecovery хранилищами служб.</span><span class="sxs-lookup"><span data-stu-id="80290-123">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="80290-124">После 15 октября 2017 г. нельзя использовать PowerShell toocreate резервное копирование хранилищ.</span><span class="sxs-lookup"><span data-stu-id="80290-124">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="80290-125">**К 1 ноября 2017 года**:</span><span class="sxs-lookup"><span data-stu-id="80290-125">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="80290-126">Все оставшиеся хранилища резервной копии будет автоматически обновленные tooRecovery хранилищами служб.</span><span class="sxs-lookup"><span data-stu-id="80290-126">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="80290-127">Вы не будет возможности tooaccess данные резервной копии hello классического портала.</span><span class="sxs-lookup"><span data-stu-id="80290-127">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="80290-128">Вместо этого используйте hello Azure портала tooaccess резервного копирования данных в хранилищах службы восстановления.</span><span class="sxs-lookup"><span data-stu-id="80290-128">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="step-1---discover-azure-virtual-machines"></a><span data-ttu-id="80290-129">Шаг 1. Обнаружение виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="80290-129">Step 1 - Discover Azure virtual machines</span></span>
<span data-ttu-id="80290-130">подписка добавлена toohello виртуальных машин (ВМ) определяются перед регистрацией tooensure запустить процесс обнаружения hello.</span><span class="sxs-lookup"><span data-stu-id="80290-130">tooensure any new virtual machines (VMs) added toohello subscription are identified before registering, run hello discovery process.</span></span> <span data-ttu-id="80290-131">Hello процесс запрашивает Azure hello список виртуальных машин в подписке hello, а также дополнительные сведения, такие как имя облачной службы hello и регион hello.</span><span class="sxs-lookup"><span data-stu-id="80290-131">hello process queries Azure for hello list of virtual machines in hello subscription, along with additional information like hello cloud service name and hello region.</span></span>

1. <span data-ttu-id="80290-132">Войдите в toohello [классический портал](http://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="80290-132">Sign in toohello [Classic portal](http://manage.windowsazure.com/)</span></span>
2. <span data-ttu-id="80290-133">В списке hello служб Azure, выберите **службы восстановления** tooopen hello список хранилищ архивации и Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="80290-133">In hello list of Azure services, click **Recovery Services** tooopen hello list of Backup and Site Recovery vaults.</span></span>
    <span data-ttu-id="80290-134">![Открытие списка хранилищ](./media/backup-azure-vms/choose-vault-list.png)</span><span class="sxs-lookup"><span data-stu-id="80290-134">![Open vault list](./media/backup-azure-vms/choose-vault-list.png)</span></span>
3. <span data-ttu-id="80290-135">В списке hello хранилищ архивации выберите tooback хранилище hello ВМ.</span><span class="sxs-lookup"><span data-stu-id="80290-135">In hello list of Backup vaults, select hello vault tooback up a VM.</span></span>

    <span data-ttu-id="80290-136">Если это новый портал hello хранилище открывает toohello **быстрый запуск** страницы.</span><span class="sxs-lookup"><span data-stu-id="80290-136">If this is a new vault hello portal opens toohello **Quick Start** page.</span></span>

    ![Открытие меню "Зарегистрированные элементы"](./media/backup-azure-vms/vault-quick-start.png)

    <span data-ttu-id="80290-138">Если ранее был настроен hello хранилища, toohello самые последние использовавшиеся меню открывается, hello портала.</span><span class="sxs-lookup"><span data-stu-id="80290-138">If hello vault has previously been configured, hello portal opens toohello most recently used menu.</span></span>
4. <span data-ttu-id="80290-139">Меню hello хранилища (вверху hello hello страницы), выберите пункт **зарегистрированные элементы**.</span><span class="sxs-lookup"><span data-stu-id="80290-139">From hello vault menu (at hello top of hello page), click **Registered Items**.</span></span>

    ![Открытие меню "Зарегистрированные элементы"](./media/backup-azure-vms/vault-menu.png)
5. <span data-ttu-id="80290-141">Из hello **тип** последовательно выберите пункты **виртуальной машине Azure**.</span><span class="sxs-lookup"><span data-stu-id="80290-141">From hello **Type** menu, select **Azure Virtual Machine**.</span></span>

    ![Выбор рабочей нагрузки](./media/backup-azure-vms/discovery-select-workload.png)
6. <span data-ttu-id="80290-143">Нажмите кнопку **DISCOVER** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="80290-143">Click **DISCOVER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="80290-144">![Кнопка обнаружения](./media/backup-azure-vms/discover-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="80290-144">![Discover button](./media/backup-azure-vms/discover-button-only.png)</span></span>

    <span data-ttu-id="80290-145">процесс обнаружения Hello помещаются hello виртуальных машин может потребоваться несколько минут.</span><span class="sxs-lookup"><span data-stu-id="80290-145">hello discovery process may take a few minutes while hello virtual machines are being tabulated.</span></span> <span data-ttu-id="80290-146">Нет уведомлений hello нижней части экрана приветствия, информирующее о том, что выполняется процесс hello.</span><span class="sxs-lookup"><span data-stu-id="80290-146">There is a notification at hello bottom of hello screen that lets you know that hello process is running.</span></span>

    ![Обнаружение виртуальных машин](./media/backup-azure-vms/discovering-vms.png)

    <span data-ttu-id="80290-148">Hello уведомления меняется после завершения процесса hello.</span><span class="sxs-lookup"><span data-stu-id="80290-148">hello notification changes when hello process is complete.</span></span> <span data-ttu-id="80290-149">Если процесс обнаружения hello не удалось найти виртуальные машины hello, сначала убедитесь, что существует hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="80290-149">If hello discovery process did not find hello virtual machines, first ensure hello VMs exist.</span></span> <span data-ttu-id="80290-150">Если виртуальные машины hello существует, убедитесь, hello виртуальные машины находятся в hello же регионе, что hello резервного хранилища.</span><span class="sxs-lookup"><span data-stu-id="80290-150">If hello VMs exist, ensure hello VMs are in hello same region as hello backup vault.</span></span> <span data-ttu-id="80290-151">Если виртуальные машины hello существует и в hello же регионе, убедитесь, что виртуальные машины hello еще не зарегистрированных tooa резервного хранилища.</span><span class="sxs-lookup"><span data-stu-id="80290-151">If hello VMs exist and are in hello same region, ensure hello VMs are not already registered tooa backup vault.</span></span> <span data-ttu-id="80290-152">Если виртуальная машина является назначенным tooa резервного хранилища не доступные toobe назначенный tooother резервными хранилищами.</span><span class="sxs-lookup"><span data-stu-id="80290-152">If a VM is assigned tooa backup vault it is not available toobe assigned tooother backup vaults.</span></span>

    ![Обнаружение завершено](./media/backup-azure-vms/discovery-complete.png)

    <span data-ttu-id="80290-154">После обнаружения новых элементов hello go tooStep 2 и зарегистрируйте виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="80290-154">Once you have discovered hello new items, go tooStep 2 and register your VMs.</span></span>

## <a name="step-2---register-azure-virtual-machines"></a><span data-ttu-id="80290-155">Шаг 2. Регистрация виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="80290-155">Step 2 - Register Azure virtual machines</span></span>
<span data-ttu-id="80290-156">Зарегистрировать tooassociate виртуальной машины Azure с помощью службы архивации Azure hello.</span><span class="sxs-lookup"><span data-stu-id="80290-156">You register an Azure virtual machine tooassociate it with hello Azure Backup service.</span></span> <span data-ttu-id="80290-157">Как правило, это разовая операция.</span><span class="sxs-lookup"><span data-stu-id="80290-157">This is typically a one-time activity.</span></span>

1. <span data-ttu-id="80290-158">Перейдите toohello резервного хранилища в группе **службы восстановления** в hello портал Azure и нажмите кнопку **зарегистрированные элементы**.</span><span class="sxs-lookup"><span data-stu-id="80290-158">Navigate toohello backup vault under **Recovery Services** in hello Azure portal, and then click **Registered Items**.</span></span>
2. <span data-ttu-id="80290-159">Выберите **виртуальной машине Azure** hello раскрывающегося меню.</span><span class="sxs-lookup"><span data-stu-id="80290-159">Select **Azure Virtual Machine** from hello drop-down menu.</span></span>

    ![Выбор рабочей нагрузки](./media/backup-azure-vms/discovery-select-workload.png)
3. <span data-ttu-id="80290-161">Нажмите кнопку **ЗАРЕГИСТРИРОВАТЬ** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="80290-161">Click **REGISTER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="80290-162">![Кнопка регистрации](./media/backup-azure-vms/register-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="80290-162">![Register button](./media/backup-azure-vms/register-button-only.png)</span></span>
4. <span data-ttu-id="80290-163">В hello **зарегистрировать элементы** контекстное меню, выберите hello виртуальных машин, которые должны tooregister.</span><span class="sxs-lookup"><span data-stu-id="80290-163">In hello **Register Items** shortcut menu, select hello virtual machines that you want tooregister.</span></span> <span data-ttu-id="80290-164">При наличии двух или нескольких виртуальных машин с hello таким же именем, используйте toodistinguish hello облачной службы, между ними.</span><span class="sxs-lookup"><span data-stu-id="80290-164">If there are two or more virtual machines with hello same name, use hello cloud service toodistinguish between them.</span></span>

   > [!TIP]
   > <span data-ttu-id="80290-165">В ходе одной процедуры можно зарегистрировать несколько виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="80290-165">Multiple virtual machines can be registered at one time.</span></span>
   >
   >

    <span data-ttu-id="80290-166">Для каждой выбранной виртуальной машины будет создано задание.</span><span class="sxs-lookup"><span data-stu-id="80290-166">A job is created for each virtual machine that you've selected.</span></span>
5. <span data-ttu-id="80290-167">Нажмите кнопку **просмотреть задание** в hello уведомления toogo toohello **заданий** страницы.</span><span class="sxs-lookup"><span data-stu-id="80290-167">Click **View Job** in hello notification toogo toohello **Jobs** page.</span></span>

    ![Задание регистрации](./media/backup-azure-vms/register-create-job.png)

    <span data-ttu-id="80290-169">Виртуальная машина Hello также отображается в список зарегистрированных элементов, с указанием состояния hello операции регистрации hello hello.</span><span class="sxs-lookup"><span data-stu-id="80290-169">hello virtual machine also appears in hello list of registered items, along with hello status of hello registration operation.</span></span>

    ![Состояние регистрации 1](./media/backup-azure-vms/register-status01.png)

    <span data-ttu-id="80290-171">По завершении операции hello hello состояние изменяется tooreflect hello *зарегистрированные* состояния.</span><span class="sxs-lookup"><span data-stu-id="80290-171">When hello operation completes, hello status changes tooreflect hello *registered* state.</span></span>

    ![Состояние регистрации 2](./media/backup-azure-vms/register-status02.png)

## <a name="step-3---protect-azure-virtual-machines"></a><span data-ttu-id="80290-173">Шаг 3. Защита виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="80290-173">Step 3 - Protect Azure virtual machines</span></span>
<span data-ttu-id="80290-174">Теперь можно настроить политику резервного копирования и хранения для виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="80290-174">Now you can set up a backup and retention policy for hello virtual machine.</span></span> <span data-ttu-id="80290-175">Одним действием можно защитить несколько виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="80290-175">Multiple virtual machines can be protected by using a single protect action.</span></span>

<span data-ttu-id="80290-176">Созданные после май 2015 г. входящие в состав хранилищах службы архивации Azure политику по умолчанию встроены в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="80290-176">Azure Backup vaults created after May 2015 come with a default policy built into hello vault.</span></span> <span data-ttu-id="80290-177">Эта политика определяет не только стандартный срок хранения (30 дней), но и расписание ежедневного резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="80290-177">This default policy comes with a default retention of 30 days and a once-daily backup schedule.</span></span>

1. <span data-ttu-id="80290-178">Перейдите toohello резервного хранилища в группе **службы восстановления** в hello портал Azure и нажмите кнопку **зарегистрированные элементы**.</span><span class="sxs-lookup"><span data-stu-id="80290-178">Navigate toohello backup vault under **Recovery Services** in hello Azure portal, and then click **Registered Items**.</span></span>
2. <span data-ttu-id="80290-179">Выберите **виртуальной машине Azure** hello раскрывающегося меню.</span><span class="sxs-lookup"><span data-stu-id="80290-179">Select **Azure Virtual Machine** from hello drop-down menu.</span></span>

    ![Выберите рабочую нагрузку на портале](./media/backup-azure-vms/select-workload.png)
3. <span data-ttu-id="80290-181">Нажмите кнопку **ЗАЩИТИТЬ** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="80290-181">Click **PROTECT** at hello bottom of hello page.</span></span>

    <span data-ttu-id="80290-182">Hello **мастер защиты элементов** отображается.</span><span class="sxs-lookup"><span data-stu-id="80290-182">hello **Protect Items wizard** appears.</span></span> <span data-ttu-id="80290-183">Мастер Hello только список виртуальных машин, которые зарегистрированы и не защищен.</span><span class="sxs-lookup"><span data-stu-id="80290-183">hello wizard only lists virtual machines that are registered and not protected.</span></span> <span data-ttu-id="80290-184">Выберите hello виртуальных машин, которые должны tooprotect.</span><span class="sxs-lookup"><span data-stu-id="80290-184">Select hello virtual machines that you want tooprotect.</span></span>

    <span data-ttu-id="80290-185">При наличии двух или нескольких виртуальных машин с hello таким же именем, используйте toodistinguish hello облачной службы, между виртуальными машинами hello.</span><span class="sxs-lookup"><span data-stu-id="80290-185">If there are two or more virtual machines with hello same name, use hello cloud service toodistinguish between hello virtual machines.</span></span>

   > [!TIP]
   > <span data-ttu-id="80290-186">Можно защитить несколько виртуальных машин одновременно.</span><span class="sxs-lookup"><span data-stu-id="80290-186">You can protect multiple virtual machines at one time.</span></span>
   >
   >

    ![Настройка защиты нужного уровня](./media/backup-azure-vms/protect-at-scale.png)

4. <span data-ttu-id="80290-188">Выберите **расписание резервного копирования** tooback копирование hello виртуальных машин, которые вы выбрали.</span><span class="sxs-lookup"><span data-stu-id="80290-188">Choose a **backup schedule** tooback up hello virtual machines that you've selected.</span></span> <span data-ttu-id="80290-189">Выберите политику из существующего набора или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="80290-189">You can pick from an existing set of policies or define a new one.</span></span>

    <span data-ttu-id="80290-190">У каждой политики резервного копирования может быть несколько связанных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="80290-190">Each backup policy can have multiple virtual machines associated with it.</span></span> <span data-ttu-id="80290-191">Однако hello виртуальной машины может быть связан только с одной политики в любой момент времени.</span><span class="sxs-lookup"><span data-stu-id="80290-191">However, hello virtual machine can only be associated with one policy at any given point in time.</span></span>

    ![Защита с помощью новой политики](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > <span data-ttu-id="80290-193">Политики резервного копирования включает в себя схему хранения для резервных копий, запланированных hello.</span><span class="sxs-lookup"><span data-stu-id="80290-193">A backup policy includes a retention scheme for hello scheduled backups.</span></span> <span data-ttu-id="80290-194">Если выбрать существующую политику резервного копирования, невозможно изменить параметры хранения hello в следующем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="80290-194">If you select an existing backup policy, you cannot modify hello retention options in hello next step.</span></span>
   >
   >

5. <span data-ttu-id="80290-195">Выберите **диапазон хранения** tooassociate с резервными копиями hello.</span><span class="sxs-lookup"><span data-stu-id="80290-195">Choose a **retention range** tooassociate with hello backups.</span></span>

    ![Защита с помощью гибких возможностей хранения](./media/backup-azure-vms/policy-retention.png)

    <span data-ttu-id="80290-197">Политика хранения указывает hello интервал времени для хранения резервной копии.</span><span class="sxs-lookup"><span data-stu-id="80290-197">Retention policy specifies hello length of time for storing a backup.</span></span> <span data-ttu-id="80290-198">Можно указать при hello резервная копия создается на основе политик крепления.</span><span class="sxs-lookup"><span data-stu-id="80290-198">You can specify different retention policies based on when hello backup is taken.</span></span> <span data-ttu-id="80290-199">Например, точка ежедневной архивации (которая служит точкой оперативного восстановления) может храниться в течение 90 дней.</span><span class="sxs-lookup"><span data-stu-id="80290-199">For example, a backup point taken daily (which serves as an operational recovery point) might be preserved for 90 days.</span></span> <span data-ttu-id="80290-200">В отличие от этого точки резервного копирования, которое выполняется в конце каждого квартала (для целей аудита) в hello может понадобиться toobe сохраняются для нескольких месяцев или лет.</span><span class="sxs-lookup"><span data-stu-id="80290-200">In comparison, a backup point taken at hello end of each quarter (for audit purposes) may need toobe preserved for many months or years.</span></span>

    ![Резервное копирование виртуальной машины с точкой восстановления](./media/backup-azure-vms/long-term-retention.png)

    <span data-ttu-id="80290-202">Описание политик, приведенных на изображении выше:</span><span class="sxs-lookup"><span data-stu-id="80290-202">In this example image:</span></span>

   * <span data-ttu-id="80290-203">**Ежедневная политика хранения**. Резервные копии, создаваемые ежедневно, хранятся в течение 30 дней.</span><span class="sxs-lookup"><span data-stu-id="80290-203">**Daily retention policy**: Backups taken daily are stored for 30 days.</span></span>
   * <span data-ttu-id="80290-204">**Еженедельная политика хранения**. Резервные копии, создаваемые каждое воскресенье, хранятся 104 недели.</span><span class="sxs-lookup"><span data-stu-id="80290-204">**Weekly retention policy**: Backups taken every week on Sunday are preserved for 104 weeks.</span></span>
   * <span data-ttu-id="80290-205">**Ежемесячные политики хранения**: 120 месяцев сохраняются резервные копии hello последнее воскресенье каждого месяца.</span><span class="sxs-lookup"><span data-stu-id="80290-205">**Monthly retention policy**: Backups taken on hello last Sunday of each month are preserved for 120 months.</span></span>
   * <span data-ttu-id="80290-206">**Ежегодно политики хранения**: резервные копии hello первое воскресенье каждого января, сохраняются в течение 99 лет.</span><span class="sxs-lookup"><span data-stu-id="80290-206">**Yearly retention policy**: Backups taken on hello first Sunday of every January are preserved for 99 years.</span></span>

     <span data-ttu-id="80290-207">Задание создается политика защиты tooconfigure hello и связать политику toothat hello виртуальные машины для каждой виртуальной машины с вами.</span><span class="sxs-lookup"><span data-stu-id="80290-207">A job is created tooconfigure hello protection policy and associate hello virtual machines toothat policy for each virtual machine that you've selected.</span></span>
6. <span data-ttu-id="80290-208">Список hello tooview **Настройка защиты** заданий hello хранилищ меню, щелкните **заданий** и выберите **Настройка защиты** из hello **операции**  фильтра.</span><span class="sxs-lookup"><span data-stu-id="80290-208">tooview hello list of **Configure Protection** jobs, from hello vaults menu, click **Jobs** and select **Configure Protection** from hello **Operation** filter.</span></span>

    ![Настройка задания защиты](./media/backup-azure-vms/protect-configureprotection.png)

## <a name="initial-backup"></a><span data-ttu-id="80290-210">Начальное резервное копирование</span><span class="sxs-lookup"><span data-stu-id="80290-210">Initial backup</span></span>
<span data-ttu-id="80290-211">После hello виртуальная машина защищена с политикой, оно отображается в списке hello **защищенные элементы** вкладка со статусом hello *защищенные - (Ожидание начальной резервной копии)*.</span><span class="sxs-lookup"><span data-stu-id="80290-211">Once hello virtual machine is protected with a policy, it shows up under hello **Protected Items** tab with hello status of *Protected - (pending initial backup)*.</span></span> <span data-ttu-id="80290-212">По умолчанию hello первого запланированного резервного копирования — hello *начальной резервной копии*.</span><span class="sxs-lookup"><span data-stu-id="80290-212">By default, hello first scheduled backup is hello *initial backup*.</span></span>

<span data-ttu-id="80290-213">tootrigger hello начальную резервную копию немедленно после настройки защиты:</span><span class="sxs-lookup"><span data-stu-id="80290-213">tootrigger hello initial backup immediately after configuring protection:</span></span>

1. <span data-ttu-id="80290-214">Внизу hello hello **защищенные элементы** щелкните **создать резервную копию**.</span><span class="sxs-lookup"><span data-stu-id="80290-214">At hello bottom of hello **Protected Items** page, click **Backup Now**.</span></span>

    <span data-ttu-id="80290-215">Hello службы резервного копирования Azure создает задание резервного копирования для hello начальной резервной копии.</span><span class="sxs-lookup"><span data-stu-id="80290-215">hello Azure Backup service creates a backup job for hello initial backup operation.</span></span>
2. <span data-ttu-id="80290-216">Нажмите кнопку hello **заданий** вкладку tooview hello список заданий.</span><span class="sxs-lookup"><span data-stu-id="80290-216">Click hello **Jobs** tab tooview hello list of jobs.</span></span>

    ![Выполняется резервное копирование](./media/backup-azure-vms/protect-inprogress.png)

> [!NOTE]
> <span data-ttu-id="80290-218">Во время операции резервного копирования hello hello службы резервного копирования Azure выдает команды toohello расширение резервного копирования в каждой виртуальной машины tooflush все записи задания и занять согласованный моментальный снимок.</span><span class="sxs-lookup"><span data-stu-id="80290-218">During hello backup operation, hello Azure Backup service issues a command toohello backup extension in each virtual machine tooflush all write jobs and take a consistent snapshot.</span></span>
>
>

<span data-ttu-id="80290-219">После завершения начальной резервной копии hello hello состояние виртуальной машины hello в hello **защищенные элементы** вкладка — *Protected*.</span><span class="sxs-lookup"><span data-stu-id="80290-219">When hello initial backup finishes, hello status of hello virtual machine in hello **Protected Items** tab is *Protected*.</span></span>

![Резервное копирование виртуальной машины с точкой восстановления](./media/backup-azure-vms/protect-backedupvm.png)

## <a name="viewing-backup-status-and-details"></a><span data-ttu-id="80290-221">Просмотр состояния резервного копирования и подробностей</span><span class="sxs-lookup"><span data-stu-id="80290-221">Viewing backup status and details</span></span>
<span data-ttu-id="80290-222">После защищен, количество виртуальных машин hello также увеличивается в hello **мониторинга** страница сводки.</span><span class="sxs-lookup"><span data-stu-id="80290-222">Once protected, hello virtual machine count also increases in hello **Dashboard** page summary.</span></span> <span data-ttu-id="80290-223">Hello **мониторинга** hello количество заданий из hello последние 24 часа, которые были также показывается *успешно*, имеют *сбой*и являются *выполняется*.</span><span class="sxs-lookup"><span data-stu-id="80290-223">hello **Dashboard** page also shows hello number of jobs from hello last 24 hours that were *successful*, have *failed*, and are *in progress*.</span></span> <span data-ttu-id="80290-224">На hello **заданий** используйте hello **состояние**, **операции**, или **из** и **для** toofilter меню задания Hello.</span><span class="sxs-lookup"><span data-stu-id="80290-224">On hello **Jobs** page, use hello **Status**, **Operation**, or **From** and **To** menus toofilter hello jobs.</span></span>

![Состояние резервного копирования на странице панели мониторинга](./media/backup-azure-vms/dashboard-protectedvms.png)

<span data-ttu-id="80290-226">Значения в панель мониторинга hello обновляются каждые 24 часа.</span><span class="sxs-lookup"><span data-stu-id="80290-226">Values in hello dashboard are refreshed once every 24 hours.</span></span>

## <a name="troubleshooting-errors"></a><span data-ttu-id="80290-227">Устранение ошибок</span><span class="sxs-lookup"><span data-stu-id="80290-227">Troubleshooting errors</span></span>
<span data-ttu-id="80290-228">Если возникнут проблемы во время резервного копирования виртуальной машины посмотрите hello [статьи по устранению неполадок виртуальной Машины](backup-azure-vms-troubleshoot.md) для справки.</span><span class="sxs-lookup"><span data-stu-id="80290-228">If you run into issues while backing up your virtual machine, look at hello [VM     troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="80290-229">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="80290-229">Next steps</span></span>
* [<span data-ttu-id="80290-230">Мониторинг виртуальных машин и управление ими</span><span class="sxs-lookup"><span data-stu-id="80290-230">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="80290-231">Восстановление виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="80290-231">Restore virtual machines</span></span>](backup-azure-restore-vms.md)
