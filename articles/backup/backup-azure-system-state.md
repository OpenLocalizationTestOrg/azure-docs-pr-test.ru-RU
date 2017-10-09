---
title: "aaaBack копирование tooAzure состояние системы Windows | Документы Microsoft"
description: "Узнайте, tooback копирование состояния системы hello Windows Server и/или tooAzure компьютеров Windows."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: carmonm
editor: 
keywords: "как toobackup; как tooback. резервное копирование файлов и папок"
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: saurse;markgal
ms.openlocfilehash: be5d4be81af981c10de82add9fe962a730753cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-windows-system-state-in-resource-manager-deployment"></a><span data-ttu-id="3080c-104">Резервное копирование состояния системы Windows с использованием модели развертывания Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3080c-104">Back up Windows system state in Resource Manager deployment</span></span>
<span data-ttu-id="3080c-105">В этой статье объясняется, как состояние tooAzure в tooback системы Windows Server.</span><span class="sxs-lookup"><span data-stu-id="3080c-105">This article explains how tooback up your Windows Server system state tooAzure.</span></span> <span data-ttu-id="3080c-106">Это учебник предполагаемого toowalk можно выполнить с помощью основы hello.</span><span class="sxs-lookup"><span data-stu-id="3080c-106">It's a tutorial intended toowalk you through hello basics.</span></span>

