---
title: "Первое знакомство. Резервное копирование виртуальных машин Azure в хранилище службы архивации | Документация Майкрософт"
description: "С помощью классического портала tooback hello копирование виртуальных машин Azure tooa резервное хранилище. В этом учебнике описано всех этапов, включая создание hello резервное хранилище, регистрация hello виртуальные машины, создание политики резервного копирования и запуск задания резервного копирования начальной hello."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 722820dc-b65f-425c-a9e5-c1946e896a87
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/2/2017
ms.author: markgal;
ms.openlocfilehash: 77700e69eab9faccbc7ef923e1eb4e1f97be75d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="first-look-backing-up-azure-virtual-machines"></a><span data-ttu-id="841a0-104">Первое знакомство: резервное копирование виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="841a0-104">First look: Backing up Azure virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="841a0-105">Защита виртуальных машин в хранилище служб восстановления</span><span class="sxs-lookup"><span data-stu-id="841a0-105">Protect VMs with a recovery services vault</span></span>](backup-azure-vms-first-look-arm.md)
> * [<span data-ttu-id="841a0-106">Защита виртуальных машин Azure в хранилище службы архивации</span><span class="sxs-lookup"><span data-stu-id="841a0-106">Protect Azure VMs with a backup vault</span></span>](backup-azure-vms-first-look.md)
>
>

<span data-ttu-id="841a0-107">Этот учебник руководит hello резервного копирования виртуальной машины (VM) Azure tooa резервное хранилище в Azure.</span><span class="sxs-lookup"><span data-stu-id="841a0-107">This tutorial takes you through hello steps for backing up an Azure virtual machine (VM) tooa backup vault in Azure.</span></span> <span data-ttu-id="841a0-108">В этой статье описываются hello классической модели или модели развертывания Service Manager, для резервного копирования виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="841a0-108">This article describes hello classic model or Service Manager deployment model, for backing up VMs.</span></span> <span data-ttu-id="841a0-109">Hello следующие шаги применяются только tooBackup хранилищ, созданные в классическом портале hello.</span><span class="sxs-lookup"><span data-stu-id="841a0-109">hello following steps apply only tooBackup vaults created in hello classic portal.</span></span> <span data-ttu-id="841a0-110">Майкрософт рекомендует использовать модель hello диспетчера ресурсов для новых развертываний.</span><span class="sxs-lookup"><span data-stu-id="841a0-110">Microsoft recommends using hello Resource Manager model for new deployments.</span></span>

