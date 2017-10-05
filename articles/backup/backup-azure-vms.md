---
title: "Архивация классических виртуальных машин Azure в хранилище архивации | Документация Майкрософт"
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
ms.openlocfilehash: e1da8bce96078a43c656f84005cefc8bbe81c9e3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="back-up-azure-virtual-machines-classic-portal"></a><span data-ttu-id="5a846-104">Архивация виртуальных машин Azure (классический портал)</span><span class="sxs-lookup"><span data-stu-id="5a846-104">Back up Azure virtual machines (classic portal)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5a846-105">Резервное копирование виртуальных машин в хранилище служб восстановления</span><span class="sxs-lookup"><span data-stu-id="5a846-105">Back up VMs to Recovery Services vault</span></span>](backup-azure-arm-vms.md)
> * [<span data-ttu-id="5a846-106">Резервное копирование виртуальных машин в хранилище архивации</span><span class="sxs-lookup"><span data-stu-id="5a846-106">Back up VMs to Backup vault</span></span>](backup-azure-vms.md)
>
>

<span data-ttu-id="5a846-107">В этой статье описываются процедуры резервного копирования виртуальной машины (VM) Azure, развернутой с использованием классической модели развертывания, в хранилище архивации.</span><span class="sxs-lookup"><span data-stu-id="5a846-107">This article provides the procedures for backing up a Classic-deployed Azure virtual machine (VM) to a Backup vault.</span></span> <span data-ttu-id="5a846-108">Есть несколько задач, которые необходимо выполнить до резервного копирования виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="5a846-108">There are a few tasks you need to take care of before you can back up an Azure virtual machine.</span></span> <span data-ttu-id="5a846-109">Выполните [предварительные требования](backup-azure-vms-prepare.md) (если вы еще этого не сделали), чтобы подготовить среду к резервному копированию виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5a846-109">If you haven't already done so, complete the [prerequisites](backup-azure-vms-prepare.md) to prepare your environment for backing up your VMs.</span></span>