<span data-ttu-id="3080c-107">Дополнительные сведения об архивации Azure tooknow следует прочитать этот [Обзор](backup-introduction-to-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="3080c-107">If you want tooknow more about Azure Backup, read this [overview](backup-introduction-to-azure-backup.md).</span></span>

<span data-ttu-id="3080c-108">Если у вас нет подписки Azure, вы можете создать [бесплатную учетную запись](https://azure.microsoft.com/free/), предоставляющую доступ ко всем службам Azure.</span><span class="sxs-lookup"><span data-stu-id="3080c-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) that lets you access any Azure service.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="3080c-109">Создание хранилища служб восстановления</span><span class="sxs-lookup"><span data-stu-id="3080c-109">Create a recovery services vault</span></span>
<span data-ttu-id="3080c-110">tooback копирования файлов и папок необходимо toocreate хранилище служб восстановления в регионе hello место toostore hello данных.</span><span class="sxs-lookup"><span data-stu-id="3080c-110">tooback up your files and folders, you need toocreate a Recovery Services vault in hello region where you want toostore hello data.</span></span> <span data-ttu-id="3080c-111">Необходимо также toodetermine способ репликации хранилища.</span><span class="sxs-lookup"><span data-stu-id="3080c-111">You also need toodetermine how you want your storage replicated.</span></span>

### <a name="toocreate-a-recovery-services-vault"></a><span data-ttu-id="3080c-112">toocreate хранилище служб восстановления</span><span class="sxs-lookup"><span data-stu-id="3080c-112">toocreate a Recovery Services vault</span></span>
1. <span data-ttu-id="3080c-113">Если это еще не сделано, войдите в toohello [портала Azure](https://portal.azure.com/) с помощью вашей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="3080c-113">If you haven't already done so, sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="3080c-114">Hello концентратора меню **дополнительные службы** и введите в список ресурсов hello, **службы восстановления** и нажмите кнопку **хранилищ служб восстановления**.</span><span class="sxs-lookup"><span data-stu-id="3080c-114">On hello Hub menu, click **More services** and in hello list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Создание хранилища служб восстановления — шаг 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="3080c-116">Если в подписке hello хранилищами служб восстановления, перечисленных hello хранилищ.</span><span class="sxs-lookup"><span data-stu-id="3080c-116">If there are recovery services vaults in hello subscription, hello vaults are listed.</span></span>
3. <span data-ttu-id="3080c-117">На hello **хранилищ служб восстановления** меню, нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="3080c-117">On hello **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Создание хранилища служб восстановления — шаг 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="3080c-119">хранилище служб восстановления Hello открывает колонку приглашением tooprovide **имя**, **подписки**, **группы ресурсов**, и **расположение**.</span><span class="sxs-lookup"><span data-stu-id="3080c-119">hello Recovery Services vault blade opens, prompting you tooprovide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Создание хранилища служб восстановления — шаг 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="3080c-121">Для **имя**, введите понятное имя tooidentify hello хранилище.</span><span class="sxs-lookup"><span data-stu-id="3080c-121">For **Name**, enter a friendly name tooidentify hello vault.</span></span> <span data-ttu-id="3080c-122">Имя Hello должно toobe уникальным для hello подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="3080c-122">hello name needs toobe unique for hello Azure subscription.</span></span> <span data-ttu-id="3080c-123">Введите имя длиной от 2 до 50 знаков.</span><span class="sxs-lookup"><span data-stu-id="3080c-123">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="3080c-124">Имя должно начинаться с буквы, оно может содержать только буквы, цифры и дефисы.</span><span class="sxs-lookup"><span data-stu-id="3080c-124">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="3080c-125">В hello **подписки** используйте hello раскрывающееся меню toochoose hello подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="3080c-125">In hello **Subscription** section, use hello drop-down menu toochoose hello Azure subscription.</span></span> <span data-ttu-id="3080c-126">При использовании только одной подписке, появившемся подписки и toohello следующий шаг можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="3080c-126">If you use only one subscription, that subscription appears and you can skip toohello next step.</span></span> <span data-ttu-id="3080c-127">Если вы не уверены, какие toouse подписки, используется по умолчанию hello (или рекомендуемые) подписки.</span><span class="sxs-lookup"><span data-stu-id="3080c-127">If you are not sure which subscription toouse, use hello default (or suggested) subscription.</span></span> <span data-ttu-id="3080c-128">Вариантов будет несколько только в том случае, если учетная запись вашей организации связана с несколькими подписками Azure.</span><span class="sxs-lookup"><span data-stu-id="3080c-128">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="3080c-129">В hello **группы ресурсов** раздела:</span><span class="sxs-lookup"><span data-stu-id="3080c-129">In hello **Resource group** section:</span></span>

    * <span data-ttu-id="3080c-130">Выберите **создать новый** Если toocreate группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3080c-130">select **Create new** if you want toocreate a Resource group.</span></span>
    <span data-ttu-id="3080c-131">Или</span><span class="sxs-lookup"><span data-stu-id="3080c-131">Or</span></span>
    * <span data-ttu-id="3080c-132">Выберите **использовать существующие** и нажмите кнопку hello раскрывающееся меню toosee hello списка доступных групп ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3080c-132">select **Use existing** and click hello drop-down menu toosee hello available list of Resource groups.</span></span>

  <span data-ttu-id="3080c-133">Полные сведения для групп ресурсов см. в разделе hello [Обзор диспетчера ресурсов Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3080c-133">For complete information on Resource groups, see hello [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="3080c-134">Нажмите кнопку **расположение** tooselect hello географического региона для hello хранилища.</span><span class="sxs-lookup"><span data-stu-id="3080c-134">Click **Location** tooselect hello geographic region for hello vault.</span></span> <span data-ttu-id="3080c-135">Сделанный выбор определяет hello географическом регионе, куда отправлять данные резервной копии.</span><span class="sxs-lookup"><span data-stu-id="3080c-135">This choice determines hello geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="3080c-136">Hello нижней части колонки хранилище служб восстановления hello, нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="3080c-136">At hello bottom of hello Recovery Services vault blade, click **Create**.</span></span>

    <span data-ttu-id="3080c-137">Он может занять несколько минут для hello toobe создан в хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="3080c-137">It can take several minutes for hello Recovery Services vault toobe created.</span></span> <span data-ttu-id="3080c-138">Отслеживать уведомления о состоянии hello в верхней правой части hello hello портала.</span><span class="sxs-lookup"><span data-stu-id="3080c-138">Monitor hello status notifications in hello upper right-hand area of hello portal.</span></span> <span data-ttu-id="3080c-139">После создания своего хранилища, он отображается в списке hello хранилищами служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="3080c-139">Once your vault is created, it appears in hello list of Recovery Services vaults.</span></span> <span data-ttu-id="3080c-140">Если через несколько минут хранилище не отобразилось, нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="3080c-140">If after several minutes you don't see your vault, click **Refresh**.</span></span>

    ![Кнопка "Обновить"](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    <span data-ttu-id="3080c-142">Как только вы увидите ваше хранилище hello списка хранилищ служб восстановления, вы являетесь избыточности хранилища готов tooset hello.</span><span class="sxs-lookup"><span data-stu-id="3080c-142">Once you see your vault in hello list of Recovery Services vaults, you are ready tooset hello storage redundancy.</span></span>

### <a name="set-storage-redundancy-for-hello-vault"></a><span data-ttu-id="3080c-143">Значение избыточности хранилища для хранилища hello</span><span class="sxs-lookup"><span data-stu-id="3080c-143">Set storage redundancy for hello vault</span></span>
<span data-ttu-id="3080c-144">При создании хранилище служб восстановления, убедитесь, что избыточности хранилища является нужным образом настроенные hello.</span><span class="sxs-lookup"><span data-stu-id="3080c-144">When you create a Recovery Services vault, make sure storage redundancy is configured hello way you want.</span></span>

1. <span data-ttu-id="3080c-145">Из hello **хранилищ служб восстановления** колонка, щелкните новое хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="3080c-145">From hello **Recovery Services vaults** blade, click hello new vault.</span></span>

    ![Выберите новое хранилище hello hello списке хранилище служб восстановления](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="3080c-147">При выборе хранилища hello hello **хранилище служб восстановления** сужает колонки, а также колонку параметров hello (*имеющую hello имя хранилища hello вверху hello*) и откройте колонку сведения о хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="3080c-147">When you select hello vault, hello **Recovery Services vault** blade narrows, and hello Settings blade (*which has hello name of hello vault at hello top*) and hello vault details blade open.</span></span>

    ![Просмотр hello конфигурации хранилища для нового хранилища](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. <span data-ttu-id="3080c-149">В колонке параметров hello новое хранилище, используйте tooscroll вертикальной слайд hello вниз toohello управление раздел и нажмите кнопку **инфраструктуры резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="3080c-149">In hello new vault's Settings blade, use hello vertical slide tooscroll down toohello Manage section, and click **Backup Infrastructure**.</span></span>
    <span data-ttu-id="3080c-150">Открывает колонку Hello инфраструктуры резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="3080c-150">hello Backup Infrastructure blade opens.</span></span>
3. <span data-ttu-id="3080c-151">В колонке hello инфраструктуры резервного копирования, нажмите кнопку **конфигурация резервного копирования** tooopen hello **конфигурация резервного копирования** колонку.</span><span class="sxs-lookup"><span data-stu-id="3080c-151">In hello Backup Infrastructure blade, click **Backup Configuration** tooopen hello **Backup Configuration** blade.</span></span>

    ![Задание hello конфигурации хранилища для нового хранилища](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. <span data-ttu-id="3080c-153">Выберите параметр репликации соответствующих дисковых hello хранилища.</span><span class="sxs-lookup"><span data-stu-id="3080c-153">Choose hello appropriate storage replication option for your vault.</span></span>

    ![Варианты конфигурации хранилища](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    <span data-ttu-id="3080c-155">По умолчанию это геоизбыточное хранилище.</span><span class="sxs-lookup"><span data-stu-id="3080c-155">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="3080c-156">Если используется Azure в качестве конечной точки основного резервного хранилища, по-прежнему toouse **геоизбыточное**.</span><span class="sxs-lookup"><span data-stu-id="3080c-156">If you use Azure as a primary backup storage endpoint, continue toouse **Geo-redundant**.</span></span> <span data-ttu-id="3080c-157">Если вы не используете Azure как конечная точка основного хранилища резервной копии, выберите **локально избыточной**, что снижает затраты на хранилище Azure hello.</span><span class="sxs-lookup"><span data-stu-id="3080c-157">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces hello Azure storage costs.</span></span> <span data-ttu-id="3080c-158">Дополнительные сведения о [геоизбыточном](../storage/common/storage-redundancy.md#geo-redundant-storage) и [локально избыточном](../storage/common/storage-redundancy.md#locally-redundant-storage) хранилищах см. в статье [Репликация службы хранилища Azure](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="3080c-158">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="3080c-159">Теперь, когда вы создали хранилище, настройте в нем резервное копирование состояния системы Windows.</span><span class="sxs-lookup"><span data-stu-id="3080c-159">Now that you've created a vault, configure it for backing up Windows System State.</span></span>

## <a name="configure-hello-vault"></a><span data-ttu-id="3080c-160">Настройка хранилища hello</span><span class="sxs-lookup"><span data-stu-id="3080c-160">Configure hello vault</span></span>
1. <span data-ttu-id="3080c-161">На Здравствуйте колонку хранилище служб восстановления (для hello хранилища только что созданную), в разделе "Приступая к работе" hello, нажмите кнопку **резервного копирования**, то на hello **Приступая к резервному копированию** колонке выберите  **Цель резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="3080c-161">On hello Recovery Services vault blade (for hello vault you just created), in hello Getting Started section, click **Backup**, then on hello **Getting Started with Backup** blade, select **Backup goal**.</span></span>

    ![Открытая колонка цели резервного копирования](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    <span data-ttu-id="3080c-163">Hello **цель резервного копирования** открывает колонку.</span><span class="sxs-lookup"><span data-stu-id="3080c-163">hello **Backup Goal** blade opens.</span></span>

    ![Открытая колонка цели резервного копирования](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="3080c-165">Из hello **где выполняется рабочая нагрузка?** раскрывающееся меню, выберите **локальной**.</span><span class="sxs-lookup"><span data-stu-id="3080c-165">From hello **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

    <span data-ttu-id="3080c-166">Вы выбираете параметр **Локально**, потому что ваш компьютер Windows Server или Windows — это физический компьютер, которые не находится в Azure.</span><span class="sxs-lookup"><span data-stu-id="3080c-166">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="3080c-167">Из hello **что вам требуется toobackup?** последовательно выберите пункты **состояния системы**и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="3080c-167">From hello **What do you want toobackup?** menu, select **System State**, and click **OK**.</span></span>

    ![Настройка резервного копирования файлов и папок](./media/backup-azure-system-state/backup-goal-system-state.png)

    <span data-ttu-id="3080c-169">После нажатия кнопки ОК, устанавливается флажок Далее слишком**цель резервного копирования**и hello **подготовки инфраструктуры** открывает колонку.</span><span class="sxs-lookup"><span data-stu-id="3080c-169">After clicking OK, a checkmark appears next too**Backup goal**, and hello **Prepare infrastructure** blade opens.</span></span>

    ![Цель резервного копирования настроена, на очереди подготовка инфраструктуры](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="3080c-171">На hello **подготовки инфраструктуры** колонка, щелкните **загрузить агент для Windows Server или Windows Client**.</span><span class="sxs-lookup"><span data-stu-id="3080c-171">On hello **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

    ![Download Agent for Windows Server or Windows Client](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    <span data-ttu-id="3080c-173">Если вы используете Windows Server необходимо, выберите toodownload hello агент для Windows Server Essential.</span><span class="sxs-lookup"><span data-stu-id="3080c-173">If you are using Windows Server Essential, then choose toodownload hello agent for Windows Server Essential.</span></span> <span data-ttu-id="3080c-174">Во всплывающем меню предложит toorun или сохранить MARSAgentInstaller.exe.</span><span class="sxs-lookup"><span data-stu-id="3080c-174">A pop-up menu prompts you toorun or save MARSAgentInstaller.exe.</span></span>

    ![Диалоговое окно MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="3080c-176">Во всплывающем меню загрузки приветствия щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3080c-176">In hello download pop-up menu, click **Save**.</span></span>

    <span data-ttu-id="3080c-177">По умолчанию hello **MARSagentinstaller.exe** файл сохраняется в папке загрузки tooyour.</span><span class="sxs-lookup"><span data-stu-id="3080c-177">By default, hello **MARSagentinstaller.exe** file is saved tooyour Downloads folder.</span></span> <span data-ttu-id="3080c-178">После завершения работы установщика hello появится всплывающее окно запросом установщиком toorun hello, или откройте папку hello.</span><span class="sxs-lookup"><span data-stu-id="3080c-178">When hello installer completes, you will see a pop-up asking if you want toorun hello installer, or open hello folder.</span></span>

    ![Download Agent for Windows Server or Windows Client](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    <span data-ttu-id="3080c-180">Tooinstall hello агент еще не требуется.</span><span class="sxs-lookup"><span data-stu-id="3080c-180">You don't need tooinstall hello agent yet.</span></span> <span data-ttu-id="3080c-181">Hello агент можно установить после загрузки hello учетные данные хранилища.</span><span class="sxs-lookup"><span data-stu-id="3080c-181">You can install hello agent after you have downloaded hello vault credentials.</span></span>

6. <span data-ttu-id="3080c-182">На hello **подготовки инфраструктуры** колонка, щелкните **загрузить**.</span><span class="sxs-lookup"><span data-stu-id="3080c-182">On hello **Prepare infrastructure** blade, click **Download**.</span></span>

    ![Скачивание учетных данных хранилища](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    <span data-ttu-id="3080c-184">Папка загрузки tooyour загрузки Hello учетные данные хранилища.</span><span class="sxs-lookup"><span data-stu-id="3080c-184">hello vault credentials download tooyour Downloads folder.</span></span> <span data-ttu-id="3080c-185">После завершения загрузки учетные данные хранилища hello появиться всплывающее окно запроса, если хотите tooopen или сохранить учетные данные hello.</span><span class="sxs-lookup"><span data-stu-id="3080c-185">After hello vault credentials finish downloading, you see a pop-up asking if you want tooopen or save hello credentials.</span></span> <span data-ttu-id="3080c-186">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3080c-186">Click **Save**.</span></span> <span data-ttu-id="3080c-187">Если вы случайно щелкнете **откройте**, позволяют hello диалоговое окно, которое пытается tooopen учетные данные хранилища hello, не.</span><span class="sxs-lookup"><span data-stu-id="3080c-187">If you accidentally click **Open**, let hello dialog that attempts tooopen hello vault credentials, fail.</span></span> <span data-ttu-id="3080c-188">Не удается открыть hello учетные данные хранилища.</span><span class="sxs-lookup"><span data-stu-id="3080c-188">You cannot open hello vault credentials.</span></span> <span data-ttu-id="3080c-189">Продолжить toohello следующий шаг.</span><span class="sxs-lookup"><span data-stu-id="3080c-189">Proceed toohello next step.</span></span> <span data-ttu-id="3080c-190">учетные данные хранилища Hello находятся в папке загрузки hello.</span><span class="sxs-lookup"><span data-stu-id="3080c-190">hello vault credentials are in hello Downloads folder.</span></span>   

    ![Загрузка учетных данных хранилища завершена](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a><span data-ttu-id="3080c-192">Установка и регистрация агента hello</span><span class="sxs-lookup"><span data-stu-id="3080c-192">Install and register hello agent</span></span>

> [!NOTE]
> <span data-ttu-id="3080c-193">Включение резервного копирования с использованием hello портал Azure, пока недоступно.</span><span class="sxs-lookup"><span data-stu-id="3080c-193">Enabling backup through hello Azure portal is not available, yet.</span></span> <span data-ttu-id="3080c-194">Используйте агент служб восстановления Microsoft Azure tooback hello копирование состояния системы Windows Server.</span><span class="sxs-lookup"><span data-stu-id="3080c-194">Use hello Microsoft Azure Recovery Services Agent tooback up Windows Server System State.</span></span>
>

1. <span data-ttu-id="3080c-195">Найдите и дважды щелкните hello **MARSagentinstaller.exe** из hello загрузки (или другие сохраненного расположения).</span><span class="sxs-lookup"><span data-stu-id="3080c-195">Locate and double-click hello **MARSagentinstaller.exe** from hello Downloads folder (or other saved location).</span></span>

    <span data-ttu-id="3080c-196">Установщик Hello предоставляет ряд сообщений извлечения, устанавливает и регистрирует агент служб восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="3080c-196">hello installer provides a series of messages as it extracts, installs, and registers hello Recovery Services agent.</span></span>

    ![Запуск установщика агента служб восстановления](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="3080c-198">Завершите мастер установки агента служб восстановления Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="3080c-198">Complete hello Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="3080c-199">Мастер toocomplete hello, необходимо:</span><span class="sxs-lookup"><span data-stu-id="3080c-199">toocomplete hello wizard, you need to:</span></span>

   * <span data-ttu-id="3080c-200">Выберите расположение для папки установки и кэша hello.</span><span class="sxs-lookup"><span data-stu-id="3080c-200">Choose a location for hello installation and cache folder.</span></span>
   * <span data-ttu-id="3080c-201">Укажите прокси-сведений о сервере, если вы используете toohello tooconnect сервера прокси-сервера Интернета.</span><span class="sxs-lookup"><span data-stu-id="3080c-201">Provide your proxy server info if you use a proxy server tooconnect toohello internet.</span></span>
   * <span data-ttu-id="3080c-202">Если используется прокси-сервер, прошедший проверку подлинности, ввести имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="3080c-202">Provide your user name and password details if you use an authenticated proxy.</span></span>
   * <span data-ttu-id="3080c-203">Укажите учетные данные хранилища загружаются hello</span><span class="sxs-lookup"><span data-stu-id="3080c-203">Provide hello downloaded vault credentials</span></span>
   * <span data-ttu-id="3080c-204">Сохраните парольную фразу для шифрования hello в безопасном месте.</span><span class="sxs-lookup"><span data-stu-id="3080c-204">Save hello encryption passphrase in a secure location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="3080c-205">При потере или забудете парольную фразу hello, корпорация Майкрософт не может выполнить восстановление резервной копии данных hello.</span><span class="sxs-lookup"><span data-stu-id="3080c-205">If you lose or forget hello passphrase, Microsoft cannot help recover hello backup data.</span></span> <span data-ttu-id="3080c-206">Сохраните файл hello в безопасном месте.</span><span class="sxs-lookup"><span data-stu-id="3080c-206">Save hello file in a secure location.</span></span> <span data-ttu-id="3080c-207">Это обязательный toorestore резервной копии.</span><span class="sxs-lookup"><span data-stu-id="3080c-207">It is required toorestore a backup.</span></span>
     >
     >

<span data-ttu-id="3080c-208">Hello агент установлен, и ваш компьютер входит в хранилище зарегистрированного toohello.</span><span class="sxs-lookup"><span data-stu-id="3080c-208">hello agent is now installed and your machine is registered toohello vault.</span></span> <span data-ttu-id="3080c-209">Вы будете готовы tooconfigure и расписания резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="3080c-209">You're ready tooconfigure and schedule your backup.</span></span>

## <a name="back-up-windows-server-system-state-preview"></a><span data-ttu-id="3080c-210">Состояние резервного копирования системы Windows Server (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="3080c-210">Back up Windows Server System State (Preview)</span></span>
<span data-ttu-id="3080c-211">Hello начальной резервной копии содержит три задачи:</span><span class="sxs-lookup"><span data-stu-id="3080c-211">hello initial backup includes three tasks:</span></span>

* <span data-ttu-id="3080c-212">Включить архивацию состояния системы с помощью агента Azure Backup hello</span><span class="sxs-lookup"><span data-stu-id="3080c-212">Enable System State Backup using hello Azure Backup agent</span></span>
* <span data-ttu-id="3080c-213">Планирование резервного копирования hello</span><span class="sxs-lookup"><span data-stu-id="3080c-213">Schedule hello backup</span></span>
* <span data-ttu-id="3080c-214">Резервное копирование файлов и папок для hello первый раз</span><span class="sxs-lookup"><span data-stu-id="3080c-214">Back up files and folders for hello first time</span></span>

<span data-ttu-id="3080c-215">toocomplete hello начальной резервной копии, используйте агент служб восстановления Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="3080c-215">toocomplete hello initial backup, use hello Microsoft Azure Recovery Services agent.</span></span>

### <a name="tooenable-system-state-backup-using-hello-azure-backup-agent"></a><span data-ttu-id="3080c-216">tooenable резервной копии состояния системы с помощью агента резервного копирования Azure hello</span><span class="sxs-lookup"><span data-stu-id="3080c-216">tooenable System State backup using hello Azure Backup agent</span></span>

1. <span data-ttu-id="3080c-217">В сеансе PowerShell запустите hello, следующая команда toostop hello Azure Backup ядра.</span><span class="sxs-lookup"><span data-stu-id="3080c-217">In a PowerShell session, run hello following command toostop hello Azure Backup engine.</span></span>

  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="3080c-218">Откройте реестр Windows hello.</span><span class="sxs-lookup"><span data-stu-id="3080c-218">Open hello Windows Registry.</span></span>

  ```
  PS C:\> regedit.exe
  ```

3. <span data-ttu-id="3080c-219">Добавьте следующий раздел реестра hello hello указано значение DWord.</span><span class="sxs-lookup"><span data-stu-id="3080c-219">Add hello following registry key with hello specified DWord Value.</span></span>

  | <span data-ttu-id="3080c-220">Путь к элементу реестра</span><span class="sxs-lookup"><span data-stu-id="3080c-220">Registry path</span></span> | <span data-ttu-id="3080c-221">Раздел реестра</span><span class="sxs-lookup"><span data-stu-id="3080c-221">Registry key</span></span> | <span data-ttu-id="3080c-222">Значение DWORD</span><span class="sxs-lookup"><span data-stu-id="3080c-222">DWord value</span></span> |
  |---------------|--------------|-------------|
  | <span data-ttu-id="3080c-223">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span><span class="sxs-lookup"><span data-stu-id="3080c-223">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span></span> | <span data-ttu-id="3080c-224">TurnOffSSBFeature</span><span class="sxs-lookup"><span data-stu-id="3080c-224">TurnOffSSBFeature</span></span> | <span data-ttu-id="3080c-225">2</span><span class="sxs-lookup"><span data-stu-id="3080c-225">2</span></span> |

4. <span data-ttu-id="3080c-226">Перезапустите engine hello резервной копии, выполнив следующую команду в командную строку hello.</span><span class="sxs-lookup"><span data-stu-id="3080c-226">Restart hello Backup engine by executing hello following command in an elevated command prompt.</span></span>

  ```
  PS C:\> Net start obengine
  ```

### <a name="tooschedule-hello-backup-job"></a><span data-ttu-id="3080c-227">задание резервного копирования tooschedule hello</span><span class="sxs-lookup"><span data-stu-id="3080c-227">tooschedule hello backup job</span></span>

1. <span data-ttu-id="3080c-228">Откройте hello агента служб восстановления Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3080c-228">Open hello Microsoft Azure Recovery Services agent.</span></span> <span data-ttu-id="3080c-229">Его можно найти, выполнив поиск строки **служба архивации Microsoft Azure**на компьютере.</span><span class="sxs-lookup"><span data-stu-id="3080c-229">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Запустите агент служб восстановления Azure hello](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)

2. <span data-ttu-id="3080c-231">Агент служб восстановления hello, щелкните **планирования резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="3080c-231">In hello Recovery Services agent, click **Schedule Backup**.</span></span>

    ![Планирование архивации Windows Server](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)

3. <span data-ttu-id="3080c-233">На hello Приступая к работе страница приветствия мастера планирования резервного копирования, нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3080c-233">On hello Getting started page of hello Schedule Backup Wizard, click **Next**.</span></span>

4. <span data-ttu-id="3080c-234">На странице выбора элементов tooBackup hello щелкните **добавить элементы**.</span><span class="sxs-lookup"><span data-stu-id="3080c-234">On hello Select Items tooBackup page, click **Add Items**.</span></span>

5. <span data-ttu-id="3080c-235">Выберите **Состояние системы** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="3080c-235">Select **System State** and then click **OK**.</span></span>

6. <span data-ttu-id="3080c-236">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3080c-236">Click **Next**.</span></span>

7. <span data-ttu-id="3080c-237">Hello расписание резервного копирования состояния системы и хранения автоматически устанавливается tooback копирование каждое воскресенье в 9:00 по местному времени, и задать срок хранения hello too60 дней.</span><span class="sxs-lookup"><span data-stu-id="3080c-237">hello System State Backup and Retention schedule is automatically set tooback up every Sunday at 9:00 PM local time, and hello retention period is set too60 days.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3080c-238">Политики резервного копирования и хранения состояния системы настраиваются автоматически.</span><span class="sxs-lookup"><span data-stu-id="3080c-238">System State backup and retention policy is automatically configured.</span></span> <span data-ttu-id="3080c-239">При создании резервной копии файлов и папок, кроме состояния системы toohello Windows Server, укажите только hello архивации и политику хранения для резервных копий файлов с помощью мастера hello.</span><span class="sxs-lookup"><span data-stu-id="3080c-239">If you back up Files and Folders in addition toohello Windows Server System State, specify only hello Backup and Retention policy for file backups from hello wizard.</span></span> 
   >

8. <span data-ttu-id="3080c-240">На странице подтверждения hello, просмотрите сведения hello и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="3080c-240">On hello Confirmation page, review hello information, and then click **Finish**.</span></span>

9. <span data-ttu-id="3080c-241">После завершения работы мастера hello, создания расписания резервного копирования hello, нажмите кнопку **закрыть**.</span><span class="sxs-lookup"><span data-stu-id="3080c-241">After hello wizard finishes creating hello backup schedule, click **Close**.</span></span>

### <a name="tooback-up-windows-server-system-state-for-hello-first-time"></a><span data-ttu-id="3080c-242">tooback копирование состояния системы Windows Server для hello первый раз</span><span class="sxs-lookup"><span data-stu-id="3080c-242">tooback up Windows Server System State for hello first time</span></span>

1. <span data-ttu-id="3080c-243">Убедитесь, что для Windows Server нет незавершенных обновлений, которые требуют перезагрузки.</span><span class="sxs-lookup"><span data-stu-id="3080c-243">Make sure there are no pending updates for Windows Server that require a reboot.</span></span>

2. <span data-ttu-id="3080c-244">Агент служб восстановления hello, щелкните **Архивировать** toocomplete hello начального заполнения hello сети.</span><span class="sxs-lookup"><span data-stu-id="3080c-244">In hello Recovery Services agent, click **Back Up Now** toocomplete hello initial seeding over hello network.</span></span>

    ![Моментальная архивация Windows Server](./media/backup-try-azure-backup-in-10-mins/backup-now.png)

3. <span data-ttu-id="3080c-246">На странице подтверждения hello просмотрите параметры hello hello мастер немедленной архивации будет использовать tooback машину hello.</span><span class="sxs-lookup"><span data-stu-id="3080c-246">On hello Confirmation page, review hello settings that hello Back Up Now Wizard will use tooback up hello machine.</span></span> <span data-ttu-id="3080c-247">Затем нажмите кнопку **Архивировать**.</span><span class="sxs-lookup"><span data-stu-id="3080c-247">Then click **Back Up**.</span></span>

4. <span data-ttu-id="3080c-248">Нажмите кнопку **закрыть** tooclose приветствия мастера.</span><span class="sxs-lookup"><span data-stu-id="3080c-248">Click **Close** tooclose hello wizard.</span></span> <span data-ttu-id="3080c-249">Если вы закроете мастер hello до завершения процесса резервного копирования hello, мастер hello переходит toorun в фоновом режиме hello.</span><span class="sxs-lookup"><span data-stu-id="3080c-249">If you close hello wizard before hello backup process finishes, hello wizard continues toorun in hello background.</span></span>

5. <span data-ttu-id="3080c-250">Если резервное копирование файлов и папок на сервере, кроме состояния системы toohello Windows Server, приветствия мастера создать резервную копию только выполнит резервное копирование файлов.</span><span class="sxs-lookup"><span data-stu-id="3080c-250">If you back up Files and Folders on your server, in addition toohello Windows Server System State, hello Backup Now wizard will only back up files.</span></span> <span data-ttu-id="3080c-251">tooperform нерегламентированной состояния системы резервного копирования, выполните следующую команду PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="3080c-251">tooperform an ad hoc System State back up, use hello following PowerShell command:</span></span>

    ```
    PS C:\> Start-OBSystemStateBackup
    ```

  <span data-ttu-id="3080c-252">После завершения начальной резервной копии hello hello **задание завершено** состояние отображается в консоли hello резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="3080c-252">After hello initial backup is completed, hello **Job completed** status appears in hello Backup console.</span></span>

  ![Первоначальное восстановление завершено](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="frequently-asked-questions"></a><span data-ttu-id="3080c-254">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="3080c-254">Frequently asked questions</span></span>

<span data-ttu-id="3080c-255">Hello следующие вопросы и ответы предоставляют дополнительную информацию.</span><span class="sxs-lookup"><span data-stu-id="3080c-255">hello following questions and answers provide supplementary information.</span></span>

### <a name="what-is-hello-staging-volume"></a><span data-ttu-id="3080c-256">Что такое hello промежуточной тома?</span><span class="sxs-lookup"><span data-stu-id="3080c-256">What is hello Staging Volume?</span></span>

<span data-ttu-id="3080c-257">Hello тома промежуточной представляет hello промежуточного расположения, где изначально доступна hello архивации данных Windows Server готовит hello резервной копии состояния системы.</span><span class="sxs-lookup"><span data-stu-id="3080c-257">hello Staging Volume represents hello intermediate location where hello natively available, Windows Server Backup stages hello System State Backup.</span></span> <span data-ttu-id="3080c-258">Azure Backup agent затем сжимает и шифрует этот промежуточный резервного копирования и отправляет его через безопасный протокол HTTPS toohello настроить хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="3080c-258">Azure Backup agent then compresses and encrypts this intermediate backup and sends it via secure HTTPS Protocol toohello configured Recovery Services Vault.</span></span> <span data-ttu-id="3080c-259">**Настоятельно рекомендуется установить hello промежуточной тома на томе Windows ОС. Если вы заметили проблемы с резервных копий состояния системы, проверка hello расположение промежуточной тома является первым шагом по устранению неполадок hello.**</span><span class="sxs-lookup"><span data-stu-id="3080c-259">**We strongly recommended you establish hello Staging Volume in a non-Windows-OS volume. If you observe problems with System State Backups, checking hello location of your Staging Volume is hello first troubleshooting step.**</span></span> 

### <a name="how-can-i-change-hello-staging-volume-path-specified-in-hello-azure-backup-agent"></a><span data-ttu-id="3080c-260">Как изменить hello промежуточной тома путь, указанный в hello Azure Backup agent?</span><span class="sxs-lookup"><span data-stu-id="3080c-260">How can I change hello Staging Volume Path specified in hello Azure Backup agent?</span></span>

<span data-ttu-id="3080c-261">Hello промежуточной тома по умолчанию расположен в папке кэша hello.</span><span class="sxs-lookup"><span data-stu-id="3080c-261">hello Staging Volume is located in hello cache folder by default.</span></span> 

1. <span data-ttu-id="3080c-262">toochange это расположение hello используйте следующую команду (в командную строку):</span><span class="sxs-lookup"><span data-stu-id="3080c-262">toochange this location, use hello following command (in an elevated command prompt):</span></span>
  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="3080c-263">Затем обновите hello следующих параметров реестра hello путь toohello новой тома промежуточной папке.</span><span class="sxs-lookup"><span data-stu-id="3080c-263">Then update hello following registry entries with hello path toohello new Staging Volume folder.</span></span>

  |<span data-ttu-id="3080c-264">Путь к элементу реестра</span><span class="sxs-lookup"><span data-stu-id="3080c-264">Registry path</span></span>|<span data-ttu-id="3080c-265">Раздел реестра</span><span class="sxs-lookup"><span data-stu-id="3080c-265">Registry key</span></span>|<span data-ttu-id="3080c-266">Значение</span><span class="sxs-lookup"><span data-stu-id="3080c-266">Value</span></span>|
  |-------------|------------|-----|
  |<span data-ttu-id="3080c-267">HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span><span class="sxs-lookup"><span data-stu-id="3080c-267">HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span></span> | <span data-ttu-id="3080c-268">SSBStagingPath</span><span class="sxs-lookup"><span data-stu-id="3080c-268">SSBStagingPath</span></span> | <span data-ttu-id="3080c-269">новое расположение промежуточного тома</span><span class="sxs-lookup"><span data-stu-id="3080c-269">new staging volume location</span></span> |

<span data-ttu-id="3080c-270">Hello путь размещения чувствительно к регистру и должны быть точно один регистр hello как то, что существует на сервере hello.</span><span class="sxs-lookup"><span data-stu-id="3080c-270">hello Staging Path is case sensitive and must be hello exact same casing as what exists on hello server.</span></span> 

3. <span data-ttu-id="3080c-271">После преобразования путь тома промежуточной hello перезапустите engine hello резервного копирования:</span><span class="sxs-lookup"><span data-stu-id="3080c-271">Once you change hello Staging volume path, restart hello Backup engine:</span></span>
  ```
  PS C:\> Net start obengine
  ```
4. <span data-ttu-id="3080c-272">toopick hello изменить путь, откройте hello агента служб восстановления Microsoft Azure и триггер Нерегламентированное резервное копирование состояния системы.</span><span class="sxs-lookup"><span data-stu-id="3080c-272">toopick up hello changed path, open hello Microsoft Azure Recovery Services agent and trigger an ad hoc backup of System State.</span></span>

### <a name="why-is-hello-system-state-default-retention-set-too60-days"></a><span data-ttu-id="3080c-273">Почему необходимо hello состояния системы, срок хранения по умолчанию значение too60 дней?</span><span class="sxs-lookup"><span data-stu-id="3080c-273">Why is hello System State default retention set too60 days?</span></span>

<span data-ttu-id="3080c-274">Hello полезного использования резервной копии состояния системы является hello то же, что параметр hello «время жизни захоронения» для роли Windows Server Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="3080c-274">hello useful life of a system state backup is hello same as hello "tombstone lifetime" setting for hello Windows Server Active Directory role.</span></span> <span data-ttu-id="3080c-275">значение по умолчанию Hello для записи времени жизни захоронения hello — 60 дней.</span><span class="sxs-lookup"><span data-stu-id="3080c-275">hello default value for hello tombstone lifetime entry is 60 days.</span></span> <span data-ttu-id="3080c-276">Это значение может быть задано на hello объекта конфигурации службы каталогов (NTDS).</span><span class="sxs-lookup"><span data-stu-id="3080c-276">This value can be set on hello Directory Service (NTDS) config object.</span></span>

### <a name="how-do-i-change-hello-default-backup-and-retention-policy-for-system-state"></a><span data-ttu-id="3080c-277">Как изменить по умолчанию hello архивации и политику хранения для состояния системы?</span><span class="sxs-lookup"><span data-stu-id="3080c-277">How do I change hello default Backup and Retention Policy for System State?</span></span>

<span data-ttu-id="3080c-278">по умолчанию hello toochange архивации и политику хранения для состояния системы:</span><span class="sxs-lookup"><span data-stu-id="3080c-278">toochange hello default Backup and Retention Policy for System State:</span></span>
1. <span data-ttu-id="3080c-279">Остановка резервного копирования подсистемы hello.</span><span class="sxs-lookup"><span data-stu-id="3080c-279">Stop hello Backup engine.</span></span> <span data-ttu-id="3080c-280">Выполните следующую команду из командной строки с повышенными привилегиями hello.</span><span class="sxs-lookup"><span data-stu-id="3080c-280">Run hello following command from an elevated command prompt.</span></span>

  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="3080c-281">Добавление или обновление следующих параметров реестра ключа в Azure Backup\Config\CloudBackupProvider параметру hello.</span><span class="sxs-lookup"><span data-stu-id="3080c-281">Add or update hello following registry key entries in HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider.</span></span>

  |<span data-ttu-id="3080c-282">Имя реестра</span><span class="sxs-lookup"><span data-stu-id="3080c-282">Registry Name</span></span>|<span data-ttu-id="3080c-283">Описание</span><span class="sxs-lookup"><span data-stu-id="3080c-283">Description</span></span>|<span data-ttu-id="3080c-284">Значение</span><span class="sxs-lookup"><span data-stu-id="3080c-284">Value</span></span>|
  |-------------|-----------|-----|
  |<span data-ttu-id="3080c-285">SSBScheduleTime</span><span class="sxs-lookup"><span data-stu-id="3080c-285">SSBScheduleTime</span></span>|<span data-ttu-id="3080c-286">Использовать время hello tooconfigure hello резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="3080c-286">Used tooconfigure hello time of hello backup.</span></span> <span data-ttu-id="3080c-287">Значение по умолчанию — 21:00 по местному времени.</span><span class="sxs-lookup"><span data-stu-id="3080c-287">Default is 9PM local time.</span></span>|<span data-ttu-id="3080c-288">DWORD: формат ЧЧММ (десятичное число), например 2130 для 21:30 по местному времени.</span><span class="sxs-lookup"><span data-stu-id="3080c-288">DWord: Format HHMM (Decimal) for example 2130 for 9:30PM local time</span></span>|
  |<span data-ttu-id="3080c-289">SSBScheduleDays</span><span class="sxs-lookup"><span data-stu-id="3080c-289">SSBScheduleDays</span></span>|<span data-ttu-id="3080c-290">Используется tooconfigure hello дни, когда резервная копия состояния системы должна быть выполнена в hello указывать время.</span><span class="sxs-lookup"><span data-stu-id="3080c-290">Used tooconfigure hello days when System State Backup must be performed at hello specified time.</span></span> <span data-ttu-id="3080c-291">Отдельные цифр укажите дни недели hello.</span><span class="sxs-lookup"><span data-stu-id="3080c-291">Individual digits specify days of hello week.</span></span> <span data-ttu-id="3080c-292">0 означает воскресенье, 1 — понедельник и т. д.</span><span class="sxs-lookup"><span data-stu-id="3080c-292">0 represents Sunday, 1 is Monday, and so on.</span></span> <span data-ttu-id="3080c-293">Стандартным днем для резервного копирования является воскресенье.</span><span class="sxs-lookup"><span data-stu-id="3080c-293">Default day for backup is Sunday.</span></span>|<span data-ttu-id="3080c-294">DWord: дни hello недели toorun резервного копирования (десятичное), например 1230 планирует резервное копирование в понедельник, Вторник, среда и воскресенье.</span><span class="sxs-lookup"><span data-stu-id="3080c-294">DWord: days of hello week toorun backup (decimal) for example 1230 schedules backups on Monday, Tuesday, Wednesday, and Sunday.</span></span>|
  |<span data-ttu-id="3080c-295">SSBRetentionDays</span><span class="sxs-lookup"><span data-stu-id="3080c-295">SSBRetentionDays</span></span>|<span data-ttu-id="3080c-296">Резервное копирование tooretain дней hello используется tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="3080c-296">Used tooconfigure hello days tooretain backup.</span></span> <span data-ttu-id="3080c-297">Значение по умолчанию — 60.</span><span class="sxs-lookup"><span data-stu-id="3080c-297">Default value is 60.</span></span> <span data-ttu-id="3080c-298">Допустимое значение не должно превышать 180.</span><span class="sxs-lookup"><span data-stu-id="3080c-298">Maximum allowed value is 180.</span></span>|<span data-ttu-id="3080c-299">DWord: Дни tooretain резервного копирования (десятичное значение).</span><span class="sxs-lookup"><span data-stu-id="3080c-299">DWord: Days tooretain backup (decimal).</span></span>|

3. <span data-ttu-id="3080c-300">Используйте hello следующая команда модуля архивации toorestart hello.</span><span class="sxs-lookup"><span data-stu-id="3080c-300">Use hello following command toorestart hello backup engine.</span></span>
    ```
    PS C:\> Net start obengine
    ```

4. <span data-ttu-id="3080c-301">Откройте агент служб восстановления Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="3080c-301">Open hello Microsoft Recovery Services agent.</span></span>

5. <span data-ttu-id="3080c-302">Нажмите кнопку **планирования резервного копирования** и нажмите кнопку **Далее** пока не увидите изменившиеся hello.</span><span class="sxs-lookup"><span data-stu-id="3080c-302">Click **Schedule Backup** and then click **Next** until you see hello changes reflected.</span></span>

6. <span data-ttu-id="3080c-303">Нажмите кнопку **Готово** tooapply hello изменения.</span><span class="sxs-lookup"><span data-stu-id="3080c-303">Click **Finish** tooapply hello changes.</span></span>


## <a name="questions"></a><span data-ttu-id="3080c-304">Вопросы?</span><span class="sxs-lookup"><span data-stu-id="3080c-304">Questions?</span></span>
<span data-ttu-id="3080c-305">Если у вас есть вопросы или при наличии любой возможности, хотелось бы включены, toosee [отправить отзыв](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="3080c-305">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3080c-306">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3080c-306">Next steps</span></span>
* <span data-ttu-id="3080c-307">См. дополнительные сведения об [архивации компьютеров Windows](backup-configure-vault.md).</span><span class="sxs-lookup"><span data-stu-id="3080c-307">Get more details about [backing up Windows machines](backup-configure-vault.md).</span></span>
* <span data-ttu-id="3080c-308">Теперь, когда вы выполнили резервное копирование файлов и папок, вы можете [управлять хранилищами и серверами](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="3080c-308">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="3080c-309">Если вам требуется toorestore резервной копии, используйте в этой статье слишком[восстановить компьютер Windows tooa файлы](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="3080c-309">If you need toorestore a backup, use this article too[restore files tooa Windows machine](backup-azure-restore-windows-server.md).</span></span>
