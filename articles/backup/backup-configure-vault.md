---
title: "aaaUse tooback агент архивации Azure копирования файлов и папок | Документы Microsoft"
description: "Используйте tooback агента службы архивации Microsoft Azure hello копирование файлов и папок tooAzure Windows. Создание хранилища служб восстановления, установка агента резервного копирования hello, определить политику резервного копирования hello и выполнить резервное копирование начальной hello hello файлов и папок."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "хранилище архивации; архивация сервера Windows; архивация Windows;"
ms.assetid: 7f5b1943-b3c1-4ddb-8fb7-3560533c68d5
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: be203c24841971872b5c6e7cf260a2fa5c58ac47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-windows-server-or-client-tooazure-using-hello-resource-manager-deployment-model"></a><span data-ttu-id="1cb72-105">Резервное копирование сервера или клиента tooAzure, с помощью модели развертывания диспетчера ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="1cb72-105">Back up a Windows Server or client tooAzure using hello Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1cb72-106">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="1cb72-106">Azure portal</span></span>](backup-configure-vault.md)
> * [<span data-ttu-id="1cb72-107">Классический портал.</span><span class="sxs-lookup"><span data-stu-id="1cb72-107">Classic portal</span></span>](backup-configure-vault-classic.md)
>
>

<span data-ttu-id="1cb72-108">В этой статье объясняется, как tooAzure tooback Windows Server (или клиента Windows) файлов и папок с помощью службы архивации Azure hello модели развертывания диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="1cb72-108">This article explains how tooback up your Windows Server (or Windows client) files and folders tooAzure with Azure Backup using hello Resource Manager deployment model.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/backup-deployment-models.md)]

![Шаги архивации](./media/backup-configure-vault/initial-backup-process.png)