<span data-ttu-id="5a846-110">Дополнительные сведения см. в статьях о [планировании инфраструктуры архивации виртуальных машин в Azure](backup-azure-vms-introduction.md) и о [виртуальных машинах Azure](https://azure.microsoft.com/documentation/services/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="5a846-110">For additional information, see the articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span>

> [!NOTE]
> <span data-ttu-id="5a846-111">В Azure предусмотрены две модели развертывания, позволяющие создавать ресурсы и работать с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="5a846-111">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="5a846-112">Хранилище архивации может защитить только виртуальные машины, которые были развернуты с использованием классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="5a846-112">A Backup vault can only protect Classic-deployed VMs.</span></span> <span data-ttu-id="5a846-113">С помощью хранилища архивации невозможно защитить виртуальные машины, развернутые с использованием модели Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5a846-113">You cannot protect Resource Manager-deployed VMs with a Backup vault.</span></span> <span data-ttu-id="5a846-114">Дополнительные сведения о работе с хранилищем служб восстановления см. в статье [Резервное копирование виртуальных машин Azure в хранилище служб восстановления](backup-azure-arm-vms.md).</span><span class="sxs-lookup"><span data-stu-id="5a846-114">See [Back up VMs to Recovery Services vault](backup-azure-arm-vms.md) for details on working with Recovery Services vaults.</span></span>
>
>

<span data-ttu-id="5a846-115">Резервное копирование виртуальных машин Azure состоит из трех основных шагов.</span><span class="sxs-lookup"><span data-stu-id="5a846-115">Backing up Azure virtual machines involves three key steps:</span></span>

![Три этапа резервного копирования виртуальной машины Azure IaaS](./media/backup-azure-vms/3-steps-for-backup.png)

> [!NOTE]
> <span data-ttu-id="5a846-117">Резервное копирование виртуальных машин — локальный процесс.</span><span class="sxs-lookup"><span data-stu-id="5a846-117">Backing up virtual machines is a local process.</span></span> <span data-ttu-id="5a846-118">Выполнить архивацию виртуальных машин из одного региона в хранилище архивации в другом регионе нельзя.</span><span class="sxs-lookup"><span data-stu-id="5a846-118">You cannot back up virtual machines in one region to a backup vault in another region.</span></span> <span data-ttu-id="5a846-119">Поэтому необходимо создать хранилище архивации в каждом регионе Azure, в котором есть виртуальные машины, которые будут архивироваться.</span><span class="sxs-lookup"><span data-stu-id="5a846-119">So, you must create a backup vault in each Azure region, where there are VMs that will be backed up.</span></span>
>
> [!IMPORTANT]
> <span data-ttu-id="5a846-120">Начиная с марта 2017 года классический портал больше нельзя использовать для создания хранилищ службы архивации.</span><span class="sxs-lookup"><span data-stu-id="5a846-120">Starting March 2017, you can no longer use the classic portal to create Backup vaults.</span></span>
> <span data-ttu-id="5a846-121">Теперь вы можете обновить свои резервные хранилища до хранилищ служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="5a846-121">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="5a846-122">См. дополнительные сведения об [обновлении резервного хранилища до хранилища служб восстановления](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="5a846-122">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="5a846-123">Корпорация Майкрософт рекомендует обновить резервные хранилища до хранилищ служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="5a846-123">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="5a846-124">После 15 октября 2017 года вы не сможете использовать PowerShell для создания резервных хранилищ.</span><span class="sxs-lookup"><span data-stu-id="5a846-124">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="5a846-125">**К 1 ноября 2017 года**:</span><span class="sxs-lookup"><span data-stu-id="5a846-125">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="5a846-126">Все остальные резервные хранилища будут автоматически обновлены до хранилищ служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="5a846-126">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="5a846-127">Вы не сможете получить доступ к данным резервных копий на классическом портале.</span><span class="sxs-lookup"><span data-stu-id="5a846-127">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="5a846-128">Вместо этого для доступа к данным резервных копий в хранилищах служб восстановления используйте портал Azure.</span><span class="sxs-lookup"><span data-stu-id="5a846-128">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="step-1---discover-azure-virtual-machines"></a><span data-ttu-id="5a846-129">Шаг 1. Обнаружение виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="5a846-129">Step 1 - Discover Azure virtual machines</span></span>
<span data-ttu-id="5a846-130">Чтобы идентифицировать все виртуальные машины, недавно добавленные в подписку, перед регистрацией, запустите процесс обнаружения.</span><span class="sxs-lookup"><span data-stu-id="5a846-130">To ensure any new virtual machines (VMs) added to the subscription are identified before registering, run the discovery process.</span></span> <span data-ttu-id="5a846-131">В ходе этого процесса в Azure отправляется запрос о предоставлении списка виртуальных машин в подписке и дополнительных сведений, в том числе имени и региона облачной службы.</span><span class="sxs-lookup"><span data-stu-id="5a846-131">The process queries Azure for the list of virtual machines in the subscription, along with additional information like the cloud service name and the region.</span></span>

1. <span data-ttu-id="5a846-132">Войдите на [классический портал](http://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="5a846-132">Sign in to the [Classic portal](http://manage.windowsazure.com/)</span></span>
2. <span data-ttu-id="5a846-133">В списке служб Azure щелкните **Службы восстановления**, чтобы открыть список хранилищ служб архивации и Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="5a846-133">In the list of Azure services, click **Recovery Services** to open the list of Backup and Site Recovery vaults.</span></span>
    <span data-ttu-id="5a846-134">![Открытие списка хранилищ](./media/backup-azure-vms/choose-vault-list.png)</span><span class="sxs-lookup"><span data-stu-id="5a846-134">![Open vault list](./media/backup-azure-vms/choose-vault-list.png)</span></span>
3. <span data-ttu-id="5a846-135">Из списка хранилищ архивации выберите хранилище для архивации виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="5a846-135">In the list of Backup vaults, select the vault to back up a VM.</span></span>

    <span data-ttu-id="5a846-136">Если это новое хранилище, на портале откроется страница **быстрого запуска** .</span><span class="sxs-lookup"><span data-stu-id="5a846-136">If this is a new vault the portal opens to the **Quick Start** page.</span></span>

    ![Открытие меню "Зарегистрированные элементы"](./media/backup-azure-vms/vault-quick-start.png)

    <span data-ttu-id="5a846-138">Если это уже настроенное хранилище, на портале откроется меню последних использованных элементов.</span><span class="sxs-lookup"><span data-stu-id="5a846-138">If the vault has previously been configured, the portal opens to the most recently used menu.</span></span>
4. <span data-ttu-id="5a846-139">В меню хранилища (в верхней части страницы) щелкните **Зарегистрированные элементы**.</span><span class="sxs-lookup"><span data-stu-id="5a846-139">From the vault menu (at the top of the page), click **Registered Items**.</span></span>

    ![Открытие меню "Зарегистрированные элементы"](./media/backup-azure-vms/vault-menu.png)
5. <span data-ttu-id="5a846-141">В меню **Тип** выберите пункт **Виртуальная машина Azure**.</span><span class="sxs-lookup"><span data-stu-id="5a846-141">From the **Type** menu, select **Azure Virtual Machine**.</span></span>

    ![Выбор рабочей нагрузки](./media/backup-azure-vms/discovery-select-workload.png)
6. <span data-ttu-id="5a846-143">В нижней части страницы щелкните **Обнаружить** .</span><span class="sxs-lookup"><span data-stu-id="5a846-143">Click **DISCOVER** at the bottom of the page.</span></span>
    <span data-ttu-id="5a846-144">![Кнопка обнаружения](./media/backup-azure-vms/discover-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="5a846-144">![Discover button](./media/backup-azure-vms/discover-button-only.png)</span></span>

    <span data-ttu-id="5a846-145">Процесс обнаружения может длиться несколько минут, в течение которых будет создаваться таблица со списком виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5a846-145">The discovery process may take a few minutes while the virtual machines are being tabulated.</span></span> <span data-ttu-id="5a846-146">В нижней части экрана отобразится уведомление о ходе выполнения процесса.</span><span class="sxs-lookup"><span data-stu-id="5a846-146">There is a notification at the bottom of the screen that lets you know that the process is running.</span></span>

    ![Обнаружение виртуальных машин](./media/backup-azure-vms/discovering-vms.png)

    <span data-ttu-id="5a846-148">Уведомление изменится, когда процесс завершится.</span><span class="sxs-lookup"><span data-stu-id="5a846-148">The notification changes when the process is complete.</span></span> <span data-ttu-id="5a846-149">Если процессу обнаружения не удалось найти виртуальные машины, сначала убедитесь, что они существуют.</span><span class="sxs-lookup"><span data-stu-id="5a846-149">If the discovery process did not find the virtual machines, first ensure the VMs exist.</span></span> <span data-ttu-id="5a846-150">Если виртуальные машины существует, убедитесь, что они находятся в одном регионе с хранилищем архивации.</span><span class="sxs-lookup"><span data-stu-id="5a846-150">If the VMs exist, ensure the VMs are in the same region as the backup vault.</span></span> <span data-ttu-id="5a846-151">Если виртуальные машины существуют и находятся в том же регионе, убедитесь, что они еще не зарегистрированы в хранилище архивации.</span><span class="sxs-lookup"><span data-stu-id="5a846-151">If the VMs exist and are in the same region, ensure the VMs are not already registered to a backup vault.</span></span> <span data-ttu-id="5a846-152">Если виртуальные машины назначены хранилищу архивации, их нельзя будет назначить другим хранилищам архивации.</span><span class="sxs-lookup"><span data-stu-id="5a846-152">If a VM is assigned to a backup vault it is not available to be assigned to other backup vaults.</span></span>

    ![Обнаружение завершено](./media/backup-azure-vms/discovery-complete.png)

    <span data-ttu-id="5a846-154">После обнаружения новых элементов перейдите к шагу 2 и зарегистрируйте виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="5a846-154">Once you have discovered the new items, go to Step 2 and register your VMs.</span></span>

## <a name="step-2---register-azure-virtual-machines"></a><span data-ttu-id="5a846-155">Шаг 2. Регистрация виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="5a846-155">Step 2 - Register Azure virtual machines</span></span>
<span data-ttu-id="5a846-156">Чтобы связать виртуальную машину со службой архивации Azure, выполняется ее регистрация.</span><span class="sxs-lookup"><span data-stu-id="5a846-156">You register an Azure virtual machine to associate it with the Azure Backup service.</span></span> <span data-ttu-id="5a846-157">Как правило, это разовая операция.</span><span class="sxs-lookup"><span data-stu-id="5a846-157">This is typically a one-time activity.</span></span>

1. <span data-ttu-id="5a846-158">На портале Azure перейдите в хранилище архивации в разделе **Службы восстановления**, а затем откройте вкладку **Зарегистрированные элементы**.</span><span class="sxs-lookup"><span data-stu-id="5a846-158">Navigate to the backup vault under **Recovery Services** in the Azure portal, and then click **Registered Items**.</span></span>
2. <span data-ttu-id="5a846-159">В раскрывающемся меню выберите пункт **Виртуальная машина Azure** .</span><span class="sxs-lookup"><span data-stu-id="5a846-159">Select **Azure Virtual Machine** from the drop-down menu.</span></span>

    ![Выбор рабочей нагрузки](./media/backup-azure-vms/discovery-select-workload.png)
3. <span data-ttu-id="5a846-161">В нижней части страницы щелкните **Зарегистрировать** .</span><span class="sxs-lookup"><span data-stu-id="5a846-161">Click **REGISTER** at the bottom of the page.</span></span>
    <span data-ttu-id="5a846-162">![Кнопка регистрации](./media/backup-azure-vms/register-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="5a846-162">![Register button](./media/backup-azure-vms/register-button-only.png)</span></span>
4. <span data-ttu-id="5a846-163">В контекстном меню **Регистрация элементов** выберите виртуальные машины, которые нужно зарегистрировать.</span><span class="sxs-lookup"><span data-stu-id="5a846-163">In the **Register Items** shortcut menu, select the virtual machines that you want to register.</span></span> <span data-ttu-id="5a846-164">Если в меню отображаются виртуальные машины с одинаковыми именами, используйте облачную службу, чтобы идентифицировать их.</span><span class="sxs-lookup"><span data-stu-id="5a846-164">If there are two or more virtual machines with the same name, use the cloud service to distinguish between them.</span></span>

   > [!TIP]
   > <span data-ttu-id="5a846-165">В ходе одной процедуры можно зарегистрировать несколько виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5a846-165">Multiple virtual machines can be registered at one time.</span></span>
   >
   >

    <span data-ttu-id="5a846-166">Для каждой выбранной виртуальной машины будет создано задание.</span><span class="sxs-lookup"><span data-stu-id="5a846-166">A job is created for each virtual machine that you've selected.</span></span>
5. <span data-ttu-id="5a846-167">В уведомлении щелкните **Просмотреть задание**, чтобы перейти на страницу **Задания**.</span><span class="sxs-lookup"><span data-stu-id="5a846-167">Click **View Job** in the notification to go to the **Jobs** page.</span></span>

    ![Задание регистрации](./media/backup-azure-vms/register-create-job.png)

    <span data-ttu-id="5a846-169">Виртуальная машина также отображается в списке зарегистрированных элементов с указанием состояния операции регистрации.</span><span class="sxs-lookup"><span data-stu-id="5a846-169">The virtual machine also appears in the list of registered items, along with the status of the registration operation.</span></span>

    ![Состояние регистрации 1](./media/backup-azure-vms/register-status01.png)

    <span data-ttu-id="5a846-171">По завершении операции состояние изменится на *registered* (зарегистрировано).</span><span class="sxs-lookup"><span data-stu-id="5a846-171">When the operation completes, the status changes to reflect the *registered* state.</span></span>

    ![Состояние регистрации 2](./media/backup-azure-vms/register-status02.png)

## <a name="step-3---protect-azure-virtual-machines"></a><span data-ttu-id="5a846-173">Шаг 3. Защита виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="5a846-173">Step 3 - Protect Azure virtual machines</span></span>
<span data-ttu-id="5a846-174">Теперь вы можете настроить для виртуальной машины политику резервного копирования и хранения.</span><span class="sxs-lookup"><span data-stu-id="5a846-174">Now you can set up a backup and retention policy for the virtual machine.</span></span> <span data-ttu-id="5a846-175">Одним действием можно защитить несколько виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5a846-175">Multiple virtual machines can be protected by using a single protect action.</span></span>

<span data-ttu-id="5a846-176">Хранилища службы архивации Azure, созданные после мая 2015 г., доступны со встроенной политикой по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="5a846-176">Azure Backup vaults created after May 2015 come with a default policy built into the vault.</span></span> <span data-ttu-id="5a846-177">Эта политика определяет не только стандартный срок хранения (30 дней), но и расписание ежедневного резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="5a846-177">This default policy comes with a default retention of 30 days and a once-daily backup schedule.</span></span>

1. <span data-ttu-id="5a846-178">На портале Azure перейдите в хранилище архивации в разделе **Службы восстановления**, а затем откройте вкладку **Зарегистрированные элементы**.</span><span class="sxs-lookup"><span data-stu-id="5a846-178">Navigate to the backup vault under **Recovery Services** in the Azure portal, and then click **Registered Items**.</span></span>
2. <span data-ttu-id="5a846-179">В раскрывающемся меню выберите пункт **Виртуальная машина Azure** .</span><span class="sxs-lookup"><span data-stu-id="5a846-179">Select **Azure Virtual Machine** from the drop-down menu.</span></span>

    ![Выберите рабочую нагрузку на портале](./media/backup-azure-vms/select-workload.png)
3. <span data-ttu-id="5a846-181">В нижней части страницы щелкните **ЗАЩИТИТЬ** .</span><span class="sxs-lookup"><span data-stu-id="5a846-181">Click **PROTECT** at the bottom of the page.</span></span>

    <span data-ttu-id="5a846-182">Откроется **мастер защиты элементов** .</span><span class="sxs-lookup"><span data-stu-id="5a846-182">The **Protect Items wizard** appears.</span></span> <span data-ttu-id="5a846-183">В этом мастере перечислены только незарегистрированные и незащищенные виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="5a846-183">The wizard only lists virtual machines that are registered and not protected.</span></span> <span data-ttu-id="5a846-184">Выберите виртуальные машины, которые необходимо защитить.</span><span class="sxs-lookup"><span data-stu-id="5a846-184">Select the virtual machines that you want to protect.</span></span>

    <span data-ttu-id="5a846-185">При наличии двух или нескольких виртуальных машин с одинаковым именем используйте облачную службу, чтобы их различить.</span><span class="sxs-lookup"><span data-stu-id="5a846-185">If there are two or more virtual machines with the same name, use the cloud service to distinguish between the virtual machines.</span></span>

   > [!TIP]
   > <span data-ttu-id="5a846-186">Можно защитить несколько виртуальных машин одновременно.</span><span class="sxs-lookup"><span data-stu-id="5a846-186">You can protect multiple virtual machines at one time.</span></span>
   >
   >

    ![Настройка защиты нужного уровня](./media/backup-azure-vms/protect-at-scale.png)

4. <span data-ttu-id="5a846-188">Выберите **расписание резервного копирования** , чтобы создать резервную копию выбранных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5a846-188">Choose a **backup schedule** to back up the virtual machines that you've selected.</span></span> <span data-ttu-id="5a846-189">Выберите политику из существующего набора или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="5a846-189">You can pick from an existing set of policies or define a new one.</span></span>

    <span data-ttu-id="5a846-190">У каждой политики резервного копирования может быть несколько связанных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5a846-190">Each backup policy can have multiple virtual machines associated with it.</span></span> <span data-ttu-id="5a846-191">Но в определенный момент времени виртуальная машина может быть связана только с одной политикой.</span><span class="sxs-lookup"><span data-stu-id="5a846-191">However, the virtual machine can only be associated with one policy at any given point in time.</span></span>

    ![Защита с помощью новой политики](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > <span data-ttu-id="5a846-193">Политика резервного копирования включает схему хранения плановых резервных копий.</span><span class="sxs-lookup"><span data-stu-id="5a846-193">A backup policy includes a retention scheme for the scheduled backups.</span></span> <span data-ttu-id="5a846-194">Выбрав существующую политику архивации, вы не сможете изменить параметры хранения впоследствии.</span><span class="sxs-lookup"><span data-stu-id="5a846-194">If you select an existing backup policy, you cannot modify the retention options in the next step.</span></span>
   >
   >

5. <span data-ttu-id="5a846-195">Выберите **диапазон хранения** , который нужно связать с резервными копиями.</span><span class="sxs-lookup"><span data-stu-id="5a846-195">Choose a **retention range** to associate with the backups.</span></span>

    ![Защита с помощью гибких возможностей хранения](./media/backup-azure-vms/policy-retention.png)

    <span data-ttu-id="5a846-197">Политика хранения определяет длительность хранения резервной копии.</span><span class="sxs-lookup"><span data-stu-id="5a846-197">Retention policy specifies the length of time for storing a backup.</span></span> <span data-ttu-id="5a846-198">Можно указать разные политики хранения на основе времени создания резервной копии.</span><span class="sxs-lookup"><span data-stu-id="5a846-198">You can specify different retention policies based on when the backup is taken.</span></span> <span data-ttu-id="5a846-199">Например, точка ежедневной архивации (которая служит точкой оперативного восстановления) может храниться в течение 90 дней.</span><span class="sxs-lookup"><span data-stu-id="5a846-199">For example, a backup point taken daily (which serves as an operational recovery point) might be preserved for 90 days.</span></span> <span data-ttu-id="5a846-200">В то же время точка архивации, которая обновляется в конце каждого квартала (и служит для целей аудита) может храниться в течение нескольких месяцев или лет.</span><span class="sxs-lookup"><span data-stu-id="5a846-200">In comparison, a backup point taken at the end of each quarter (for audit purposes) may need to be preserved for many months or years.</span></span>

    ![Резервное копирование виртуальной машины с точкой восстановления](./media/backup-azure-vms/long-term-retention.png)

    <span data-ttu-id="5a846-202">Описание политик, приведенных на изображении выше:</span><span class="sxs-lookup"><span data-stu-id="5a846-202">In this example image:</span></span>

   * <span data-ttu-id="5a846-203">**Ежедневная политика хранения**. Резервные копии, создаваемые ежедневно, хранятся в течение 30 дней.</span><span class="sxs-lookup"><span data-stu-id="5a846-203">**Daily retention policy**: Backups taken daily are stored for 30 days.</span></span>
   * <span data-ttu-id="5a846-204">**Еженедельная политика хранения**. Резервные копии, создаваемые каждое воскресенье, хранятся 104 недели.</span><span class="sxs-lookup"><span data-stu-id="5a846-204">**Weekly retention policy**: Backups taken every week on Sunday are preserved for 104 weeks.</span></span>
   * <span data-ttu-id="5a846-205">**Ежемесячная политика хранения**. Резервные копии, создаваемые в последнее воскресенье каждого месяца, хранятся 120 месяцев.</span><span class="sxs-lookup"><span data-stu-id="5a846-205">**Monthly retention policy**: Backups taken on the last Sunday of each month are preserved for 120 months.</span></span>
   * <span data-ttu-id="5a846-206">**Ежегодная политика хранения**. Резервные копии, создаваемые в первое воскресенье января, хранятся 99 лет.</span><span class="sxs-lookup"><span data-stu-id="5a846-206">**Yearly retention policy**: Backups taken on the first Sunday of every January are preserved for 99 years.</span></span>

     <span data-ttu-id="5a846-207">Чтобы настроить политику защиты и связать ее с виртуальными машинами, для каждой выбранной виртуальной машины создается задание.</span><span class="sxs-lookup"><span data-stu-id="5a846-207">A job is created to configure the protection policy and associate the virtual machines to that policy for each virtual machine that you've selected.</span></span>
6. <span data-ttu-id="5a846-208">Чтобы просмотреть список заданий **настройки защиты**, в меню "Хранилища" щелкните **Задания** и выберите **Настройка защиты** для фильтра **Операция**.</span><span class="sxs-lookup"><span data-stu-id="5a846-208">To view the list of **Configure Protection** jobs, from the vaults menu, click **Jobs** and select **Configure Protection** from the **Operation** filter.</span></span>

    ![Настройка задания защиты](./media/backup-azure-vms/protect-configureprotection.png)

## <a name="initial-backup"></a><span data-ttu-id="5a846-210">Начальное резервное копирование</span><span class="sxs-lookup"><span data-stu-id="5a846-210">Initial backup</span></span>
<span data-ttu-id="5a846-211">Виртуальная машина, защищенная политикой, появится на вкладке **Защищенные элементы** с состоянием *Защищено (в ожидании начального резервного копирования)*.</span><span class="sxs-lookup"><span data-stu-id="5a846-211">Once the virtual machine is protected with a policy, it shows up under the **Protected Items** tab with the status of *Protected - (pending initial backup)*.</span></span> <span data-ttu-id="5a846-212">По умолчанию *начальным резервным копированием*является первое запланированное резервное копирование.</span><span class="sxs-lookup"><span data-stu-id="5a846-212">By default, the first scheduled backup is the *initial backup*.</span></span>

<span data-ttu-id="5a846-213">Чтобы активировать начальное резервное копирование сразу же после настройки, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="5a846-213">To trigger the initial backup immediately after configuring protection:</span></span>

1. <span data-ttu-id="5a846-214">В нижней части страницы **Защищенные элементы** щелкните **Выполнить архивацию**.</span><span class="sxs-lookup"><span data-stu-id="5a846-214">At the bottom of the **Protected Items** page, click **Backup Now**.</span></span>

    <span data-ttu-id="5a846-215">Служба архивации Azure создаст задание резервного копирования для операции начального резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="5a846-215">The Azure Backup service creates a backup job for the initial backup operation.</span></span>
2. <span data-ttu-id="5a846-216">Чтобы просмотреть список заданий, щелкните вкладку **Задания** .</span><span class="sxs-lookup"><span data-stu-id="5a846-216">Click the **Jobs** tab to view the list of jobs.</span></span>

    ![Выполняется резервное копирование](./media/backup-azure-vms/protect-inprogress.png)

> [!NOTE]
> <span data-ttu-id="5a846-218">В ходе архивации служба архивации Azure отправляет расширению архивации на каждой виртуальной машине команду освободить все задания записи и сделать согласованный моментальный снимок.</span><span class="sxs-lookup"><span data-stu-id="5a846-218">During the backup operation, the Azure Backup service issues a command to the backup extension in each virtual machine to flush all write jobs and take a consistent snapshot.</span></span>
>
>

<span data-ttu-id="5a846-219">После завершения начальной архивации состояние виртуальной машины на вкладке **Защищенные элементы** изменится на *Защищено*.</span><span class="sxs-lookup"><span data-stu-id="5a846-219">When the initial backup finishes, the status of the virtual machine in the **Protected Items** tab is *Protected*.</span></span>

![Резервное копирование виртуальной машины с точкой восстановления](./media/backup-azure-vms/protect-backedupvm.png)

## <a name="viewing-backup-status-and-details"></a><span data-ttu-id="5a846-221">Просмотр состояния резервного копирования и подробностей</span><span class="sxs-lookup"><span data-stu-id="5a846-221">Viewing backup status and details</span></span>
<span data-ttu-id="5a846-222">После обеспечения защиты число виртуальных машин также увеличивается на странице сводки **Панели мониторинга** .</span><span class="sxs-lookup"><span data-stu-id="5a846-222">Once protected, the virtual machine count also increases in the **Dashboard** page summary.</span></span> <span data-ttu-id="5a846-223">На странице **Панель мониторинга** также отображается количество *успешных*, *завершившихся сбоем* и *выполняющихся* заданий за последние 24 часа.</span><span class="sxs-lookup"><span data-stu-id="5a846-223">The **Dashboard** page also shows the number of jobs from the last 24 hours that were *successful*, have *failed*, and are *in progress*.</span></span> <span data-ttu-id="5a846-224">На странице **Задания** используйте меню **Состояние**, **Операция**, **Из** и **Кому**, чтобы отфильтровать задания.</span><span class="sxs-lookup"><span data-stu-id="5a846-224">On the **Jobs** page, use the **Status**, **Operation**, or **From** and **To** menus to filter the jobs.</span></span>

![Состояние резервного копирования на странице панели мониторинга](./media/backup-azure-vms/dashboard-protectedvms.png)

<span data-ttu-id="5a846-226">Значения на панели мониторинга обновляются каждые 24 часа.</span><span class="sxs-lookup"><span data-stu-id="5a846-226">Values in the dashboard are refreshed once every 24 hours.</span></span>

## <a name="troubleshooting-errors"></a><span data-ttu-id="5a846-227">Устранение ошибок</span><span class="sxs-lookup"><span data-stu-id="5a846-227">Troubleshooting errors</span></span>
<span data-ttu-id="5a846-228">Если во время архивации виртуальной машины возникнут проблемы, см. статью об [устранении неполадок при архивации виртуальных машин Azure](backup-azure-vms-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="5a846-228">If you run into issues while backing up your virtual machine, look at the [VM     troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a846-229">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5a846-229">Next steps</span></span>
* [<span data-ttu-id="5a846-230">Мониторинг виртуальных машин и управление ими</span><span class="sxs-lookup"><span data-stu-id="5a846-230">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="5a846-231">Восстановление виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="5a846-231">Restore virtual machines</span></span>](backup-azure-restore-vms.md)
