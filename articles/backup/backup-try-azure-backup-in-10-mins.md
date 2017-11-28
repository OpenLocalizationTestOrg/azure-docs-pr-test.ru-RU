---
title: "aaaBack копии Windows файлы и папки tooAzure (диспетчера ресурсов) | Документы Microsoft"
description: "Узнайте, tooback копии Windows tooAzure файлов и папок в развертывании диспетчера ресурсов."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "как toobackup; как tooback. резервное копирование файлов и папок"
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 8/15/2017
ms.author: markgal;
ms.openlocfilehash: 07d6580a84d5092ed2c61bf86ff5fcb148423ef2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="first-look-back-up-files-and-folders-in-resource-manager-deployment"></a><span data-ttu-id="ec246-104">Первое знакомство. Резервное копирование файлов и папок с использованием модели развертывания с помощью Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ec246-104">First look: back up files and folders in Resource Manager deployment</span></span>
<span data-ttu-id="ec246-105">В этой статье объясняется, как tooback Windows Server (или компьютере Windows) файлов и папок tooAzure, с помощью развертывания диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ec246-105">This article explains how tooback up your Windows Server (or Windows computer) files and folders tooAzure using a Resource Manager deployment.</span></span> <span data-ttu-id="ec246-106">Это учебник предполагаемого toowalk можно выполнить с помощью основы hello.</span><span class="sxs-lookup"><span data-stu-id="ec246-106">It's a tutorial intended toowalk you through hello basics.</span></span> <span data-ttu-id="ec246-107">Если требуется tooget к работе с Azure Backup, вы в нужном месте hello.</span><span class="sxs-lookup"><span data-stu-id="ec246-107">If you want tooget started using Azure Backup, you're in hello right place.</span></span>

