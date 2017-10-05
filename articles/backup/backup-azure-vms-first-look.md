---
title: "Первое знакомство. Резервное копирование виртуальных машин Azure в хранилище службы архивации | Документация Майкрософт"
description: "Используйте классический портал для резервного копирования виртуальных машин Azure в хранилище службы архивации. В этом руководстве описываются все этапы, включая создание хранилища службы архивации, регистрацию виртуальных машин, создание политики архивации и выполнение задания начального резервного копирования."
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
ms.openlocfilehash: fc31d7654e455ec5b4e4bb9af4cf1a166f1661ee
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="first-look-backing-up-azure-virtual-machines"></a><span data-ttu-id="02365-104">Первое знакомство: резервное копирование виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="02365-104">First look: Backing up Azure virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="02365-105">Защита виртуальных машин в хранилище служб восстановления</span><span class="sxs-lookup"><span data-stu-id="02365-105">Protect VMs with a recovery services vault</span></span>](backup-azure-vms-first-look-arm.md)
> * [<span data-ttu-id="02365-106">Защита виртуальных машин Azure в хранилище службы архивации</span><span class="sxs-lookup"><span data-stu-id="02365-106">Protect Azure VMs with a backup vault</span></span>](backup-azure-vms-first-look.md)
>
>

<span data-ttu-id="02365-107">В этом руководстве описана процедура резервного копирования виртуальной машины (ВМ) в резервное хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="02365-107">This tutorial takes you through the steps for backing up an Azure virtual machine (VM) to a backup vault in Azure.</span></span> <span data-ttu-id="02365-108">В этой статье описывается классическая модель развертывания (модель развертывания Service Manager) для резервного копирования виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="02365-108">This article describes the classic model or Service Manager deployment model, for backing up VMs.</span></span> <span data-ttu-id="02365-109">Следующие инструкции применяются только к хранилищам службы архивации, созданным на классическом портале.</span><span class="sxs-lookup"><span data-stu-id="02365-109">The following steps apply only to Backup vaults created in the classic portal.</span></span> <span data-ttu-id="02365-110">Для новых развертываний мы советуем использовать модель развертывания Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="02365-110">Microsoft recommends using the Resource Manager model for new deployments.</span></span>