## <a name="before-you-start"></a><span data-ttu-id="1cb72-110">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="1cb72-110">Before you start</span></span>
<span data-ttu-id="1cb72-111">tooback tooAzure клиента или сервера требуется учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="1cb72-111">tooback up a server or client tooAzure, you need an Azure account.</span></span> <span data-ttu-id="1cb72-112">Если ее нет, можно создать [бесплатную учетную запись](https://azure.microsoft.com/free/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="1cb72-112">If you don't have one, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="1cb72-113">Создание хранилища служб восстановления</span><span class="sxs-lookup"><span data-stu-id="1cb72-113">Create a Recovery Services vault</span></span>
<span data-ttu-id="1cb72-114">Хранилище служб восстановления — это сущность, в которой хранятся все резервные копии hello и точек восстановления, которые создаются в течение времени.</span><span class="sxs-lookup"><span data-stu-id="1cb72-114">A Recovery Services vault is an entity that stores all hello backups and recovery points you create over time.</span></span> <span data-ttu-id="1cb72-115">хранилище служб восстановления Hello также содержит hello применить политику резервного копирования toohello защищенные файлы и папки.</span><span class="sxs-lookup"><span data-stu-id="1cb72-115">hello Recovery Services vault also contains hello backup policy applied toohello protected files and folders.</span></span> <span data-ttu-id="1cb72-116">При создании хранилище служб восстановления следует также выбрать параметр избыточности хранилища соответствующие hello.</span><span class="sxs-lookup"><span data-stu-id="1cb72-116">When you create a Recovery Services vault, you should also select hello appropriate storage redundancy option.</span></span>

### <a name="toocreate-a-recovery-services-vault"></a><span data-ttu-id="1cb72-117">toocreate хранилище служб восстановления</span><span class="sxs-lookup"><span data-stu-id="1cb72-117">toocreate a Recovery Services vault</span></span>
1. <span data-ttu-id="1cb72-118">Если это еще не сделано, войдите в toohello [портала Azure](https://portal.azure.com/) с помощью вашей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="1cb72-118">If you haven't already done so, sign in toohello [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="1cb72-119">Hello концентратора меню **дополнительные службы** и введите в список ресурсов hello, **службы восстановления** и нажмите кнопку **хранилищ служб восстановления**.</span><span class="sxs-lookup"><span data-stu-id="1cb72-119">On hello Hub menu, click **More services** and in hello list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Создание хранилища служб восстановления — шаг 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="1cb72-121">Если в подписке hello хранилищами служб восстановления, перечисленных hello хранилищ.</span><span class="sxs-lookup"><span data-stu-id="1cb72-121">If there are recovery services vaults in hello subscription, hello vaults are listed.</span></span>

3. <span data-ttu-id="1cb72-122">На hello **хранилищ служб восстановления** меню, нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="1cb72-122">On hello **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Создание хранилища служб восстановления — шаг 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="1cb72-124">хранилище служб восстановления Hello открывает колонку приглашением tooprovide **имя**, **подписки**, **группы ресурсов**, и **расположение**.</span><span class="sxs-lookup"><span data-stu-id="1cb72-124">hello Recovery Services vault blade opens, prompting you tooprovide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Создание хранилища служб восстановления — шаг 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="1cb72-126">Для **имя**, введите понятное имя tooidentify hello хранилище.</span><span class="sxs-lookup"><span data-stu-id="1cb72-126">For **Name**, enter a friendly name tooidentify hello vault.</span></span> <span data-ttu-id="1cb72-127">Имя Hello должно toobe уникальным для hello подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="1cb72-127">hello name needs toobe unique for hello Azure subscription.</span></span> <span data-ttu-id="1cb72-128">Введите имя длиной от 2 до 50 знаков.</span><span class="sxs-lookup"><span data-stu-id="1cb72-128">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="1cb72-129">Имя должно начинаться с буквы, оно может содержать только буквы, цифры и дефисы.</span><span class="sxs-lookup"><span data-stu-id="1cb72-129">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="1cb72-130">В hello **подписки** используйте hello раскрывающееся меню toochoose hello подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="1cb72-130">In hello **Subscription** section, use hello drop-down menu toochoose hello Azure subscription.</span></span> <span data-ttu-id="1cb72-131">При использовании только одной подписке, появившемся подписки и toohello следующий шаг можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="1cb72-131">If you use only one subscription, that subscription appears and you can skip toohello next step.</span></span> <span data-ttu-id="1cb72-132">Если вы не уверены, какие toouse подписки, используется по умолчанию hello (или рекомендуемые) подписки.</span><span class="sxs-lookup"><span data-stu-id="1cb72-132">If you are not sure which subscription toouse, use hello default (or suggested) subscription.</span></span> <span data-ttu-id="1cb72-133">Вариантов будет несколько только в том случае, если учетная запись вашей организации связана с несколькими подписками Azure.</span><span class="sxs-lookup"><span data-stu-id="1cb72-133">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="1cb72-134">В hello **группы ресурсов** раздела:</span><span class="sxs-lookup"><span data-stu-id="1cb72-134">In hello **Resource group** section:</span></span>

    * <span data-ttu-id="1cb72-135">Выберите **создать новый** Если toocreate новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="1cb72-135">select **Create new** if you want toocreate a new Resource group.</span></span>
    <span data-ttu-id="1cb72-136">Или</span><span class="sxs-lookup"><span data-stu-id="1cb72-136">Or</span></span>
    * <span data-ttu-id="1cb72-137">Выберите **использовать существующие** и нажмите кнопку hello раскрывающееся меню toosee hello списка доступных групп ресурсов.</span><span class="sxs-lookup"><span data-stu-id="1cb72-137">select **Use existing** and click hello drop-down menu toosee hello available list of Resource groups.</span></span>

  <span data-ttu-id="1cb72-138">Полные сведения для групп ресурсов см. в разделе hello [Обзор диспетчера ресурсов Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1cb72-138">For complete information on Resource groups, see hello [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="1cb72-139">Нажмите кнопку **расположение** tooselect hello географического региона для hello хранилища.</span><span class="sxs-lookup"><span data-stu-id="1cb72-139">Click **Location** tooselect hello geographic region for hello vault.</span></span> <span data-ttu-id="1cb72-140">Сделанный выбор определяет hello географическом регионе, куда отправлять данные резервной копии.</span><span class="sxs-lookup"><span data-stu-id="1cb72-140">This choice determines hello geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="1cb72-141">Hello нижней части колонки хранилище служб восстановления hello, нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="1cb72-141">At hello bottom of hello Recovery Services vault blade, click **Create**.</span></span>

  <span data-ttu-id="1cb72-142">Он может занять несколько минут для hello toobe создан в хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="1cb72-142">It can take several minutes for hello Recovery Services vault toobe created.</span></span> <span data-ttu-id="1cb72-143">Отслеживать уведомления о состоянии hello в верхней правой части hello hello портала.</span><span class="sxs-lookup"><span data-stu-id="1cb72-143">Monitor hello status notifications in hello upper right-hand area of hello portal.</span></span> <span data-ttu-id="1cb72-144">После создания своего хранилища, он отображается в списке hello хранилищами служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="1cb72-144">Once your vault is created, it appears in hello list of Recovery Services vaults.</span></span> <span data-ttu-id="1cb72-145">Если через несколько минут хранилище не отобразилось, нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="1cb72-145">If after several minutes you don't see your vault, click **Refresh**.</span></span>

  ![Кнопка "Обновить"](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

  <span data-ttu-id="1cb72-147">Как только вы увидите ваше хранилище hello списка хранилищ служб восстановления, вы являетесь избыточности хранилища готов tooset hello.</span><span class="sxs-lookup"><span data-stu-id="1cb72-147">Once you see your vault in hello list of Recovery Services vaults, you are ready tooset hello storage redundancy.</span></span>


### <a name="set-storage-redundancy"></a><span data-ttu-id="1cb72-148">Установка избыточности хранилища</span><span class="sxs-lookup"><span data-stu-id="1cb72-148">Set storage redundancy</span></span>
<span data-ttu-id="1cb72-149">При первом создании хранилища служб восстановления нужно определить способ его репликации.</span><span class="sxs-lookup"><span data-stu-id="1cb72-149">When you first create a Recovery Services vault you determine how storage is replicated.</span></span>

1. <span data-ttu-id="1cb72-150">Из hello **хранилищ служб восстановления** колонка, щелкните новое хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="1cb72-150">From hello **Recovery Services vaults** blade, click hello new vault.</span></span>

    ![Выберите новое хранилище hello hello списке хранилище служб восстановления](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="1cb72-152">При выборе хранилища hello hello **хранилище служб восстановления** сужает колонки, а также колонку параметров hello (*имеющую hello имя хранилища hello вверху hello*) и откройте колонку сведения о хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="1cb72-152">When you select hello vault, hello **Recovery Services vault** blade narrows, and hello Settings blade (*which has hello name of hello vault at hello top*) and hello vault details blade open.</span></span>

    ![Просмотр hello конфигурации хранилища для нового хранилища](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)

2. <span data-ttu-id="1cb72-154">В колонке параметров hello новое хранилище, используйте tooscroll вертикальной слайд hello вниз toohello управление раздел и нажмите кнопку **инфраструктуры резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="1cb72-154">In hello new vault's Settings blade, use hello vertical slide tooscroll down toohello Manage section, and click **Backup Infrastructure**.</span></span>

  <span data-ttu-id="1cb72-155">Открывает колонку Hello инфраструктуры резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="1cb72-155">hello Backup Infrastructure blade opens.</span></span>

3. <span data-ttu-id="1cb72-156">В колонке hello инфраструктуры резервного копирования, нажмите кнопку **конфигурация резервного копирования** tooopen hello **конфигурация резервного копирования** колонку.</span><span class="sxs-lookup"><span data-stu-id="1cb72-156">In hello Backup Infrastructure blade, click **Backup Configuration** tooopen hello **Backup Configuration** blade.</span></span>

  ![Задание hello конфигурации хранилища для нового хранилища](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)

4. <span data-ttu-id="1cb72-158">Выберите параметр репликации соответствующих дисковых hello хранилища.</span><span class="sxs-lookup"><span data-stu-id="1cb72-158">Choose hello appropriate storage replication option for your vault.</span></span>

  ![Варианты конфигурации хранилища](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

  <span data-ttu-id="1cb72-160">По умолчанию это геоизбыточное хранилище.</span><span class="sxs-lookup"><span data-stu-id="1cb72-160">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="1cb72-161">Если используется Azure в качестве конечной точки основного резервного хранилища, по-прежнему toouse **геоизбыточное**.</span><span class="sxs-lookup"><span data-stu-id="1cb72-161">If you use Azure as a primary backup storage endpoint, continue toouse **Geo-redundant**.</span></span> <span data-ttu-id="1cb72-162">Если вы не используете Azure как конечная точка основного хранилища резервной копии, выберите **локально избыточной**, что снижает затраты на хранилище Azure hello.</span><span class="sxs-lookup"><span data-stu-id="1cb72-162">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces hello Azure storage costs.</span></span> <span data-ttu-id="1cb72-163">Дополнительные сведения о [геоизбыточном](../storage/common/storage-redundancy.md#geo-redundant-storage) и [локально избыточном](../storage/common/storage-redundancy.md#locally-redundant-storage) хранилищах см. в статье [Репликация службы хранилища Azure](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="1cb72-163">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="1cb72-164">После создания хранилища Подготовьте tooback вашей инфраструктуры, файлов и папок, загрузка и установка агента служб восстановления Microsoft Azure hello, загрузить учетные данные хранилища и затем с помощью агента hello tooregister эти учетные данные, с хранилище Hello.</span><span class="sxs-lookup"><span data-stu-id="1cb72-164">Now that you've created a vault, prepare your infrastructure tooback up files and folders by downloading and installing hello Microsoft Azure Recovery Services agent, downloading vault credentials, and then using those credentials tooregister hello agent with hello vault.</span></span>

## <a name="configure-hello-vault"></a><span data-ttu-id="1cb72-165">Настройка хранилища hello</span><span class="sxs-lookup"><span data-stu-id="1cb72-165">Configure hello vault</span></span>

1. <span data-ttu-id="1cb72-166">На Здравствуйте колонку хранилище служб восстановления (для hello хранилища только что созданную), в разделе "Приступая к работе" hello, нажмите кнопку **резервного копирования**, то на hello **Приступая к резервному копированию** колонке выберите  **Цель резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="1cb72-166">On hello Recovery Services vault blade (for hello vault you just created), in hello Getting Started section, click **Backup**, then on hello **Getting Started with Backup** blade, select **Backup goal**.</span></span>

  ![Открытая колонка цели резервного копирования](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

  <span data-ttu-id="1cb72-168">Hello **цель резервного копирования** открывает колонку.</span><span class="sxs-lookup"><span data-stu-id="1cb72-168">hello **Backup Goal** blade opens.</span></span> <span data-ttu-id="1cb72-169">Если hello хранилище служб восстановления был ранее настроен, затем hello **цель резервного копирования** колонок открывается при нажатии кнопки **резервного копирования** на hello служб восстановления хранилище колонку.</span><span class="sxs-lookup"><span data-stu-id="1cb72-169">If hello Recovery Services vault has been previously configured, then hello **Backup Goal** blades opens when you click **Backup** on hello Recovery Services vault blade.</span></span>

  ![Открытая колонка цели резервного копирования](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="1cb72-171">Из hello **где выполняется рабочая нагрузка?** раскрывающееся меню, выберите **локальной**.</span><span class="sxs-lookup"><span data-stu-id="1cb72-171">From hello **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

  <span data-ttu-id="1cb72-172">Вы выбираете параметр **Локально**, потому что ваш компьютер Windows Server или Windows — это физический компьютер, которые не находится в Azure.</span><span class="sxs-lookup"><span data-stu-id="1cb72-172">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="1cb72-173">Из hello **что вам требуется toobackup?** последовательно выберите пункты **файлы и папки**и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1cb72-173">From hello **What do you want toobackup?** menu, select **Files and folders**, and click **OK**.</span></span>

  ![Настройка резервного копирования файлов и папок](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

  <span data-ttu-id="1cb72-175">После нажатия кнопки ОК, устанавливается флажок Далее слишком**цель резервного копирования**и hello **подготовки инфраструктуры** открывает колонку.</span><span class="sxs-lookup"><span data-stu-id="1cb72-175">After clicking OK, a checkmark appears next too**Backup goal**, and hello **Prepare infrastructure** blade opens.</span></span>

  ![Цель резервного копирования настроена, на очереди подготовка инфраструктуры](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="1cb72-177">На hello **подготовки инфраструктуры** колонка, щелкните **загрузить агент для Windows Server или Windows Client**.</span><span class="sxs-lookup"><span data-stu-id="1cb72-177">On hello **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

  ![Download Agent for Windows Server or Windows Client](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

  <span data-ttu-id="1cb72-179">Если вы используете Windows Server необходимо, выберите toodownload hello агент для Windows Server Essential.</span><span class="sxs-lookup"><span data-stu-id="1cb72-179">If you are using Windows Server Essential, then choose toodownload hello agent for Windows Server Essential.</span></span> <span data-ttu-id="1cb72-180">Во всплывающем меню предложит toorun или сохранить MARSAgentInstaller.exe.</span><span class="sxs-lookup"><span data-stu-id="1cb72-180">A pop-up menu prompts you toorun or save MARSAgentInstaller.exe.</span></span>

  ![Диалоговое окно MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="1cb72-182">Во всплывающем меню загрузки приветствия щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="1cb72-182">In hello download pop-up menu, click **Save**.</span></span>

  <span data-ttu-id="1cb72-183">По умолчанию hello **MARSagentinstaller.exe** файл сохраняется в папке загрузки tooyour.</span><span class="sxs-lookup"><span data-stu-id="1cb72-183">By default, hello **MARSagentinstaller.exe** file is saved tooyour Downloads folder.</span></span> <span data-ttu-id="1cb72-184">После завершения работы установщика hello появится всплывающее окно запросом установщиком toorun hello, или откройте папку hello.</span><span class="sxs-lookup"><span data-stu-id="1cb72-184">When hello installer completes, you will see a pop-up asking if you want toorun hello installer, or open hello folder.</span></span>

  ![Download Agent for Windows Server or Windows Client](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

  <span data-ttu-id="1cb72-186">Tooinstall hello агент еще не требуется.</span><span class="sxs-lookup"><span data-stu-id="1cb72-186">You don't need tooinstall hello agent yet.</span></span> <span data-ttu-id="1cb72-187">Hello агент можно установить после загрузки hello учетные данные хранилища.</span><span class="sxs-lookup"><span data-stu-id="1cb72-187">You can install hello agent after you have downloaded hello vault credentials.</span></span>

6. <span data-ttu-id="1cb72-188">На hello **подготовки инфраструктуры** колонка, щелкните **загрузить**.</span><span class="sxs-lookup"><span data-stu-id="1cb72-188">On hello **Prepare infrastructure** blade, click **Download**.</span></span>

  ![Скачивание учетных данных хранилища](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

  <span data-ttu-id="1cb72-190">Папка загрузки tooyour загрузки Hello учетные данные хранилища.</span><span class="sxs-lookup"><span data-stu-id="1cb72-190">hello vault credentials download tooyour Downloads folder.</span></span> <span data-ttu-id="1cb72-191">После завершения загрузки учетные данные хранилища hello появиться всплывающее окно запроса, если хотите tooopen или сохранить учетные данные hello.</span><span class="sxs-lookup"><span data-stu-id="1cb72-191">After hello vault credentials finish downloading, you see a pop-up asking if you want tooopen or save hello credentials.</span></span> <span data-ttu-id="1cb72-192">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="1cb72-192">Click **Save**.</span></span> <span data-ttu-id="1cb72-193">Если вы случайно щелкнете **откройте**, позволяют hello диалоговое окно, которое пытается tooopen учетные данные хранилища hello, не.</span><span class="sxs-lookup"><span data-stu-id="1cb72-193">If you accidentally click **Open**, let hello dialog that attempts tooopen hello vault credentials, fail.</span></span> <span data-ttu-id="1cb72-194">Не удается открыть hello учетные данные хранилища.</span><span class="sxs-lookup"><span data-stu-id="1cb72-194">You cannot open hello vault credentials.</span></span> <span data-ttu-id="1cb72-195">Продолжить toohello следующий шаг.</span><span class="sxs-lookup"><span data-stu-id="1cb72-195">Proceed toohello next step.</span></span> <span data-ttu-id="1cb72-196">учетные данные хранилища Hello находятся в папке загрузки hello.</span><span class="sxs-lookup"><span data-stu-id="1cb72-196">hello vault credentials are in hello Downloads folder.</span></span>   

  ![Загрузка учетных данных хранилища завершена](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a><span data-ttu-id="1cb72-198">Установка и регистрация агента hello</span><span class="sxs-lookup"><span data-stu-id="1cb72-198">Install and register hello agent</span></span>

> [!NOTE]
> <span data-ttu-id="1cb72-199">Включение резервного копирования с использованием hello портал Azure, пока недоступно.</span><span class="sxs-lookup"><span data-stu-id="1cb72-199">Enabling backup through hello Azure portal is not available, yet.</span></span> <span data-ttu-id="1cb72-200">Используйте tooback агента служб восстановления Microsoft Azure hello копирования файлов и папок.</span><span class="sxs-lookup"><span data-stu-id="1cb72-200">Use hello Microsoft Azure Recovery Services Agent tooback up your files and folders.</span></span>
>

1. <span data-ttu-id="1cb72-201">Найдите и дважды щелкните hello **MARSagentinstaller.exe** из hello загрузки (или другие сохраненного расположения).</span><span class="sxs-lookup"><span data-stu-id="1cb72-201">Locate and double-click hello **MARSagentinstaller.exe** from hello Downloads folder (or other saved location).</span></span>

  <span data-ttu-id="1cb72-202">Установщик Hello предоставляет ряд сообщений извлечения, устанавливает и регистрирует агент служб восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="1cb72-202">hello installer provides a series of messages as it extracts, installs, and registers hello Recovery Services agent.</span></span>

  ![Запуск установщика агента служб восстановления](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="1cb72-204">Завершите мастер установки агента служб восстановления Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="1cb72-204">Complete hello Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="1cb72-205">Мастер toocomplete hello, необходимо:</span><span class="sxs-lookup"><span data-stu-id="1cb72-205">toocomplete hello wizard, you need to:</span></span>

  * <span data-ttu-id="1cb72-206">Выберите расположение для папки установки и кэша hello.</span><span class="sxs-lookup"><span data-stu-id="1cb72-206">Choose a location for hello installation and cache folder.</span></span>
  * <span data-ttu-id="1cb72-207">Укажите прокси-сведений о сервере, если вы используете toohello tooconnect сервера прокси-сервера Интернета.</span><span class="sxs-lookup"><span data-stu-id="1cb72-207">Provide your proxy server info if you use a proxy server tooconnect toohello internet.</span></span>
  * <span data-ttu-id="1cb72-208">Если используется прокси-сервер, прошедший проверку подлинности, ввести имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="1cb72-208">Provide your user name and password details if you use an authenticated proxy.</span></span>
  * <span data-ttu-id="1cb72-209">Укажите учетные данные хранилища загружаются hello</span><span class="sxs-lookup"><span data-stu-id="1cb72-209">Provide hello downloaded vault credentials</span></span>
  * <span data-ttu-id="1cb72-210">Сохраните парольную фразу для шифрования hello в безопасном месте.</span><span class="sxs-lookup"><span data-stu-id="1cb72-210">Save hello encryption passphrase in a secure location.</span></span>

  > [!NOTE]
  > <span data-ttu-id="1cb72-211">При потере или забудете парольную фразу hello, корпорация Майкрософт не может выполнить восстановление резервной копии данных hello.</span><span class="sxs-lookup"><span data-stu-id="1cb72-211">If you lose or forget hello passphrase, Microsoft cannot help recover hello backup data.</span></span> <span data-ttu-id="1cb72-212">Сохраните файл hello в безопасном месте.</span><span class="sxs-lookup"><span data-stu-id="1cb72-212">Save hello file in a secure location.</span></span> <span data-ttu-id="1cb72-213">Это обязательный toorestore резервной копии.</span><span class="sxs-lookup"><span data-stu-id="1cb72-213">It is required toorestore a backup.</span></span>
  >
  >

<span data-ttu-id="1cb72-214">Hello агент установлен, и ваш компьютер входит в хранилище зарегистрированного toohello.</span><span class="sxs-lookup"><span data-stu-id="1cb72-214">hello agent is now installed and your machine is registered toohello vault.</span></span> <span data-ttu-id="1cb72-215">Вы будете готовы tooconfigure и расписания резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="1cb72-215">You're ready tooconfigure and schedule your backup.</span></span>

## <a name="network-and-connectivity-requirements"></a><span data-ttu-id="1cb72-216">Требования к сети и подключению</span><span class="sxs-lookup"><span data-stu-id="1cb72-216">Network and Connectivity Requirements</span></span>

<span data-ttu-id="1cb72-217">Если компьютер или прокси-сервера имеет ограниченный доступ к Интернету, обеспечить параметры брандмауэра на компьютере hello и прокси-hello настроенных tooallow следующие URL-адреса:</span><span class="sxs-lookup"><span data-stu-id="1cb72-217">If your machine/proxy has limited internet access, ensure that firewall settings on hello machine/proxy are configured tooallow hello following URLs:</span></span> <br>
    1. <span data-ttu-id="1cb72-218">www.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="1cb72-218">www.msftncsi.com</span></span>
    2. <span data-ttu-id="1cb72-219">*.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="1cb72-219">*.Microsoft.com</span></span>
    3. <span data-ttu-id="1cb72-220">*.WindowsAzure.com</span><span class="sxs-lookup"><span data-stu-id="1cb72-220">*.WindowsAzure.com</span></span>
    4. <span data-ttu-id="1cb72-221">*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="1cb72-221">*.microsoftonline.com</span></span>
    5. <span data-ttu-id="1cb72-222">*.windows.net</span><span class="sxs-lookup"><span data-stu-id="1cb72-222">*.windows.ne</span></span>


## <a name="create-hello-backup-policy"></a><span data-ttu-id="1cb72-223">Создание политики резервного копирования hello</span><span class="sxs-lookup"><span data-stu-id="1cb72-223">Create hello backup policy</span></span>
<span data-ttu-id="1cb72-224">политики резервного копирования Hello при hello расписание точки восстановления создаются и hello продолжительность времени хранения точки восстановления hello сохраняются.</span><span class="sxs-lookup"><span data-stu-id="1cb72-224">hello backup policy is hello schedule when recovery points are taken, and hello length of time hello recovery points are retained.</span></span> <span data-ttu-id="1cb72-225">Используйте hello Microsoft Azure Backup agent toocreate hello политику резервного копирования для файлов и папок.</span><span class="sxs-lookup"><span data-stu-id="1cb72-225">Use hello Microsoft Azure Backup agent toocreate hello backup policy for files and folders.</span></span>

### <a name="toocreate-a-backup-schedule"></a><span data-ttu-id="1cb72-226">toocreate расписание резервного копирования</span><span class="sxs-lookup"><span data-stu-id="1cb72-226">toocreate a backup schedule</span></span>
1. <span data-ttu-id="1cb72-227">Откройте агент Microsoft Azure Backup hello.</span><span class="sxs-lookup"><span data-stu-id="1cb72-227">Open hello Microsoft Azure Backup agent.</span></span> <span data-ttu-id="1cb72-228">Его можно найти, выполнив поиск строки **служба архивации Microsoft Azure**на компьютере.</span><span class="sxs-lookup"><span data-stu-id="1cb72-228">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Запустите агент Azure Backup hello](./media/backup-configure-vault/snap-in-search.png)
2. <span data-ttu-id="1cb72-230">В агенте резервного копирования hello **действия** области, нажмите кнопку **планирования резервного копирования** toolaunch hello мастер планирования резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="1cb72-230">In hello Backup agent's **Actions** pane, click **Schedule Backup** toolaunch hello Schedule Backup Wizard.</span></span>

    ![Планирование архивации Windows Server](./media/backup-configure-vault/schedule-first-backup.png)

3. <span data-ttu-id="1cb72-232">На hello **Приступая к работе** страница приветствия мастера расписания архивации нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="1cb72-232">On hello **Getting started** page of hello Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="1cb72-233">На hello **tooBackup выбрать элементы** щелкните **добавить элементы**.</span><span class="sxs-lookup"><span data-stu-id="1cb72-233">On hello **Select Items tooBackup** page, click **Add Items**.</span></span>

  <span data-ttu-id="1cb72-234">Откроется диалоговое окно Выбор элементов Hello.</span><span class="sxs-lookup"><span data-stu-id="1cb72-234">hello Select Items dialog opens.</span></span>

5. <span data-ttu-id="1cb72-235">Выберите hello файлы и папки должны tooprotect и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1cb72-235">Select hello files and folders that you want tooprotect, and then click **OK**.</span></span>
6. <span data-ttu-id="1cb72-236">В hello **tooBackup выбрать элементы** щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="1cb72-236">In hello **Select Items tooBackup** page, click **Next**.</span></span>
7. <span data-ttu-id="1cb72-237">На hello **укажите расписание архивации** , определите расписание резервного копирования hello и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="1cb72-237">On hello **Specify Backup Schedule** page, specify hello backup schedule and click **Next**.</span></span>

    <span data-ttu-id="1cb72-238">Вы можете запланировать ежедневную (не более трех раз в день) или еженедельную архивацию.</span><span class="sxs-lookup"><span data-stu-id="1cb72-238">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Элементы для архивации Windows Server](./media/backup-configure-vault/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="1cb72-240">Дополнительные сведения о как toospecify hello расписание резервного копирования см. в статье hello [резервного копирования Azure используйте tooreplace инфраструктуры ленты](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="1cb72-240">For more information about how toospecify hello backup schedule, see hello article [Use Azure Backup tooreplace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >

8. <span data-ttu-id="1cb72-241">На hello **выбрать политику хранения** , выберите hello hello политики хранения, определенных для hello резервной копии и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="1cb72-241">On hello **Select Retention Policy** page, choose hello specific retention policies hello for hello backup copy and click **Next**.</span></span>

    <span data-ttu-id="1cb72-242">Политика хранения Hello задает длительность hello, какие hello архива.</span><span class="sxs-lookup"><span data-stu-id="1cb72-242">hello retention policy specifies hello duration which hello backup is stored.</span></span> <span data-ttu-id="1cb72-243">Вместо того чтобы просто задавать «плоский политика» для всех точек резервного копирования, можно указать при архивации hello на основе политик крепления.</span><span class="sxs-lookup"><span data-stu-id="1cb72-243">Rather than just specifying a “flat policy” for all backup points, you can specify different retention policies based on when hello backup occurs.</span></span> <span data-ttu-id="1cb72-244">Вы можете изменить toomeet политики хранения ежедневно, еженедельно, ежемесячно и ежегодно hello вашим потребностям.</span><span class="sxs-lookup"><span data-stu-id="1cb72-244">You can modify hello daily, weekly, monthly, and yearly retention policies toomeet your needs.</span></span>
9. <span data-ttu-id="1cb72-245">На странице выберите тип начального архива hello выберите тип начального архива hello.</span><span class="sxs-lookup"><span data-stu-id="1cb72-245">On hello Choose Initial Backup Type page, choose hello initial backup type.</span></span> <span data-ttu-id="1cb72-246">Оставьте параметр hello **автоматически по сети hello** , а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="1cb72-246">Leave hello option **Automatically over hello network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="1cb72-247">Резервное копирование автоматически hello сети или автономно резервное копирование.</span><span class="sxs-lookup"><span data-stu-id="1cb72-247">You can back up automatically over hello network, or you can back up offline.</span></span> <span data-ttu-id="1cb72-248">Hello в этой статье описываются hello процесс резервного копирования автоматически.</span><span class="sxs-lookup"><span data-stu-id="1cb72-248">hello remainder of this article describes hello process for backing up automatically.</span></span> <span data-ttu-id="1cb72-249">Если вы предпочитаете toodo автономной резервной копии, изучите статью hello [автономного резервного копирования рабочего процесса в службе архивации Azure](backup-azure-backup-import-export.md) для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="1cb72-249">If you prefer toodo an offline backup, review hello article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="1cb72-250">На странице подтверждения hello, просмотрите сведения hello и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="1cb72-250">On hello Confirmation page, review hello information, and then click **Finish**.</span></span>
11. <span data-ttu-id="1cb72-251">После завершения работы мастера hello, создания расписания резервного копирования hello, нажмите кнопку **закрыть**.</span><span class="sxs-lookup"><span data-stu-id="1cb72-251">After hello wizard finishes creating hello backup schedule, click **Close**.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="1cb72-252">Включение регулирования сети</span><span class="sxs-lookup"><span data-stu-id="1cb72-252">Enable network throttling</span></span>
<span data-ttu-id="1cb72-253">Hello агента службы архивации Microsoft Azure предоставляет регулирования сети.</span><span class="sxs-lookup"><span data-stu-id="1cb72-253">hello Microsoft Azure Backup agent provides network throttling.</span></span> <span data-ttu-id="1cb72-254">Регулирование управляет тем, как пропускная способность сети используется во время передачи данных.</span><span class="sxs-lookup"><span data-stu-id="1cb72-254">Throttling controls how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="1cb72-255">Этот элемент управления может пригодиться, если вам требуется tooback копирование данных в рабочее время, но не требуется toointerfere hello процесс резервного копирования с другими Интернет-трафика.</span><span class="sxs-lookup"><span data-stu-id="1cb72-255">This control can be helpful if you need tooback up data during work hours but do not want hello backup process toointerfere with other Internet traffic.</span></span> <span data-ttu-id="1cb72-256">Регулирование применяет tooback копирование и восстановление действий.</span><span class="sxs-lookup"><span data-stu-id="1cb72-256">Throttling applies tooback up and restore activities.</span></span>

> [!NOTE]
> <span data-ttu-id="1cb72-257">Регулирование сети недоступно в Windows Server 2008 R2 с пакетом обновления 1 (SP1), Windows Server 2008 с пакетом обновления 2 (SP2) или Windows 7 (с пакетами обновления).</span><span class="sxs-lookup"><span data-stu-id="1cb72-257">Network throttling is not available on Windows Server 2008 R2 SP1, Windows Server 2008 SP2, or Windows 7 (with service packs).</span></span> <span data-ttu-id="1cb72-258">регулирования компонентов сети Hello Azure Backup использует качества обслуживания (QoS) hello локальной операционной системе.</span><span class="sxs-lookup"><span data-stu-id="1cb72-258">hello Azure Backup network throttling feature engages Quality of Service (QoS) on hello local operating system.</span></span> <span data-ttu-id="1cb72-259">Хотя резервного копирования Azure можно защитить эти операционные системы, версия hello качества обслуживания, доступные на этих платформах не работает с регулирование сети Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="1cb72-259">Though Azure Backup can protect these operating systems, hello version of QoS available on these platforms doesn't work with Azure Backup network throttling.</span></span> <span data-ttu-id="1cb72-260">Регулирование сети можно использовать во всех остальных [поддерживаемых операционных системах](backup-azure-backup-faq.md).</span><span class="sxs-lookup"><span data-stu-id="1cb72-260">Network throttling can be used on all other [supported operating systems](backup-azure-backup-faq.md).</span></span>
>
>

<span data-ttu-id="1cb72-261">**Регулирование сети tooenable**</span><span class="sxs-lookup"><span data-stu-id="1cb72-261">**tooenable network throttling**</span></span>

1. <span data-ttu-id="1cb72-262">В агенте службы архивации Microsoft Azure hello, нажмите кнопку **изменить свойства**.</span><span class="sxs-lookup"><span data-stu-id="1cb72-262">In hello Microsoft Azure Backup agent, click **Change Properties**.</span></span>

    ![Изменить свойства](./media/backup-configure-vault/change-properties.png)
2. <span data-ttu-id="1cb72-264">На hello **регулирование** вкладке, выберите hello **включить регулирования для операций резервного копирования использование пропускной способности Интернета** флажок.</span><span class="sxs-lookup"><span data-stu-id="1cb72-264">On hello **Throttling** tab, select hello **Enable internet bandwidth usage throttling for backup operations** check box.</span></span>

    ![Регулирование сети](./media/backup-configure-vault/throttling-dialog.png)
3. <span data-ttu-id="1cb72-266">После включения регулирования, укажите допустимый пропускной способности, для передачи во время резервного копирования данных hello **рабочие часы** и **нерабочие часы**.</span><span class="sxs-lookup"><span data-stu-id="1cb72-266">After you have enabled throttling, specify hello allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="1cb72-267">значения Hello пропускной способности начинаются с 512 килобит в секунду (Кбит/с) и можно перейти вверх too1 023 мегабайт в секунду (Мбит/с).</span><span class="sxs-lookup"><span data-stu-id="1cb72-267">hello bandwidth values begin at 512 kilobits per second (Kbps) and can go up too1,023 megabytes per second (MBps).</span></span> <span data-ttu-id="1cb72-268">Можно также назначить hello начала и окончания для **рабочие часы**, и какие дни недели hello будут рассматриваться как рабочие дни.</span><span class="sxs-lookup"><span data-stu-id="1cb72-268">You can also designate hello start and finish for **Work hours**, and which days of hello week are considered work days.</span></span> <span data-ttu-id="1cb72-269">Время, не входящее в назначенные рабочие часы, считается нерабочим.</span><span class="sxs-lookup"><span data-stu-id="1cb72-269">Hours outside of designated work hours are considered non-work hours.</span></span>
4. <span data-ttu-id="1cb72-270">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1cb72-270">Click **OK**.</span></span>

### <a name="tooback-up-files-and-folders-for-hello-first-time"></a><span data-ttu-id="1cb72-271">tooback копирования файлов и папок для hello первый раз</span><span class="sxs-lookup"><span data-stu-id="1cb72-271">tooback up files and folders for hello first time</span></span>
1. <span data-ttu-id="1cb72-272">В hello резервного копирования, нажмите кнопку **Архивировать** toocomplete hello начального заполнения hello сети.</span><span class="sxs-lookup"><span data-stu-id="1cb72-272">In hello backup agent, click **Back Up Now** toocomplete hello initial seeding over hello network.</span></span>

    ![Моментальная архивация Windows Server](./media/backup-configure-vault/backup-now.png)
2. <span data-ttu-id="1cb72-274">На странице подтверждения hello просмотрите параметры hello hello мастер немедленной архивации будет использовать tooback машину hello.</span><span class="sxs-lookup"><span data-stu-id="1cb72-274">On hello Confirmation page, review hello settings that hello Back Up Now Wizard will use tooback up hello machine.</span></span> <span data-ttu-id="1cb72-275">Затем нажмите кнопку **Архивировать**.</span><span class="sxs-lookup"><span data-stu-id="1cb72-275">Then click **Back Up**.</span></span>
3. <span data-ttu-id="1cb72-276">Нажмите кнопку **закрыть** tooclose приветствия мастера.</span><span class="sxs-lookup"><span data-stu-id="1cb72-276">Click **Close** tooclose hello wizard.</span></span> <span data-ttu-id="1cb72-277">Если в этом случае до завершения процесса резервного копирования hello приветствия мастера продолжается toorun в фоновом режиме hello.</span><span class="sxs-lookup"><span data-stu-id="1cb72-277">If you do this before hello backup process finishes, hello wizard continues toorun in hello background.</span></span>

<span data-ttu-id="1cb72-278">После завершения начальной резервной копии hello hello **задание завершено** состояние отображается в консоли hello резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="1cb72-278">After hello initial backup is completed, hello **Job completed** status appears in hello Backup console.</span></span>

![Первоначальное восстановление завершено](./media/backup-configure-vault/ircomplete.png)

## <a name="questions"></a><span data-ttu-id="1cb72-280">Вопросы?</span><span class="sxs-lookup"><span data-stu-id="1cb72-280">Questions?</span></span>
<span data-ttu-id="1cb72-281">Если у вас есть вопросы или при наличии любой возможности, хотелось бы включены, toosee [отправить отзыв](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="1cb72-281">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1cb72-282">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1cb72-282">Next steps</span></span>
<span data-ttu-id="1cb72-283">Дополнительные сведения об архивации виртуальных машин и других рабочих нагрузок см. в следующих разделах:</span><span class="sxs-lookup"><span data-stu-id="1cb72-283">For additional information about backing up VMs or other workloads, see:</span></span>

* <span data-ttu-id="1cb72-284">Теперь, когда вы выполнили резервное копирование файлов и папок, вы можете [управлять хранилищами и серверами](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="1cb72-284">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="1cb72-285">Если вам требуется toorestore резервной копии, используйте в этой статье слишком[восстановить компьютер Windows tooa файлы](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="1cb72-285">If you need toorestore a backup, use this article too[restore files tooa Windows machine](backup-azure-restore-windows-server.md).</span></span>