<span data-ttu-id="ec246-108">Дополнительные сведения об архивации Azure tooknow следует прочитать этот [Обзор](backup-introduction-to-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="ec246-108">If you want tooknow more about Azure Backup, read this [overview](backup-introduction-to-azure-backup.md).</span></span>

<span data-ttu-id="ec246-109">Если у вас нет подписки Azure, вы можете создать [бесплатную учетную запись](https://azure.microsoft.com/free/), предоставляющую доступ ко всем службам Azure.</span><span class="sxs-lookup"><span data-stu-id="ec246-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) that lets you access any Azure service.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="ec246-110">Создание хранилища служб восстановления</span><span class="sxs-lookup"><span data-stu-id="ec246-110">Create a recovery services vault</span></span>
<span data-ttu-id="ec246-111">tooback копирования файлов и папок необходимо toocreate хранилище служб восстановления в регионе hello место toostore hello данных.</span><span class="sxs-lookup"><span data-stu-id="ec246-111">tooback up your files and folders, you need toocreate a Recovery Services vault in hello region where you want toostore hello data.</span></span> <span data-ttu-id="ec246-112">Необходимо также toodetermine способ репликации хранилища.</span><span class="sxs-lookup"><span data-stu-id="ec246-112">You also need toodetermine how you want your storage replicated.</span></span>

### <a name="toocreate-a-recovery-services-vault"></a><span data-ttu-id="ec246-113">toocreate хранилище служб восстановления</span><span class="sxs-lookup"><span data-stu-id="ec246-113">toocreate a Recovery Services vault</span></span>
1. <span data-ttu-id="ec246-114">Если это еще не сделано, войдите в toohello [портала Azure](https://portal.azure.com/) с помощью вашей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="ec246-114">If you haven't already done so, sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="ec246-115">Hello концентратора меню **дополнительные службы** и введите в список ресурсов hello, **службы восстановления** и нажмите кнопку **хранилищ служб восстановления**.</span><span class="sxs-lookup"><span data-stu-id="ec246-115">On hello Hub menu, click **More services** and in hello list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Создание хранилища служб восстановления — шаг 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="ec246-117">Если в подписке hello хранилищами служб восстановления, перечисленных hello хранилищ.</span><span class="sxs-lookup"><span data-stu-id="ec246-117">If there are recovery services vaults in hello subscription, hello vaults are listed.</span></span>
3. <span data-ttu-id="ec246-118">На hello **хранилищ служб восстановления** меню, нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="ec246-118">On hello **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Создание хранилища служб восстановления — шаг 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="ec246-120">хранилище служб восстановления Hello открывает колонку приглашением tooprovide **имя**, **подписки**, **группы ресурсов**, и **расположение**.</span><span class="sxs-lookup"><span data-stu-id="ec246-120">hello Recovery Services vault blade opens, prompting you tooprovide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Создание хранилища служб восстановления — шаг 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="ec246-122">Для **имя**, введите понятное имя tooidentify hello хранилище.</span><span class="sxs-lookup"><span data-stu-id="ec246-122">For **Name**, enter a friendly name tooidentify hello vault.</span></span> <span data-ttu-id="ec246-123">Имя Hello должно toobe уникальным для hello подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="ec246-123">hello name needs toobe unique for hello Azure subscription.</span></span> <span data-ttu-id="ec246-124">Введите имя длиной от 2 до 50 знаков.</span><span class="sxs-lookup"><span data-stu-id="ec246-124">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="ec246-125">Имя должно начинаться с буквы, оно может содержать только буквы, цифры и дефисы.</span><span class="sxs-lookup"><span data-stu-id="ec246-125">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="ec246-126">В hello **подписки** используйте hello раскрывающееся меню toochoose hello подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="ec246-126">In hello **Subscription** section, use hello drop-down menu toochoose hello Azure subscription.</span></span> <span data-ttu-id="ec246-127">При использовании только одной подписке, появившемся подписки и toohello следующий шаг можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="ec246-127">If you use only one subscription, that subscription appears and you can skip toohello next step.</span></span> <span data-ttu-id="ec246-128">Если вы не уверены, какие toouse подписки, используется по умолчанию hello (или рекомендуемые) подписки.</span><span class="sxs-lookup"><span data-stu-id="ec246-128">If you are not sure which subscription toouse, use hello default (or suggested) subscription.</span></span> <span data-ttu-id="ec246-129">Вариантов будет несколько только в том случае, если учетная запись вашей организации связана с несколькими подписками Azure.</span><span class="sxs-lookup"><span data-stu-id="ec246-129">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="ec246-130">В hello **группы ресурсов** раздела:</span><span class="sxs-lookup"><span data-stu-id="ec246-130">In hello **Resource group** section:</span></span>

    * <span data-ttu-id="ec246-131">Выберите **создать новый** Если toocreate новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ec246-131">select **Create new** if you want toocreate a new Resource group.</span></span>
    <span data-ttu-id="ec246-132">Или</span><span class="sxs-lookup"><span data-stu-id="ec246-132">Or</span></span>
    * <span data-ttu-id="ec246-133">Выберите **использовать существующие** и нажмите кнопку hello раскрывающееся меню toosee hello списка доступных групп ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ec246-133">select **Use existing** and click hello drop-down menu toosee hello available list of Resource groups.</span></span>

  <span data-ttu-id="ec246-134">Полные сведения для групп ресурсов см. в разделе hello [Обзор диспетчера ресурсов Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ec246-134">For complete information on Resource groups, see hello [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="ec246-135">Нажмите кнопку **расположение** tooselect hello географического региона для hello хранилища.</span><span class="sxs-lookup"><span data-stu-id="ec246-135">Click **Location** tooselect hello geographic region for hello vault.</span></span> <span data-ttu-id="ec246-136">Сделанный выбор определяет hello географическом регионе, куда отправлять данные резервной копии.</span><span class="sxs-lookup"><span data-stu-id="ec246-136">This choice determines hello geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="ec246-137">Hello нижней части колонки хранилище служб восстановления hello, нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="ec246-137">At hello bottom of hello Recovery Services vault blade, click **Create**.</span></span>

    <span data-ttu-id="ec246-138">Он может занять несколько минут для hello toobe создан в хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="ec246-138">It can take several minutes for hello Recovery Services vault toobe created.</span></span> <span data-ttu-id="ec246-139">Отслеживать уведомления о состоянии hello в верхней правой части hello hello портала.</span><span class="sxs-lookup"><span data-stu-id="ec246-139">Monitor hello status notifications in hello upper right-hand area of hello portal.</span></span> <span data-ttu-id="ec246-140">После создания своего хранилища, он отображается в списке hello хранилищами служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="ec246-140">Once your vault is created, it appears in hello list of Recovery Services vaults.</span></span> <span data-ttu-id="ec246-141">Если через несколько минут хранилище не отобразилось, нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="ec246-141">If after several minutes you don't see your vault, click **Refresh**.</span></span>

    ![Кнопка "Обновить"](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    <span data-ttu-id="ec246-143">Как только вы увидите ваше хранилище hello списка хранилищ служб восстановления, вы являетесь избыточности хранилища готов tooset hello.</span><span class="sxs-lookup"><span data-stu-id="ec246-143">Once you see your vault in hello list of Recovery Services vaults, you are ready tooset hello storage redundancy.</span></span>

### <a name="set-storage-redundancy-for-hello-vault"></a><span data-ttu-id="ec246-144">Значение избыточности хранилища для хранилища hello</span><span class="sxs-lookup"><span data-stu-id="ec246-144">Set storage redundancy for hello vault</span></span>
<span data-ttu-id="ec246-145">При создании хранилище служб восстановления, убедитесь, что избыточности хранилища является нужным образом настроенные hello.</span><span class="sxs-lookup"><span data-stu-id="ec246-145">When you create a Recovery Services vault, make sure storage redundancy is configured hello way you want.</span></span>

1. <span data-ttu-id="ec246-146">Из hello **хранилищ служб восстановления** колонка, щелкните новое хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="ec246-146">From hello **Recovery Services vaults** blade, click hello new vault.</span></span>

    ![Выберите новое хранилище hello hello списке хранилище служб восстановления](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="ec246-148">При выборе хранилища hello hello **хранилище служб восстановления** сужает колонки, а также колонку параметров hello (*имеющую hello имя хранилища hello вверху hello*) и откройте колонку сведения о хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="ec246-148">When you select hello vault, hello **Recovery Services vault** blade narrows, and hello Settings blade (*which has hello name of hello vault at hello top*) and hello vault details blade open.</span></span>

    ![Просмотр hello конфигурации хранилища для нового хранилища](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. <span data-ttu-id="ec246-150">В колонке параметров hello новое хранилище, используйте tooscroll вертикальной слайд hello вниз toohello управление раздел и нажмите кнопку **инфраструктуры резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="ec246-150">In hello new vault's Settings blade, use hello vertical slide tooscroll down toohello Manage section, and click **Backup Infrastructure**.</span></span>
    <span data-ttu-id="ec246-151">Открывает колонку Hello инфраструктуры резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="ec246-151">hello Backup Infrastructure blade opens.</span></span>
3. <span data-ttu-id="ec246-152">В колонке hello инфраструктуры резервного копирования, нажмите кнопку **конфигурация резервного копирования** tooopen hello **конфигурация резервного копирования** колонку.</span><span class="sxs-lookup"><span data-stu-id="ec246-152">In hello Backup Infrastructure blade, click **Backup Configuration** tooopen hello **Backup Configuration** blade.</span></span>

    ![Задание hello конфигурации хранилища для нового хранилища](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. <span data-ttu-id="ec246-154">Выберите параметр репликации соответствующих дисковых hello хранилища.</span><span class="sxs-lookup"><span data-stu-id="ec246-154">Choose hello appropriate storage replication option for your vault.</span></span>

    ![Варианты конфигурации хранилища](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    <span data-ttu-id="ec246-156">По умолчанию это геоизбыточное хранилище.</span><span class="sxs-lookup"><span data-stu-id="ec246-156">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="ec246-157">Если используется Azure в качестве конечной точки основного резервного хранилища, по-прежнему toouse **геоизбыточное**.</span><span class="sxs-lookup"><span data-stu-id="ec246-157">If you use Azure as a primary backup storage endpoint, continue toouse **Geo-redundant**.</span></span> <span data-ttu-id="ec246-158">Если вы не используете Azure как конечная точка основного хранилища резервной копии, выберите **локально избыточной**, что снижает затраты на хранилище Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ec246-158">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces hello Azure storage costs.</span></span> <span data-ttu-id="ec246-159">Дополнительные сведения о [геоизбыточном](../storage/common/storage-redundancy.md#geo-redundant-storage) и [локально избыточном](../storage/common/storage-redundancy.md#locally-redundant-storage) хранилищах см. в статье [Репликация службы хранилища Azure](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="ec246-159">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="ec246-160">Теперь, когда вы создали хранилище, настройте в нем резервное копирование файлов и папок.</span><span class="sxs-lookup"><span data-stu-id="ec246-160">Now that you've created a vault, configure it for backing up files and folders.</span></span>

## <a name="configure-hello-vault"></a><span data-ttu-id="ec246-161">Настройка хранилища hello</span><span class="sxs-lookup"><span data-stu-id="ec246-161">Configure hello vault</span></span>
1. <span data-ttu-id="ec246-162">На Здравствуйте колонку хранилище служб восстановления (для hello хранилища только что созданную), в разделе "Приступая к работе" hello, нажмите кнопку **резервного копирования**, то на hello **Приступая к резервному копированию** колонке выберите  **Цель резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="ec246-162">On hello Recovery Services vault blade (for hello vault you just created), in hello Getting Started section, click **Backup**, then on hello **Getting Started with Backup** blade, select **Backup goal**.</span></span>

    ![Открытая колонка цели резервного копирования](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    <span data-ttu-id="ec246-164">Hello **цель резервного копирования** открывает колонку.</span><span class="sxs-lookup"><span data-stu-id="ec246-164">hello **Backup Goal** blade opens.</span></span>

    ![Открытая колонка цели резервного копирования](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="ec246-166">Из hello **где выполняется рабочая нагрузка?** раскрывающееся меню, выберите **локальной**.</span><span class="sxs-lookup"><span data-stu-id="ec246-166">From hello **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

    <span data-ttu-id="ec246-167">Вы выбираете параметр **Локально**, потому что ваш компьютер Windows Server или Windows — это физический компьютер, которые не находится в Azure.</span><span class="sxs-lookup"><span data-stu-id="ec246-167">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="ec246-168">Из hello **что вам требуется toobackup?** последовательно выберите пункты **файлы и папки**и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ec246-168">From hello **What do you want toobackup?** menu, select **Files and folders**, and click **OK**.</span></span>

    ![Настройка резервного копирования файлов и папок](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

    <span data-ttu-id="ec246-170">После нажатия кнопки ОК, устанавливается флажок Далее слишком**цель резервного копирования**и hello **подготовки инфраструктуры** открывает колонку.</span><span class="sxs-lookup"><span data-stu-id="ec246-170">After clicking OK, a checkmark appears next too**Backup goal**, and hello **Prepare infrastructure** blade opens.</span></span>

    ![Цель резервного копирования настроена, на очереди подготовка инфраструктуры](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="ec246-172">На hello **подготовки инфраструктуры** колонка, щелкните **загрузить агент для Windows Server или Windows Client**.</span><span class="sxs-lookup"><span data-stu-id="ec246-172">On hello **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

    ![Download Agent for Windows Server or Windows Client](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    <span data-ttu-id="ec246-174">Если вы используете Windows Server необходимо, выберите toodownload hello агент для Windows Server Essential.</span><span class="sxs-lookup"><span data-stu-id="ec246-174">If you are using Windows Server Essential, then choose toodownload hello agent for Windows Server Essential.</span></span> <span data-ttu-id="ec246-175">Во всплывающем меню предложит toorun или сохранить MARSAgentInstaller.exe.</span><span class="sxs-lookup"><span data-stu-id="ec246-175">A pop-up menu prompts you toorun or save MARSAgentInstaller.exe.</span></span>

    ![Диалоговое окно MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="ec246-177">Во всплывающем меню загрузки приветствия щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ec246-177">In hello download pop-up menu, click **Save**.</span></span>

    <span data-ttu-id="ec246-178">По умолчанию hello **MARSagentinstaller.exe** файл сохраняется в папке загрузки tooyour.</span><span class="sxs-lookup"><span data-stu-id="ec246-178">By default, hello **MARSagentinstaller.exe** file is saved tooyour Downloads folder.</span></span> <span data-ttu-id="ec246-179">После завершения работы установщика hello появится всплывающее окно запросом установщиком toorun hello, или откройте папку hello.</span><span class="sxs-lookup"><span data-stu-id="ec246-179">When hello installer completes, you will see a pop-up asking if you want toorun hello installer, or open hello folder.</span></span>

    ![Download Agent for Windows Server or Windows Client](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    <span data-ttu-id="ec246-181">Tooinstall hello агент еще не требуется.</span><span class="sxs-lookup"><span data-stu-id="ec246-181">You don't need tooinstall hello agent yet.</span></span> <span data-ttu-id="ec246-182">Hello агент можно установить после загрузки hello учетные данные хранилища.</span><span class="sxs-lookup"><span data-stu-id="ec246-182">You can install hello agent after you have downloaded hello vault credentials.</span></span>

6. <span data-ttu-id="ec246-183">На hello **подготовки инфраструктуры** колонка, щелкните **загрузить**.</span><span class="sxs-lookup"><span data-stu-id="ec246-183">On hello **Prepare infrastructure** blade, click **Download**.</span></span>

    ![Скачивание учетных данных хранилища](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    <span data-ttu-id="ec246-185">Папка загрузки tooyour загрузки Hello учетные данные хранилища.</span><span class="sxs-lookup"><span data-stu-id="ec246-185">hello vault credentials download tooyour Downloads folder.</span></span> <span data-ttu-id="ec246-186">После завершения загрузки учетные данные хранилища hello появиться всплывающее окно запроса, если хотите tooopen или сохранить учетные данные hello.</span><span class="sxs-lookup"><span data-stu-id="ec246-186">After hello vault credentials finish downloading, you see a pop-up asking if you want tooopen or save hello credentials.</span></span> <span data-ttu-id="ec246-187">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ec246-187">Click **Save**.</span></span> <span data-ttu-id="ec246-188">Если вы случайно щелкнете **откройте**, позволяют hello диалоговое окно, которое пытается tooopen учетные данные хранилища hello, не.</span><span class="sxs-lookup"><span data-stu-id="ec246-188">If you accidentally click **Open**, let hello dialog that attempts tooopen hello vault credentials, fail.</span></span> <span data-ttu-id="ec246-189">Не удается открыть hello учетные данные хранилища.</span><span class="sxs-lookup"><span data-stu-id="ec246-189">You cannot open hello vault credentials.</span></span> <span data-ttu-id="ec246-190">Продолжить toohello следующий шаг.</span><span class="sxs-lookup"><span data-stu-id="ec246-190">Proceed toohello next step.</span></span> <span data-ttu-id="ec246-191">учетные данные хранилища Hello находятся в папке загрузки hello.</span><span class="sxs-lookup"><span data-stu-id="ec246-191">hello vault credentials are in hello Downloads folder.</span></span>   

    ![Загрузка учетных данных хранилища завершена](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a><span data-ttu-id="ec246-193">Установка и регистрация агента hello</span><span class="sxs-lookup"><span data-stu-id="ec246-193">Install and register hello agent</span></span>

> [!NOTE]
> <span data-ttu-id="ec246-194">Включение резервного копирования с использованием hello портал Azure, пока недоступно.</span><span class="sxs-lookup"><span data-stu-id="ec246-194">Enabling backup through hello Azure portal is not available, yet.</span></span> <span data-ttu-id="ec246-195">Используйте tooback агента служб восстановления Microsoft Azure hello копирования файлов и папок.</span><span class="sxs-lookup"><span data-stu-id="ec246-195">Use hello Microsoft Azure Recovery Services Agent tooback up your files and folders.</span></span>
>

1. <span data-ttu-id="ec246-196">Найдите и дважды щелкните hello **MARSagentinstaller.exe** из hello загрузки (или другие сохраненного расположения).</span><span class="sxs-lookup"><span data-stu-id="ec246-196">Locate and double-click hello **MARSagentinstaller.exe** from hello Downloads folder (or other saved location).</span></span>

    <span data-ttu-id="ec246-197">Установщик Hello предоставляет ряд сообщений извлечения, устанавливает и регистрирует агент служб восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="ec246-197">hello installer provides a series of messages as it extracts, installs, and registers hello Recovery Services agent.</span></span>

    ![Запуск установщика агента служб восстановления](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="ec246-199">Завершите мастер установки агента служб восстановления Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ec246-199">Complete hello Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="ec246-200">Мастер toocomplete hello, необходимо:</span><span class="sxs-lookup"><span data-stu-id="ec246-200">toocomplete hello wizard, you need to:</span></span>

   * <span data-ttu-id="ec246-201">Выберите расположение для папки установки и кэша hello.</span><span class="sxs-lookup"><span data-stu-id="ec246-201">Choose a location for hello installation and cache folder.</span></span>
   * <span data-ttu-id="ec246-202">Укажите прокси-сведений о сервере, если вы используете toohello tooconnect сервера прокси-сервера Интернета.</span><span class="sxs-lookup"><span data-stu-id="ec246-202">Provide your proxy server info if you use a proxy server tooconnect toohello internet.</span></span>
   * <span data-ttu-id="ec246-203">Если используется прокси-сервер, прошедший проверку подлинности, ввести имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="ec246-203">Provide your user name and password details if you use an authenticated proxy.</span></span>
   * <span data-ttu-id="ec246-204">Укажите учетные данные хранилища загружаются hello</span><span class="sxs-lookup"><span data-stu-id="ec246-204">Provide hello downloaded vault credentials</span></span>
   * <span data-ttu-id="ec246-205">Сохраните парольную фразу для шифрования hello в безопасном месте.</span><span class="sxs-lookup"><span data-stu-id="ec246-205">Save hello encryption passphrase in a secure location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="ec246-206">При потере или забудете парольную фразу hello, корпорация Майкрософт не может выполнить восстановление резервной копии данных hello.</span><span class="sxs-lookup"><span data-stu-id="ec246-206">If you lose or forget hello passphrase, Microsoft cannot help recover hello backup data.</span></span> <span data-ttu-id="ec246-207">Сохраните файл hello в безопасном месте.</span><span class="sxs-lookup"><span data-stu-id="ec246-207">Save hello file in a secure location.</span></span> <span data-ttu-id="ec246-208">Это обязательный toorestore резервной копии.</span><span class="sxs-lookup"><span data-stu-id="ec246-208">It is required toorestore a backup.</span></span>
     >
     >

<span data-ttu-id="ec246-209">Hello агент установлен, и ваш компьютер входит в хранилище зарегистрированного toohello.</span><span class="sxs-lookup"><span data-stu-id="ec246-209">hello agent is now installed and your machine is registered toohello vault.</span></span> <span data-ttu-id="ec246-210">Вы будете готовы tooconfigure и расписания резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="ec246-210">You're ready tooconfigure and schedule your backup.</span></span>

## <a name="network-and-connectivity-requirements"></a><span data-ttu-id="ec246-211">Требования к сети и подключению</span><span class="sxs-lookup"><span data-stu-id="ec246-211">Network and Connectivity Requirements</span></span>

<span data-ttu-id="ec246-212">Если компьютер или прокси-сервера имеет ограниченный доступ к Интернету, обеспечить параметры брандмауэра на mcahine hello и прокси-hello настроенных tooallow следующие URL-адреса:</span><span class="sxs-lookup"><span data-stu-id="ec246-212">If your machine/proxy has limited internet access, ensure that firewall settings on hello mcahine/proxy are configured tooallow hello following URLs:</span></span> <br>
    1. <span data-ttu-id="ec246-213">www.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="ec246-213">www.msftncsi.com</span></span>
    2. <span data-ttu-id="ec246-214">*.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="ec246-214">*.Microsoft.com</span></span>
    3. <span data-ttu-id="ec246-215">*.WindowsAzure.com</span><span class="sxs-lookup"><span data-stu-id="ec246-215">*.WindowsAzure.com</span></span>
    4. <span data-ttu-id="ec246-216">*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="ec246-216">*.microsoftonline.com</span></span>
    5. <span data-ttu-id="ec246-217">*.windows.net</span><span class="sxs-lookup"><span data-stu-id="ec246-217">*.windows.ne</span></span>

## <a name="back-up-your-files-and-folders"></a><span data-ttu-id="ec246-218">Резервное копирование файлов и папок</span><span class="sxs-lookup"><span data-stu-id="ec246-218">Back up your files and folders</span></span>
<span data-ttu-id="ec246-219">Hello начальной резервной копии включает в себя две основные задачи:</span><span class="sxs-lookup"><span data-stu-id="ec246-219">hello initial backup includes two key tasks:</span></span>

* <span data-ttu-id="ec246-220">Планирование резервного копирования hello</span><span class="sxs-lookup"><span data-stu-id="ec246-220">Schedule hello backup</span></span>
* <span data-ttu-id="ec246-221">Резервное копирование файлов и папок для hello первый раз</span><span class="sxs-lookup"><span data-stu-id="ec246-221">Back up files and folders for hello first time</span></span>

<span data-ttu-id="ec246-222">toocomplete hello начальной резервной копии, используйте агент служб восстановления Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ec246-222">toocomplete hello initial backup, use hello Microsoft Azure Recovery Services agent.</span></span>

### <a name="tooschedule-hello-backup-job"></a><span data-ttu-id="ec246-223">задание резервного копирования tooschedule hello</span><span class="sxs-lookup"><span data-stu-id="ec246-223">tooschedule hello backup job</span></span>
1. <span data-ttu-id="ec246-224">Откройте hello агента служб восстановления Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="ec246-224">Open hello Microsoft Azure Recovery Services agent.</span></span> <span data-ttu-id="ec246-225">Его можно найти, выполнив поиск строки **служба архивации Microsoft Azure**на компьютере.</span><span class="sxs-lookup"><span data-stu-id="ec246-225">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Запустите агент служб восстановления Azure hello](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)
2. <span data-ttu-id="ec246-227">Агент служб восстановления hello, щелкните **планирования резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="ec246-227">In hello Recovery Services agent, click **Schedule Backup**.</span></span>

    ![Планирование архивации Windows Server](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)
3. <span data-ttu-id="ec246-229">На hello Приступая к работе страница приветствия мастера планирования резервного копирования, нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="ec246-229">On hello Getting started page of hello Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="ec246-230">На странице выбора элементов tooBackup hello щелкните **добавить элементы**.</span><span class="sxs-lookup"><span data-stu-id="ec246-230">On hello Select Items tooBackup page, click **Add Items**.</span></span>
5. <span data-ttu-id="ec246-231">Выберите hello файлы и папки, которые вы tooback копирование и нажмите кнопку **хорошо**.</span><span class="sxs-lookup"><span data-stu-id="ec246-231">Select hello files and folders that you want tooback up, and then click **Okay**.</span></span>
6. <span data-ttu-id="ec246-232">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="ec246-232">Click **Next**.</span></span>
7. <span data-ttu-id="ec246-233">На hello **укажите расписание архивации** укажите hello **расписание резервного копирования** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="ec246-233">On hello **Specify Backup Schedule** page, specify hello **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="ec246-234">Вы можете запланировать ежедневную (не более трех раз в день) или еженедельную архивацию.</span><span class="sxs-lookup"><span data-stu-id="ec246-234">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Элементы для архивации Windows Server](./media/backup-try-azure-backup-in-10-mins/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="ec246-236">Дополнительные сведения о как toospecify hello расписание резервного копирования см. в статье hello [резервного копирования Azure используйте tooreplace инфраструктуры ленты](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="ec246-236">For more information about how toospecify hello backup schedule, see hello article [Use Azure Backup tooreplace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >

8. <span data-ttu-id="ec246-237">На hello **выбрать политику хранения** страницу, выберите hello **политики хранения** для hello резервной копии.</span><span class="sxs-lookup"><span data-stu-id="ec246-237">On hello **Select Retention Policy** page, select hello **Retention Policy** for hello backup copy.</span></span>

    <span data-ttu-id="ec246-238">Политика хранения Hello указывает время хранения резервных копий данных hello.</span><span class="sxs-lookup"><span data-stu-id="ec246-238">hello retention policy specifies how long hello backup data is stored.</span></span> <span data-ttu-id="ec246-239">Вместо того чтобы задавать «плоский политика» для всех точек резервного копирования, можно указать при архивации hello на основе политик крепления.</span><span class="sxs-lookup"><span data-stu-id="ec246-239">Rather than specifying a “flat policy” for all backup points, you can specify different retention policies based on when hello backup occurs.</span></span> <span data-ttu-id="ec246-240">Вы можете изменить toomeet политики хранения ежедневно, еженедельно, ежемесячно и ежегодно hello вашим потребностям.</span><span class="sxs-lookup"><span data-stu-id="ec246-240">You can modify hello daily, weekly, monthly, and yearly retention policies toomeet your needs.</span></span>
9. <span data-ttu-id="ec246-241">На странице выберите тип начального архива hello выберите тип начального архива hello.</span><span class="sxs-lookup"><span data-stu-id="ec246-241">On hello Choose Initial Backup Type page, choose hello initial backup type.</span></span> <span data-ttu-id="ec246-242">Оставьте параметр hello **автоматически по сети hello** , а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="ec246-242">Leave hello option **Automatically over hello network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="ec246-243">Резервное копирование автоматически hello сети или автономно резервное копирование.</span><span class="sxs-lookup"><span data-stu-id="ec246-243">You can back up automatically over hello network, or you can back up offline.</span></span> <span data-ttu-id="ec246-244">Hello в этой статье описываются hello процесс резервного копирования автоматически.</span><span class="sxs-lookup"><span data-stu-id="ec246-244">hello remainder of this article describes hello process for backing up automatically.</span></span> <span data-ttu-id="ec246-245">Если вы предпочитаете toodo автономной резервной копии, изучите статью hello [автономного резервного копирования рабочего процесса в службе архивации Azure](backup-azure-backup-import-export.md) для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="ec246-245">If you prefer toodo an offline backup, review hello article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="ec246-246">На странице подтверждения hello, просмотрите сведения hello и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="ec246-246">On hello Confirmation page, review hello information, and then click **Finish**.</span></span>
11. <span data-ttu-id="ec246-247">После завершения работы мастера hello, создания расписания резервного копирования hello, нажмите кнопку **закрыть**.</span><span class="sxs-lookup"><span data-stu-id="ec246-247">After hello wizard finishes creating hello backup schedule, click **Close**.</span></span>

### <a name="tooback-up-files-and-folders-for-hello-first-time"></a><span data-ttu-id="ec246-248">tooback копирования файлов и папок для hello первый раз</span><span class="sxs-lookup"><span data-stu-id="ec246-248">tooback up files and folders for hello first time</span></span>
1. <span data-ttu-id="ec246-249">Агент служб восстановления hello, щелкните **Архивировать** toocomplete hello начального заполнения hello сети.</span><span class="sxs-lookup"><span data-stu-id="ec246-249">In hello Recovery Services agent, click **Back Up Now** toocomplete hello initial seeding over hello network.</span></span>

    ![Моментальная архивация Windows Server](./media/backup-try-azure-backup-in-10-mins/backup-now.png)
2. <span data-ttu-id="ec246-251">На странице подтверждения hello просмотрите параметры hello hello мастер немедленной архивации будет использовать tooback машину hello.</span><span class="sxs-lookup"><span data-stu-id="ec246-251">On hello Confirmation page, review hello settings that hello Back Up Now Wizard will use tooback up hello machine.</span></span> <span data-ttu-id="ec246-252">Затем нажмите кнопку **Архивировать**.</span><span class="sxs-lookup"><span data-stu-id="ec246-252">Then click **Back Up**.</span></span>
3. <span data-ttu-id="ec246-253">Нажмите кнопку **закрыть** tooclose приветствия мастера.</span><span class="sxs-lookup"><span data-stu-id="ec246-253">Click **Close** tooclose hello wizard.</span></span> <span data-ttu-id="ec246-254">Если вы закроете мастер hello до завершения процесса резервного копирования hello, мастер hello переходит toorun в фоновом режиме hello.</span><span class="sxs-lookup"><span data-stu-id="ec246-254">If you close hello wizard before hello backup process finishes, hello wizard continues toorun in hello background.</span></span>

<span data-ttu-id="ec246-255">После завершения начальной резервной копии hello hello **задание завершено** состояние отображается в консоли hello резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="ec246-255">After hello initial backup is completed, hello **Job completed** status appears in hello Backup console.</span></span>

![Первоначальное восстановление завершено](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="questions"></a><span data-ttu-id="ec246-257">Вопросы?</span><span class="sxs-lookup"><span data-stu-id="ec246-257">Questions?</span></span>
<span data-ttu-id="ec246-258">Если у вас есть вопросы или при наличии любой возможности, хотелось бы включены, toosee [отправить отзыв](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="ec246-258">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec246-259">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ec246-259">Next steps</span></span>
* <span data-ttu-id="ec246-260">См. дополнительные сведения об [архивации компьютеров Windows](backup-configure-vault.md).</span><span class="sxs-lookup"><span data-stu-id="ec246-260">Get more details about [backing up Windows machines](backup-configure-vault.md).</span></span>
* <span data-ttu-id="ec246-261">Теперь, когда вы выполнили резервное копирование файлов и папок, вы можете [управлять хранилищами и серверами](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="ec246-261">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="ec246-262">Если вам требуется toorestore резервной копии, используйте в этой статье слишком[восстановить компьютер Windows tooa файлы](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="ec246-262">If you need toorestore a backup, use this article too[restore files tooa Windows machine](backup-azure-restore-windows-server.md).</span></span>