<span data-ttu-id="02365-111">Дополнительные сведения об архивации виртуальной машины в хранилище служб восстановления, которое принадлежит к группе ресурсов, см. в статье [Первое знакомство. Защита виртуальных машин в хранилище служб восстановления](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="02365-111">If you are interested in backing up a VM to a Recovery Services vault that belongs to a Resource Group, see [First look: Protect VMs with a recovery services vault](backup-azure-vms-first-look-arm.md).</span></span>

<span data-ttu-id="02365-112">Для успешного выполнения заданий этого руководства необходимо предварительно:</span><span class="sxs-lookup"><span data-stu-id="02365-112">To successfully complete the following tutorial, these prerequisites must exist:</span></span>

* <span data-ttu-id="02365-113">создать виртуальную машину в подписке Azure;</span><span class="sxs-lookup"><span data-stu-id="02365-113">You have created a VM in your Azure subscription.</span></span>
* <span data-ttu-id="02365-114">обеспечить подключение виртуальной машины к общедоступным IP-адресам Azure.</span><span class="sxs-lookup"><span data-stu-id="02365-114">The VM has connectivity to Azure public IP addresses.</span></span> <span data-ttu-id="02365-115">Дополнительные сведения см. в разделе [Сетевое подключение](backup-azure-vms-prepare.md#network-connectivity).</span><span class="sxs-lookup"><span data-stu-id="02365-115">For additional information, see [Network connectivity](backup-azure-vms-prepare.md#network-connectivity).</span></span>


> [!NOTE]
> <span data-ttu-id="02365-116">В Azure предусмотрены две модели развертывания, позволяющие создавать ресурсы и работать с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="02365-116">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="02365-117">Это руководство предназначено для использования при работе с виртуальными машинами, созданными на классическом портале.</span><span class="sxs-lookup"><span data-stu-id="02365-117">This tutorial is for use with virtual machines created in the classic portal.</span></span>
>
>

## <a name="create-a-backup-vault"></a><span data-ttu-id="02365-118">создать хранилище архивации;</span><span class="sxs-lookup"><span data-stu-id="02365-118">Create a backup vault</span></span>
<span data-ttu-id="02365-119">Хранилище архивации — это сущность, в которой хранятся созданные резервные копии и точки восстановления.</span><span class="sxs-lookup"><span data-stu-id="02365-119">A backup vault is an entity that stores all the backups and recovery points that have been created over time.</span></span> <span data-ttu-id="02365-120">Хранилище службы архивации также содержит политики резервного копирования, применяемые к виртуальным машинам, для которых настроена архивация.</span><span class="sxs-lookup"><span data-stu-id="02365-120">The backup vault also contains the backup policies that are applied to the virtual machines being backed up.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="02365-121">Начиная с марта 2017 года классический портал больше нельзя использовать для создания хранилищ службы архивации.</span><span class="sxs-lookup"><span data-stu-id="02365-121">Starting March 2017, you can no longer use the classic portal to create Backup vaults.</span></span>
> <span data-ttu-id="02365-122">Теперь можно обновить свои резервные хранилища до хранилищ служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="02365-122">You can upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="02365-123">См. дополнительные сведения об [обновлении резервного хранилища до хранилища служб восстановления](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="02365-123">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="02365-124">Корпорация Майкрософт рекомендует обновить резервные хранилища до хранилищ служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="02365-124">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="02365-125">После 15 октября 2017 года вы не сможете использовать PowerShell для создания резервных хранилищ.</span><span class="sxs-lookup"><span data-stu-id="02365-125">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="02365-126">**К 1 ноября 2017 года**:</span><span class="sxs-lookup"><span data-stu-id="02365-126">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="02365-127">Все остальные резервные хранилища будут автоматически обновлены до хранилищ служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="02365-127">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="02365-128">Вы не сможете получить доступ к данным резервных копий на классическом портале.</span><span class="sxs-lookup"><span data-stu-id="02365-128">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="02365-129">Вместо этого для доступа к данным резервных копий в хранилищах служб восстановления используйте портал Azure.</span><span class="sxs-lookup"><span data-stu-id="02365-129">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="discover-and-register-azure-virtual-machines"></a><span data-ttu-id="02365-130">Обнаружение и регистрация виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="02365-130">Discover and Register Azure virtual machines</span></span>
<span data-ttu-id="02365-131">Перед регистрацией VM в хранилище запустите процесс обнаружения, чтобы определить новые виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="02365-131">Before registering the VM with a vault, run the discovery process to identify any new VMs.</span></span> <span data-ttu-id="02365-132">В ходе этого процесса возвращается список виртуальных машин в подписке и дополнительные сведения о них, в том числе имя и регион облачной службы.</span><span class="sxs-lookup"><span data-stu-id="02365-132">This returns a list of virtual machines in the subscription, along with additional information like the cloud service name and the region.</span></span>

1. <span data-ttu-id="02365-133">Войдите на [классический портал Azure](http://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="02365-133">Sign in to the [Azure Classic portal](http://manage.windowsazure.com/)</span></span>
2. <span data-ttu-id="02365-134">На классическом портале Azure щелкните **Службы восстановления**, чтобы открыть список хранилищ служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="02365-134">In the Azure classic portal, click **Recovery Services** to open the list of Recovery Services vaults.</span></span>
    <span data-ttu-id="02365-135">![Выбор рабочей нагрузки](./media/backup-azure-vms-first-look/recovery-services-icon.png)</span><span class="sxs-lookup"><span data-stu-id="02365-135">![Select workload](./media/backup-azure-vms-first-look/recovery-services-icon.png)</span></span>
3. <span data-ttu-id="02365-136">Из списка выберите хранилище для резервного копирования виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="02365-136">From the list of vaults, select the vault to back up a VM.</span></span>

    <span data-ttu-id="02365-137">Когда вы выберете хранилище, откроется страница **Быстрый запуск** .</span><span class="sxs-lookup"><span data-stu-id="02365-137">When you select your vault, it opens in the **Quick Start** page</span></span>
4. <span data-ttu-id="02365-138">В меню хранилища выберите пункт **Зарегистрированные элементы**.</span><span class="sxs-lookup"><span data-stu-id="02365-138">From the vault menu, click **Registered Items**.</span></span>

    ![Выбор рабочей нагрузки](./media/backup-azure-vms-first-look/configure-registered-items.png)
5. <span data-ttu-id="02365-140">В меню **Тип** выберите пункт **Виртуальная машина Azure**.</span><span class="sxs-lookup"><span data-stu-id="02365-140">From the **Type** menu, select **Azure Virtual Machine**.</span></span>

    ![Выбор рабочей нагрузки](./media/backup-azure-vms/discovery-select-workload.png)
6. <span data-ttu-id="02365-142">В нижней части страницы щелкните **Обнаружить** .</span><span class="sxs-lookup"><span data-stu-id="02365-142">Click **DISCOVER** at the bottom of the page.</span></span>
    <span data-ttu-id="02365-143">![Кнопка обнаружения](./media/backup-azure-vms/discover-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="02365-143">![Discover button](./media/backup-azure-vms/discover-button-only.png)</span></span>

    <span data-ttu-id="02365-144">Процесс обнаружения может длиться несколько минут, в течение которых будет создаваться таблица со списком виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="02365-144">The discovery process may take a few minutes while the virtual machines are being tabulated.</span></span> <span data-ttu-id="02365-145">В нижней части экрана отобразится уведомление о ходе выполнения процесса.</span><span class="sxs-lookup"><span data-stu-id="02365-145">There is a notification at the bottom of the screen that lets you know that the process is running.</span></span>

    ![Обнаружение виртуальных машин](./media/backup-azure-vms/discovering-vms.png)

    <span data-ttu-id="02365-147">Уведомление изменится, когда процесс завершится.</span><span class="sxs-lookup"><span data-stu-id="02365-147">The notification changes when the process is complete.</span></span>

    ![Обнаружение завершено](./media/backup-azure-vms-first-look/discovery-complete.png)
7. <span data-ttu-id="02365-149">В нижней части страницы щелкните **Зарегистрировать** .</span><span class="sxs-lookup"><span data-stu-id="02365-149">Click **REGISTER** at the bottom of the page.</span></span>
    <span data-ttu-id="02365-150">![Кнопка регистрации](./media/backup-azure-vms-first-look/register-icon.png)</span><span class="sxs-lookup"><span data-stu-id="02365-150">![Register button](./media/backup-azure-vms-first-look/register-icon.png)</span></span>
8. <span data-ttu-id="02365-151">В контекстном меню **Регистрация элементов** выберите виртуальные машины, которые нужно зарегистрировать.</span><span class="sxs-lookup"><span data-stu-id="02365-151">In the **Register Items** shortcut menu, select the virtual machines that you want to register.</span></span>

   > [!TIP]
   > <span data-ttu-id="02365-152">В ходе одной процедуры можно зарегистрировать несколько виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="02365-152">Multiple virtual machines can be registered at one time.</span></span>
   >
   >

    <span data-ttu-id="02365-153">Для каждой выбранной виртуальной машины будет создано задание.</span><span class="sxs-lookup"><span data-stu-id="02365-153">A job is created for each virtual machine that you've selected.</span></span>
9. <span data-ttu-id="02365-154">В уведомлении щелкните **Просмотреть задание**, чтобы перейти на страницу **Задания**.</span><span class="sxs-lookup"><span data-stu-id="02365-154">Click **View Job** in the notification to go to the **Jobs** page.</span></span>

    ![Задание регистрации](./media/backup-azure-vms/register-create-job.png)

    <span data-ttu-id="02365-156">Виртуальная машина также отображается в списке зарегистрированных элементов с указанием состояния операции регистрации.</span><span class="sxs-lookup"><span data-stu-id="02365-156">The virtual machine also appears in the list of registered items, along with the status of the registration operation.</span></span>

    ![Состояние регистрации 1](./media/backup-azure-vms/register-status01.png)

    <span data-ttu-id="02365-158">По завершении операции состояние изменится на *registered* (зарегистрировано).</span><span class="sxs-lookup"><span data-stu-id="02365-158">When the operation completes, the status changes to reflect the *registered* state.</span></span>

    ![Состояние регистрации 2](./media/backup-azure-vms/register-status02.png)

## <a name="install-the-vm-agent-on-the-virtual-machine"></a><span data-ttu-id="02365-160">Установка агента ВМ на виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="02365-160">Install the VM Agent on the virtual machine</span></span>
<span data-ttu-id="02365-161">Агент VM Azure необходимо установить на виртуальной машине Azure, чтобы обеспечить работоспособность модуля резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="02365-161">The Azure VM Agent must be installed on the Azure virtual machine for the Backup extension to work.</span></span> <span data-ttu-id="02365-162">Если виртуальная машина создана из коллекции Azure, на ней уже есть агент VM. Вы можете перейти к [защите виртуальных машин](backup-azure-vms-first-look.md#create-the-backup-policy).</span><span class="sxs-lookup"><span data-stu-id="02365-162">If your VM was created from the Azure gallery, the VM Agent is already present on the VM; you can skip to [protecting your VMs](backup-azure-vms-first-look.md#create-the-backup-policy).</span></span>

<span data-ttu-id="02365-163">Если виртуальная машина перенесена из локального центра данных, возможно, на ней не установлен агент VM.</span><span class="sxs-lookup"><span data-stu-id="02365-163">If your VM migrated from an on-premises datacenter, the VM probably does not have the VM Agent installed.</span></span> <span data-ttu-id="02365-164">Чтобы защитить виртуальную машину, перед продолжением необходимо установить на ней агент VM.</span><span class="sxs-lookup"><span data-stu-id="02365-164">You must install the VM Agent on the virtual machine before proceeding to protect the VM.</span></span> <span data-ttu-id="02365-165">Подробные инструкции по установке агента виртуальной машины см. в [разделе, посвященном агенту виртуальной машины, статьи об архивации виртуальных машин Azure](backup-azure-vms-prepare.md#vm-agent).</span><span class="sxs-lookup"><span data-stu-id="02365-165">For detailed steps on installing the VM Agent, see the [VM Agent section of the Backup VMs article](backup-azure-vms-prepare.md#vm-agent).</span></span>

## <a name="create-the-backup-policy"></a><span data-ttu-id="02365-166">Создание политики архивации</span><span class="sxs-lookup"><span data-stu-id="02365-166">Create the backup policy</span></span>
<span data-ttu-id="02365-167">Прежде чем инициировать задание начального резервного копирования, определите расписание создания снимков резервной копии.</span><span class="sxs-lookup"><span data-stu-id="02365-167">Before you trigger the initial backup job, set the schedule when backup snapshots are taken.</span></span> <span data-ttu-id="02365-168">Расписание создания снимков резервной копии и время хранения этих снимков — это и есть политика резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="02365-168">The schedule when backup snapshots are taken, and the length of time those snapshots are retained, is the backup policy.</span></span> <span data-ttu-id="02365-169">Сведения о хранении основаны на схеме ротации резервных копий "дед-отец-сын".</span><span class="sxs-lookup"><span data-stu-id="02365-169">The retention information is based on Grandfather-father-son backup rotation scheme.</span></span>

1. <span data-ttu-id="02365-170">На классическом портале Azure в разделе **Службы восстановления** перейдите в хранилище службы архивации и откройте вкладку **Зарегистрированные элементы**.</span><span class="sxs-lookup"><span data-stu-id="02365-170">Navigate to the backup vault under **Recovery Services** in the Azure Classic portal, and  click **Registered Items**.</span></span>
2. <span data-ttu-id="02365-171">В раскрывающемся меню выберите пункт **Виртуальная машина Azure** .</span><span class="sxs-lookup"><span data-stu-id="02365-171">Select **Azure Virtual Machine** from the drop-down menu.</span></span>

    ![Выберите рабочую нагрузку на портале](./media/backup-azure-vms/select-workload.png)
3. <span data-ttu-id="02365-173">В нижней части страницы щелкните **Защитить** .</span><span class="sxs-lookup"><span data-stu-id="02365-173">Click **PROTECT** at the bottom of the page.</span></span>
    <span data-ttu-id="02365-174">![Элемент "Защитить"](./media/backup-azure-vms-first-look/protect-icon.png)</span><span class="sxs-lookup"><span data-stu-id="02365-174">![Click Protect](./media/backup-azure-vms-first-look/protect-icon.png)</span></span>

    <span data-ttu-id="02365-175">Откроется **мастер защиты элементов** со списком *только* зарегистрированных и незащищенных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="02365-175">The **Protect Items wizard** appears and lists *only* virtual machines that are registered and not protected.</span></span>

    ![Настройка защиты нужного уровня](./media/backup-azure-vms/protect-at-scale.png)
4. <span data-ttu-id="02365-177">Выберите виртуальные машины, которые необходимо защитить.</span><span class="sxs-lookup"><span data-stu-id="02365-177">Select the virtual machines that you want to protect.</span></span>

    <span data-ttu-id="02365-178">Чтобы различить несколько виртуальных машин с одинаковым именем, используйте облачную службу.</span><span class="sxs-lookup"><span data-stu-id="02365-178">If there are two or more virtual machines with the same name, use the Cloud Service to distinguish between the virtual machines.</span></span>
5. <span data-ttu-id="02365-179">В меню **Настройка защиты** выберите существующую политику или создайте новую, чтобы защитить указанные виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="02365-179">On the **Configure protection** menu select an existing policy or create a new policy to protect the virtual machines that you identified.</span></span>

    <span data-ttu-id="02365-180">Для новых хранилищ резервных копий устанавливается политика резервного копирования по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="02365-180">New Backup vaults have a default policy associated with the vault.</span></span> <span data-ttu-id="02365-181">Согласно этой политике снимок создается каждый вечер и хранится в течение 30 дней.</span><span class="sxs-lookup"><span data-stu-id="02365-181">This policy takes a daily snapshot each evening, and the daily snapshot is retained for 30 days.</span></span> <span data-ttu-id="02365-182">У каждой политики резервного копирования может быть несколько связанных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="02365-182">Each backup policy can have multiple virtual machines associated with it.</span></span> <span data-ttu-id="02365-183">Но за один раз виртуальная машина может быть связана только с одной политикой.</span><span class="sxs-lookup"><span data-stu-id="02365-183">However, the virtual machine can only be associated with one policy at a time.</span></span>

    ![Защита с помощью новой политики](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > <span data-ttu-id="02365-185">Политика резервного копирования включает схему хранения плановых резервных копий.</span><span class="sxs-lookup"><span data-stu-id="02365-185">A backup policy includes a retention scheme for the scheduled backups.</span></span> <span data-ttu-id="02365-186">Выбрав существующую политику резервного копирования, вы не сможете впоследствии изменить параметры хранения.</span><span class="sxs-lookup"><span data-stu-id="02365-186">If you select an existing backup policy, you will be unable to modify the retention options in the next step.</span></span>
   >
   >
6. <span data-ttu-id="02365-187">В разделе **Диапазон хранения** выберите нужный вариант для ваших точек резервного копирования: ежедневно, еженедельно, ежемесячно или ежегодно.</span><span class="sxs-lookup"><span data-stu-id="02365-187">On **Retention Range** define the daily, weekly, monthly, and yearly scope for the specific backup points.</span></span>

    ![Резервное копирование виртуальной машины с точкой восстановления](./media/backup-azure-vms/long-term-retention.png)

    <span data-ttu-id="02365-189">Политика хранения определяет длительность хранения резервной копии.</span><span class="sxs-lookup"><span data-stu-id="02365-189">Retention policy specifies the length of time for storing a backup.</span></span> <span data-ttu-id="02365-190">Можно указать разные политики хранения на основе времени создания резервной копии.</span><span class="sxs-lookup"><span data-stu-id="02365-190">You can specify different retention policies based on when the backup is taken.</span></span>
7. <span data-ttu-id="02365-191">Щелкните **Задания**, чтобы просмотреть список заданий по **настройке защиты**.</span><span class="sxs-lookup"><span data-stu-id="02365-191">Click **Jobs** to view the list of **Configure Protection** jobs.</span></span>

    ![Настройка задания защиты](./media/backup-azure-vms/protect-configureprotection.png)

    <span data-ttu-id="02365-193">Теперь, когда вы определили политику, перейдите к следующему этапу и запустите начальное резервное копирование.</span><span class="sxs-lookup"><span data-stu-id="02365-193">Now that you've established the policy, go to the next step and run the initial backup.</span></span>

## <a name="initial-backup"></a><span data-ttu-id="02365-194">Начальное резервное копирование</span><span class="sxs-lookup"><span data-stu-id="02365-194">Initial backup</span></span>
<span data-ttu-id="02365-195">Защитив виртуальную машину с помощью политики, можно просмотреть связанные сведения на вкладке **Защищенные элементы** . Пока не начнется начальное резервное копирование, для параметра **Состояние защиты** будет отображаться значение **Protected - (pending initial backup)** (Защищено (в ожидании начального резервного копирования)).</span><span class="sxs-lookup"><span data-stu-id="02365-195">Once a virtual machine has been protected with a policy, you can view that relationship on the **Protected Items** tab. Until the initial backup occurs, the **Protection Status** shows as **Protected - (pending initial backup)**.</span></span> <span data-ttu-id="02365-196">По умолчанию *начальным резервным копированием*является первое запланированное резервное копирование.</span><span class="sxs-lookup"><span data-stu-id="02365-196">By default, the first scheduled backup is the *initial backup*.</span></span>

![Статус "В ожидании резервного копирования"](./media/backup-azure-vms-first-look/protection-pending-border.png)

<span data-ttu-id="02365-198">Чтобы запустить начальное резервное копирование, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="02365-198">To start the initial backup now:</span></span>

1. <span data-ttu-id="02365-199">В нижней части страницы **Защищенные элементы** щелкните **Архивировать**.</span><span class="sxs-lookup"><span data-stu-id="02365-199">On the **Protected Items** page, click **Backup Now** at the bottom of the page.</span></span>
    <span data-ttu-id="02365-200">![Элемент "Архивировать"](./media/backup-azure-vms-first-look/backup-now-icon.png)</span><span class="sxs-lookup"><span data-stu-id="02365-200">![Backup Now icon](./media/backup-azure-vms-first-look/backup-now-icon.png)</span></span>

    <span data-ttu-id="02365-201">Служба архивации Azure создаст задание резервного копирования для операции начального резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="02365-201">The Azure Backup service creates a backup job for the initial backup operation.</span></span>
2. <span data-ttu-id="02365-202">Чтобы просмотреть список заданий, щелкните вкладку **Задания** .</span><span class="sxs-lookup"><span data-stu-id="02365-202">Click the **Jobs** tab to view the list of jobs.</span></span>

    ![Выполняется резервное копирование](./media/backup-azure-vms-first-look/protect-inprogress.png)

    <span data-ttu-id="02365-204">Когда начальное резервное копирование будет завершено, на вкладке **Защищенные элементы** отобразится состояние виртуальной машины *Защищено*.</span><span class="sxs-lookup"><span data-stu-id="02365-204">When initial backup is complete, the status of the virtual machine in the **Protected Items** tab is *Protected*.</span></span>

    ![Резервное копирование виртуальной машины с точкой восстановления](./media/backup-azure-vms/protect-backedupvm.png)

   > [!NOTE]
   > <span data-ttu-id="02365-206">Резервное копирование виртуальных машин — локальный процесс.</span><span class="sxs-lookup"><span data-stu-id="02365-206">Backing up virtual machines is a local process.</span></span> <span data-ttu-id="02365-207">Создать резервную копию виртуальных машин из одного региона в хранилище службы архивации в другом регионе нельзя.</span><span class="sxs-lookup"><span data-stu-id="02365-207">You cannot back up virtual machines from one region to a backup vault in another region.</span></span> <span data-ttu-id="02365-208">Поэтому в каждом регионе Azure с виртуальными машинами, для которых требуется резервное копирование, необходимо создать как минимум одно хранилище службы архивации.</span><span class="sxs-lookup"><span data-stu-id="02365-208">So, for every Azure region that has VMs that need to be backed up, at least one backup vault must be created in that region.</span></span>
   >
   >

## <a name="next-steps"></a><span data-ttu-id="02365-209">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="02365-209">Next steps</span></span>
<span data-ttu-id="02365-210">Теперь, когда резервное копирование виртуальной машины успешно завершено, вы можете выполнить еще несколько действий.</span><span class="sxs-lookup"><span data-stu-id="02365-210">Now that you have successfully backed up a VM, there are several next steps that could be of interest.</span></span> <span data-ttu-id="02365-211">Логичнее всего будет ознакомиться с процессом восстановления данных на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="02365-211">The most logical step is to familiarize yourself with restoring data to a VM.</span></span> <span data-ttu-id="02365-212">Но есть задачи управления, которые помогут вам понять, как безопасно хранить данные и сократить расходы.</span><span class="sxs-lookup"><span data-stu-id="02365-212">However, there are management tasks that will help you understand how to keep your data safe and minimize costs.</span></span>

* [<span data-ttu-id="02365-213">Мониторинг виртуальных машин и управление ими</span><span class="sxs-lookup"><span data-stu-id="02365-213">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="02365-214">Восстановление виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="02365-214">Restore virtual machines</span></span>](backup-azure-restore-vms.md)
* [<span data-ttu-id="02365-215">Рекомендации по устранению неполадок</span><span class="sxs-lookup"><span data-stu-id="02365-215">Troubleshooting guidance</span></span>](backup-azure-vms-troubleshoot.md)

## <a name="questions"></a><span data-ttu-id="02365-216">Вопросы?</span><span class="sxs-lookup"><span data-stu-id="02365-216">Questions?</span></span>
<span data-ttu-id="02365-217">Если вы хотите задать вопрос или предложить добавить какие-либо функции, [отправьте нам свой отзыв](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="02365-217">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>