<span data-ttu-id="841a0-111">Если вы заинтересованы в резервном хранилище служб восстановления tooa виртуальной Машины, к которой относится tooa группы ресурсов, см. раздел [первый взгляд: Защита виртуальных машин с хранилище служб восстановления](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="841a0-111">If you are interested in backing up a VM tooa Recovery Services vault that belongs tooa Resource Group, see [First look: Protect VMs with a recovery services vault](backup-azure-vms-first-look-arm.md).</span></span>

<span data-ttu-id="841a0-112">toosuccessfully воспользуйтесь следующих hello учебник, должен существовать следующие предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="841a0-112">toosuccessfully complete hello following tutorial, these prerequisites must exist:</span></span>

* <span data-ttu-id="841a0-113">создать виртуальную машину в подписке Azure;</span><span class="sxs-lookup"><span data-stu-id="841a0-113">You have created a VM in your Azure subscription.</span></span>
* <span data-ttu-id="841a0-114">Hello виртуальной Машины имеет подключения к tooAzure общих IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="841a0-114">hello VM has connectivity tooAzure public IP addresses.</span></span> <span data-ttu-id="841a0-115">Дополнительные сведения см. в разделе [Сетевое подключение](backup-azure-vms-prepare.md#network-connectivity).</span><span class="sxs-lookup"><span data-stu-id="841a0-115">For additional information, see [Network connectivity](backup-azure-vms-prepare.md#network-connectivity).</span></span>


> [!NOTE]
> <span data-ttu-id="841a0-116">В Azure предусмотрены две модели развертывания, позволяющие создавать ресурсы и работать с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="841a0-116">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="841a0-117">Этот учебник предназначен для использования с виртуальных машин, созданных в классическом портале hello.</span><span class="sxs-lookup"><span data-stu-id="841a0-117">This tutorial is for use with virtual machines created in hello classic portal.</span></span>
>
>

## <a name="create-a-backup-vault"></a><span data-ttu-id="841a0-118">создать хранилище архивации;</span><span class="sxs-lookup"><span data-stu-id="841a0-118">Create a backup vault</span></span>
<span data-ttu-id="841a0-119">Резервное хранилище — это сущность, которой хранятся все резервные копии hello и точек восстановления, которые были созданы со временем.</span><span class="sxs-lookup"><span data-stu-id="841a0-119">A backup vault is an entity that stores all hello backups and recovery points that have been created over time.</span></span> <span data-ttu-id="841a0-120">резервное хранилище Hello также содержит политики резервного копирования hello, примененные toohello виртуальных машин, резервная копия.</span><span class="sxs-lookup"><span data-stu-id="841a0-120">hello backup vault also contains hello backup policies that are applied toohello virtual machines being backed up.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="841a0-121">Запуск марта 2017 г., можно использовать больше не hello классического портала toocreate резервное копирование хранилищ.</span><span class="sxs-lookup"><span data-stu-id="841a0-121">Starting March 2017, you can no longer use hello classic portal toocreate Backup vaults.</span></span>
> <span data-ttu-id="841a0-122">Вы можете обновить вашими хранилищами служб tooRecovery хранилища резервной копии.</span><span class="sxs-lookup"><span data-stu-id="841a0-122">You can upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="841a0-123">Дополнительные сведения см. в статье hello [обновление tooa хранилища резервной копии, в хранилище служб восстановления](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="841a0-123">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="841a0-124">Корпорация Майкрософт рекомендует tooupgrade вашей резервных хранилищ tooRecovery хранилищами служб.</span><span class="sxs-lookup"><span data-stu-id="841a0-124">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="841a0-125">После 15 октября 2017 г. нельзя использовать PowerShell toocreate резервное копирование хранилищ.</span><span class="sxs-lookup"><span data-stu-id="841a0-125">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="841a0-126">**К 1 ноября 2017 года**:</span><span class="sxs-lookup"><span data-stu-id="841a0-126">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="841a0-127">Все оставшиеся хранилища резервной копии будет автоматически обновленные tooRecovery хранилищами служб.</span><span class="sxs-lookup"><span data-stu-id="841a0-127">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="841a0-128">Вы не будет возможности tooaccess данные резервной копии hello классического портала.</span><span class="sxs-lookup"><span data-stu-id="841a0-128">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="841a0-129">Вместо этого используйте hello Azure портала tooaccess резервного копирования данных в хранилищах службы восстановления.</span><span class="sxs-lookup"><span data-stu-id="841a0-129">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="discover-and-register-azure-virtual-machines"></a><span data-ttu-id="841a0-130">Обнаружение и регистрация виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="841a0-130">Discover and Register Azure virtual machines</span></span>
<span data-ttu-id="841a0-131">Перед регистрацией hello виртуальной Машины с хранилищем, запустите tooidentify процесс обнаружения hello новые виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="841a0-131">Before registering hello VM with a vault, run hello discovery process tooidentify any new VMs.</span></span> <span data-ttu-id="841a0-132">Возвращает список виртуальных машин в подписке hello, а также дополнительные сведения, такие как имя облачной службы hello и регион hello.</span><span class="sxs-lookup"><span data-stu-id="841a0-132">This returns a list of virtual machines in hello subscription, along with additional information like hello cloud service name and hello region.</span></span>

1. <span data-ttu-id="841a0-133">Войдите в toohello [Azure классического портала](http://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="841a0-133">Sign in toohello [Azure Classic portal](http://manage.windowsazure.com/)</span></span>
2. <span data-ttu-id="841a0-134">В hello классический портал Azure, щелкните **службы восстановления** tooopen hello списка хранилищ служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="841a0-134">In hello Azure classic portal, click **Recovery Services** tooopen hello list of Recovery Services vaults.</span></span>
    <span data-ttu-id="841a0-135">![Выбор рабочей нагрузки](./media/backup-azure-vms-first-look/recovery-services-icon.png)</span><span class="sxs-lookup"><span data-stu-id="841a0-135">![Select workload](./media/backup-azure-vms-first-look/recovery-services-icon.png)</span></span>
3. <span data-ttu-id="841a0-136">Выберите из списка hello хранилищ tooback хранилище hello ВМ.</span><span class="sxs-lookup"><span data-stu-id="841a0-136">From hello list of vaults, select hello vault tooback up a VM.</span></span>

    <span data-ttu-id="841a0-137">При выборе ваше хранилище, он открывается в hello **быстрый запуск** страницы</span><span class="sxs-lookup"><span data-stu-id="841a0-137">When you select your vault, it opens in hello **Quick Start** page</span></span>
4. <span data-ttu-id="841a0-138">Меню hello хранилища, нажмите кнопку **зарегистрированные элементы**.</span><span class="sxs-lookup"><span data-stu-id="841a0-138">From hello vault menu, click **Registered Items**.</span></span>

    ![Выбор рабочей нагрузки](./media/backup-azure-vms-first-look/configure-registered-items.png)
5. <span data-ttu-id="841a0-140">Из hello **тип** последовательно выберите пункты **виртуальной машине Azure**.</span><span class="sxs-lookup"><span data-stu-id="841a0-140">From hello **Type** menu, select **Azure Virtual Machine**.</span></span>

    ![Выбор рабочей нагрузки](./media/backup-azure-vms/discovery-select-workload.png)
6. <span data-ttu-id="841a0-142">Нажмите кнопку **DISCOVER** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="841a0-142">Click **DISCOVER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="841a0-143">![Кнопка обнаружения](./media/backup-azure-vms/discover-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="841a0-143">![Discover button](./media/backup-azure-vms/discover-button-only.png)</span></span>

    <span data-ttu-id="841a0-144">процесс обнаружения Hello помещаются hello виртуальных машин может потребоваться несколько минут.</span><span class="sxs-lookup"><span data-stu-id="841a0-144">hello discovery process may take a few minutes while hello virtual machines are being tabulated.</span></span> <span data-ttu-id="841a0-145">Нет уведомлений hello нижней части экрана приветствия, информирующее о том, что выполняется процесс hello.</span><span class="sxs-lookup"><span data-stu-id="841a0-145">There is a notification at hello bottom of hello screen that lets you know that hello process is running.</span></span>

    ![Обнаружение виртуальных машин](./media/backup-azure-vms/discovering-vms.png)

    <span data-ttu-id="841a0-147">Hello уведомления меняется после завершения процесса hello.</span><span class="sxs-lookup"><span data-stu-id="841a0-147">hello notification changes when hello process is complete.</span></span>

    ![Обнаружение завершено](./media/backup-azure-vms-first-look/discovery-complete.png)
7. <span data-ttu-id="841a0-149">Нажмите кнопку **ЗАРЕГИСТРИРОВАТЬ** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="841a0-149">Click **REGISTER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="841a0-150">![Кнопка регистрации](./media/backup-azure-vms-first-look/register-icon.png)</span><span class="sxs-lookup"><span data-stu-id="841a0-150">![Register button](./media/backup-azure-vms-first-look/register-icon.png)</span></span>
8. <span data-ttu-id="841a0-151">В hello **зарегистрировать элементы** контекстное меню, выберите hello виртуальных машин, которые должны tooregister.</span><span class="sxs-lookup"><span data-stu-id="841a0-151">In hello **Register Items** shortcut menu, select hello virtual machines that you want tooregister.</span></span>

   > [!TIP]
   > <span data-ttu-id="841a0-152">В ходе одной процедуры можно зарегистрировать несколько виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="841a0-152">Multiple virtual machines can be registered at one time.</span></span>
   >
   >

    <span data-ttu-id="841a0-153">Для каждой выбранной виртуальной машины будет создано задание.</span><span class="sxs-lookup"><span data-stu-id="841a0-153">A job is created for each virtual machine that you've selected.</span></span>
9. <span data-ttu-id="841a0-154">Нажмите кнопку **просмотреть задание** в hello уведомления toogo toohello **заданий** страницы.</span><span class="sxs-lookup"><span data-stu-id="841a0-154">Click **View Job** in hello notification toogo toohello **Jobs** page.</span></span>

    ![Задание регистрации](./media/backup-azure-vms/register-create-job.png)

    <span data-ttu-id="841a0-156">Виртуальная машина Hello также отображается в список зарегистрированных элементов, с указанием состояния hello операции регистрации hello hello.</span><span class="sxs-lookup"><span data-stu-id="841a0-156">hello virtual machine also appears in hello list of registered items, along with hello status of hello registration operation.</span></span>

    ![Состояние регистрации 1](./media/backup-azure-vms/register-status01.png)

    <span data-ttu-id="841a0-158">По завершении операции hello hello состояние изменяется tooreflect hello *зарегистрированные* состояния.</span><span class="sxs-lookup"><span data-stu-id="841a0-158">When hello operation completes, hello status changes tooreflect hello *registered* state.</span></span>

    ![Состояние регистрации 2](./media/backup-azure-vms/register-status02.png)

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a><span data-ttu-id="841a0-160">Установите hello агент виртуальной Машины на виртуальной машине hello</span><span class="sxs-lookup"><span data-stu-id="841a0-160">Install hello VM Agent on hello virtual machine</span></span>
<span data-ttu-id="841a0-161">Hello агента ВМ Azure должны устанавливаться на hello виртуальной машины Azure для расширения toowork hello резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="841a0-161">hello Azure VM Agent must be installed on hello Azure virtual machine for hello Backup extension toowork.</span></span> <span data-ttu-id="841a0-162">Если ВМ был создан из коллекции Azure hello, hello агент виртуальной Машины уже существует на hello виртуальной Машины; Вы можете пропустить слишком[Защита виртуальных машин](backup-azure-vms-first-look.md#create-the-backup-policy).</span><span class="sxs-lookup"><span data-stu-id="841a0-162">If your VM was created from hello Azure gallery, hello VM Agent is already present on hello VM; you can skip too[protecting your VMs](backup-azure-vms-first-look.md#create-the-backup-policy).</span></span>

<span data-ttu-id="841a0-163">Если ВМ, перенесенные из центра обработки данных в локальной, hello виртуальной Машины, возможно, не имеет hello установлен агент виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="841a0-163">If your VM migrated from an on-premises datacenter, hello VM probably does not have hello VM Agent installed.</span></span> <span data-ttu-id="841a0-164">Hello агент виртуальной Машины необходимо установить на виртуальной машине hello перед продолжением tooprotect hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="841a0-164">You must install hello VM Agent on hello virtual machine before proceeding tooprotect hello VM.</span></span> <span data-ttu-id="841a0-165">Подробные инструкции по установке hello агент виртуальной Машины, см. в разделе hello [статьи агент виртуальной Машины hello резервного копирования виртуальных машин](backup-azure-vms-prepare.md#vm-agent).</span><span class="sxs-lookup"><span data-stu-id="841a0-165">For detailed steps on installing hello VM Agent, see hello [VM Agent section of hello Backup VMs article](backup-azure-vms-prepare.md#vm-agent).</span></span>

## <a name="create-hello-backup-policy"></a><span data-ttu-id="841a0-166">Создание политики резервного копирования hello</span><span class="sxs-lookup"><span data-stu-id="841a0-166">Create hello backup policy</span></span>
<span data-ttu-id="841a0-167">Прежде чем запустить задание резервного копирования начальной hello, настройте расписание для hello, когда резервного копирования делает моментальные снимки.</span><span class="sxs-lookup"><span data-stu-id="841a0-167">Before you trigger hello initial backup job, set hello schedule when backup snapshots are taken.</span></span> <span data-ttu-id="841a0-168">Hello планирование берутся резервных копий моментальных снимков и hello продолжительность времени, в таких моментальных снимках, сохраняются, — hello политику резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="841a0-168">hello schedule when backup snapshots are taken, and hello length of time those snapshots are retained, is hello backup policy.</span></span> <span data-ttu-id="841a0-169">Hello хранения информация основана на Деда отец ов схемы ротации резервных копий.</span><span class="sxs-lookup"><span data-stu-id="841a0-169">hello retention information is based on Grandfather-father-son backup rotation scheme.</span></span>

1. <span data-ttu-id="841a0-170">Перейдите toohello резервного хранилища в группе **службы восстановления** в hello Azure классическом портале и нажмите кнопку **зарегистрированные элементы**.</span><span class="sxs-lookup"><span data-stu-id="841a0-170">Navigate toohello backup vault under **Recovery Services** in hello Azure Classic portal, and  click **Registered Items**.</span></span>
2. <span data-ttu-id="841a0-171">Выберите **виртуальной машине Azure** hello раскрывающегося меню.</span><span class="sxs-lookup"><span data-stu-id="841a0-171">Select **Azure Virtual Machine** from hello drop-down menu.</span></span>

    ![Выберите рабочую нагрузку на портале](./media/backup-azure-vms/select-workload.png)
3. <span data-ttu-id="841a0-173">Нажмите кнопку **ЗАЩИТИТЬ** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="841a0-173">Click **PROTECT** at hello bottom of hello page.</span></span>
    <span data-ttu-id="841a0-174">![Элемент "Защитить"](./media/backup-azure-vms-first-look/protect-icon.png)</span><span class="sxs-lookup"><span data-stu-id="841a0-174">![Click Protect](./media/backup-azure-vms-first-look/protect-icon.png)</span></span>

    <span data-ttu-id="841a0-175">Hello **мастер защиты элементов** отображается и перечислены *только* виртуальных машин, которые зарегистрированы и не защищен.</span><span class="sxs-lookup"><span data-stu-id="841a0-175">hello **Protect Items wizard** appears and lists *only* virtual machines that are registered and not protected.</span></span>

    ![Настройка защиты нужного уровня](./media/backup-azure-vms/protect-at-scale.png)
4. <span data-ttu-id="841a0-177">Выберите hello виртуальных машин, которые должны tooprotect.</span><span class="sxs-lookup"><span data-stu-id="841a0-177">Select hello virtual machines that you want tooprotect.</span></span>

    <span data-ttu-id="841a0-178">При наличии двух или нескольких виртуальных машин с hello одинаковые имена, используйте hello toodistinguish облачной службы, между виртуальными машинами hello.</span><span class="sxs-lookup"><span data-stu-id="841a0-178">If there are two or more virtual machines with hello same name, use hello Cloud Service toodistinguish between hello virtual machines.</span></span>
5. <span data-ttu-id="841a0-179">На hello **настройки защиты** меню, выберите существующую политику или создайте новый tooprotect политики hello виртуальных машин, которые определены.</span><span class="sxs-lookup"><span data-stu-id="841a0-179">On hello **Configure protection** menu select an existing policy or create a new policy tooprotect hello virtual machines that you identified.</span></span>

    <span data-ttu-id="841a0-180">Новые хранилища резервной копии имеет политику по умолчанию, связанный с хранилищем hello.</span><span class="sxs-lookup"><span data-stu-id="841a0-180">New Backup vaults have a default policy associated with hello vault.</span></span> <span data-ttu-id="841a0-181">Эта политика имеет моментального снимка каждый вечер каждый день и ежедневно hello моментальных снимков хранятся в течение 30 дней.</span><span class="sxs-lookup"><span data-stu-id="841a0-181">This policy takes a daily snapshot each evening, and hello daily snapshot is retained for 30 days.</span></span> <span data-ttu-id="841a0-182">У каждой политики резервного копирования может быть несколько связанных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="841a0-182">Each backup policy can have multiple virtual machines associated with it.</span></span> <span data-ttu-id="841a0-183">Однако hello виртуальной машины может быть связан только с одной политики одновременно.</span><span class="sxs-lookup"><span data-stu-id="841a0-183">However, hello virtual machine can only be associated with one policy at a time.</span></span>

    ![Защита с помощью новой политики](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > <span data-ttu-id="841a0-185">Политики резервного копирования включает в себя схему хранения для резервных копий, запланированных hello.</span><span class="sxs-lookup"><span data-stu-id="841a0-185">A backup policy includes a retention scheme for hello scheduled backups.</span></span> <span data-ttu-id="841a0-186">Если выбрать существующую политику резервного копирования, будет параметры хранения не удается toomodify hello в следующем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="841a0-186">If you select an existing backup policy, you will be unable toomodify hello retention options in hello next step.</span></span>
   >
   >
6. <span data-ttu-id="841a0-187">На **диапазон хранения** определить hello ежедневно, еженедельно, ежемесячно и ежегодно область для резервного копирования точках hello.</span><span class="sxs-lookup"><span data-stu-id="841a0-187">On **Retention Range** define hello daily, weekly, monthly, and yearly scope for hello specific backup points.</span></span>

    ![Резервное копирование виртуальной машины с точкой восстановления](./media/backup-azure-vms/long-term-retention.png)

    <span data-ttu-id="841a0-189">Политика хранения указывает hello интервал времени для хранения резервной копии.</span><span class="sxs-lookup"><span data-stu-id="841a0-189">Retention policy specifies hello length of time for storing a backup.</span></span> <span data-ttu-id="841a0-190">Можно указать при hello резервная копия создается на основе политик крепления.</span><span class="sxs-lookup"><span data-stu-id="841a0-190">You can specify different retention policies based on when hello backup is taken.</span></span>
7. <span data-ttu-id="841a0-191">Нажмите кнопку **заданий** список hello tooview **Настройка защиты** заданий.</span><span class="sxs-lookup"><span data-stu-id="841a0-191">Click **Jobs** tooview hello list of **Configure Protection** jobs.</span></span>

    ![Настройка задания защиты](./media/backup-azure-vms/protect-configureprotection.png)

    <span data-ttu-id="841a0-193">Теперь, когда установил политику hello, перейдите следующему шагу toohello и запустите hello начальной резервной копии.</span><span class="sxs-lookup"><span data-stu-id="841a0-193">Now that you've established hello policy, go toohello next step and run hello initial backup.</span></span>

## <a name="initial-backup"></a><span data-ttu-id="841a0-194">Начальное резервное копирование</span><span class="sxs-lookup"><span data-stu-id="841a0-194">Initial backup</span></span>
<span data-ttu-id="841a0-195">После защищенной виртуальной машины с политикой, можно просмотреть такую связь на hello **защищенные элементы** вкладки. Пока не будет выполнена hello начальной резервной копии, hello **состояние защиты** показано, как **защищенные - (Ожидание начальной резервной копии)**.</span><span class="sxs-lookup"><span data-stu-id="841a0-195">Once a virtual machine has been protected with a policy, you can view that relationship on hello **Protected Items** tab. Until hello initial backup occurs, hello **Protection Status** shows as **Protected - (pending initial backup)**.</span></span> <span data-ttu-id="841a0-196">По умолчанию hello первого запланированного резервного копирования — hello *начальной резервной копии*.</span><span class="sxs-lookup"><span data-stu-id="841a0-196">By default, hello first scheduled backup is hello *initial backup*.</span></span>

![Статус "В ожидании резервного копирования"](./media/backup-azure-vms-first-look/protection-pending-border.png)

<span data-ttu-id="841a0-198">toostart hello начальной резервной копии теперь:</span><span class="sxs-lookup"><span data-stu-id="841a0-198">toostart hello initial backup now:</span></span>

1. <span data-ttu-id="841a0-199">На hello **защищенные элементы** щелкните **создать резервную копию** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="841a0-199">On hello **Protected Items** page, click **Backup Now** at hello bottom of hello page.</span></span>
    <span data-ttu-id="841a0-200">![Элемент "Архивировать"](./media/backup-azure-vms-first-look/backup-now-icon.png)</span><span class="sxs-lookup"><span data-stu-id="841a0-200">![Backup Now icon](./media/backup-azure-vms-first-look/backup-now-icon.png)</span></span>

    <span data-ttu-id="841a0-201">Hello службы резервного копирования Azure создает задание резервного копирования для hello начальной резервной копии.</span><span class="sxs-lookup"><span data-stu-id="841a0-201">hello Azure Backup service creates a backup job for hello initial backup operation.</span></span>
2. <span data-ttu-id="841a0-202">Нажмите кнопку hello **заданий** вкладку tooview hello список заданий.</span><span class="sxs-lookup"><span data-stu-id="841a0-202">Click hello **Jobs** tab tooview hello list of jobs.</span></span>

    ![Выполняется резервное копирование](./media/backup-azure-vms-first-look/protect-inprogress.png)

    <span data-ttu-id="841a0-204">После завершения начальной резервной копии, состояние hello hello виртуальной машины в hello **защищенные элементы** вкладка — *Protected*.</span><span class="sxs-lookup"><span data-stu-id="841a0-204">When initial backup is complete, hello status of hello virtual machine in hello **Protected Items** tab is *Protected*.</span></span>

    ![Резервное копирование виртуальной машины с точкой восстановления](./media/backup-azure-vms/protect-backedupvm.png)

   > [!NOTE]
   > <span data-ttu-id="841a0-206">Резервное копирование виртуальных машин — локальный процесс.</span><span class="sxs-lookup"><span data-stu-id="841a0-206">Backing up virtual machines is a local process.</span></span> <span data-ttu-id="841a0-207">Не удается резервное копирование виртуальных машин с одного резервное хранилище области tooa в другой области.</span><span class="sxs-lookup"><span data-stu-id="841a0-207">You cannot back up virtual machines from one region tooa backup vault in another region.</span></span> <span data-ttu-id="841a0-208">Таким образом для каждого региона Azure, с виртуальных машин, требующих toobe резервного копирования, по крайней мере один резервного хранилища должны создаваться в этом регионе.</span><span class="sxs-lookup"><span data-stu-id="841a0-208">So, for every Azure region that has VMs that need toobe backed up, at least one backup vault must be created in that region.</span></span>
   >
   >

## <a name="next-steps"></a><span data-ttu-id="841a0-209">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="841a0-209">Next steps</span></span>
<span data-ttu-id="841a0-210">Теперь, когда резервное копирование виртуальной машины успешно завершено, вы можете выполнить еще несколько действий.</span><span class="sxs-lookup"><span data-stu-id="841a0-210">Now that you have successfully backed up a VM, there are several next steps that could be of interest.</span></span> <span data-ttu-id="841a0-211">Hello проще всего toofamiliarize самостоятельно с восстановлением данных tooa виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="841a0-211">hello most logical step is toofamiliarize yourself with restoring data tooa VM.</span></span> <span data-ttu-id="841a0-212">Однако существуют задачи управления, которые помогут вам понять, как tookeep безопасном данных и минимизации расходов.</span><span class="sxs-lookup"><span data-stu-id="841a0-212">However, there are management tasks that will help you understand how tookeep your data safe and minimize costs.</span></span>

* [<span data-ttu-id="841a0-213">Мониторинг виртуальных машин и управление ими</span><span class="sxs-lookup"><span data-stu-id="841a0-213">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="841a0-214">Восстановление виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="841a0-214">Restore virtual machines</span></span>](backup-azure-restore-vms.md)
* [<span data-ttu-id="841a0-215">Рекомендации по устранению неполадок</span><span class="sxs-lookup"><span data-stu-id="841a0-215">Troubleshooting guidance</span></span>](backup-azure-vms-troubleshoot.md)

## <a name="questions"></a><span data-ttu-id="841a0-216">Вопросы?</span><span class="sxs-lookup"><span data-stu-id="841a0-216">Questions?</span></span>
<span data-ttu-id="841a0-217">Если у вас есть вопросы или при наличии любой возможности, хотелось бы включены, toosee [отправить отзыв](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="841a0-217">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>
