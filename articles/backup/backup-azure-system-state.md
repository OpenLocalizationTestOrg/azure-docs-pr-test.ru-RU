---
title: "Резервное копирование состояния системы Windows в Azure | Документация Майкрософт"
description: "Узнайте, как выполнить резервное копирование состояния системы компьютеров Windows Server и/или Windows в Azure."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: carmonm
editor: 
keywords: "как выполнять резервное копирование, резервное копирование файлов и папок"
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: saurse;markgal
ms.openlocfilehash: 6fbd96935f444d8b0c6d068ebd0d28e612f19816
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="back-up-windows-system-state-in-resource-manager-deployment"></a><span data-ttu-id="27f62-104">Резервное копирование состояния системы Windows с использованием модели развертывания Resource Manager</span><span class="sxs-lookup"><span data-stu-id="27f62-104">Back up Windows system state in Resource Manager deployment</span></span>
<span data-ttu-id="27f62-105">В этой статье описано, как выполнить резервное копирование состояния системы Windows Server в Azure.</span><span class="sxs-lookup"><span data-stu-id="27f62-105">This article explains how to back up your Windows Server system state to Azure.</span></span> <span data-ttu-id="27f62-106">В этом руководстве приведены общие сведения,</span><span class="sxs-lookup"><span data-stu-id="27f62-106">It's a tutorial intended to walk you through the basics.</span></span>

<span data-ttu-id="27f62-107">Дополнительные сведения о службе архивации Azure см. в этом [обзоре](backup-introduction-to-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="27f62-107">If you want to know more about Azure Backup, read this [overview](backup-introduction-to-azure-backup.md).</span></span>

<span data-ttu-id="27f62-108">Если у вас нет подписки Azure, вы можете создать [бесплатную учетную запись](https://azure.microsoft.com/free/), предоставляющую доступ ко всем службам Azure.</span><span class="sxs-lookup"><span data-stu-id="27f62-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) that lets you access any Azure service.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="27f62-109">Создание хранилища служб восстановления</span><span class="sxs-lookup"><span data-stu-id="27f62-109">Create a recovery services vault</span></span>
<span data-ttu-id="27f62-110">Для резервного копирования файлов и папок нужно создать хранилище служб восстановления в том регионе, в котором планируется хранить данные.</span><span class="sxs-lookup"><span data-stu-id="27f62-110">To back up your files and folders, you need to create a Recovery Services vault in the region where you want to store the data.</span></span> <span data-ttu-id="27f62-111">Кроме того, необходимо определить способ репликации хранилища.</span><span class="sxs-lookup"><span data-stu-id="27f62-111">You also need to determine how you want your storage replicated.</span></span>

### <a name="to-create-a-recovery-services-vault"></a><span data-ttu-id="27f62-112">Создание хранилища служб восстановления</span><span class="sxs-lookup"><span data-stu-id="27f62-112">To create a Recovery Services vault</span></span>
1. <span data-ttu-id="27f62-113">Используя подписку Azure, войдите на [портал Azure](https://portal.azure.com/) (если вы еще этого не сделали).</span><span class="sxs-lookup"><span data-stu-id="27f62-113">If you haven't already done so, sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="27f62-114">В главном меню щелкните **Другие службы**, а затем в списке ресурсов введите **Службы восстановления** и щелкните **Хранилища служб восстановления**.</span><span class="sxs-lookup"><span data-stu-id="27f62-114">On the Hub menu, click **More services** and in the list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Создание хранилища служб восстановления — шаг 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="27f62-116">Если в подписке есть хранилища служб восстановления, они отобразятся в списке.</span><span class="sxs-lookup"><span data-stu-id="27f62-116">If there are recovery services vaults in the subscription, the vaults are listed.</span></span>
3. <span data-ttu-id="27f62-117">В меню **Хранилища служб восстановления** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="27f62-117">On the **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Создание хранилища служб восстановления — шаг 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="27f62-119">Откроется колонка хранилища служб восстановления, в которой нужно указать **имя**, **подписку**, **группу ресурсов** и **расположение**.</span><span class="sxs-lookup"><span data-stu-id="27f62-119">The Recovery Services vault blade opens, prompting you to provide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Создание хранилища служб восстановления — шаг 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="27f62-121">В поле **Имя**введите понятное имя хранилища.</span><span class="sxs-lookup"><span data-stu-id="27f62-121">For **Name**, enter a friendly name to identify the vault.</span></span> <span data-ttu-id="27f62-122">Имя должно быть уникальным в пределах подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="27f62-122">The name needs to be unique for the Azure subscription.</span></span> <span data-ttu-id="27f62-123">Введите имя длиной от 2 до 50 знаков.</span><span class="sxs-lookup"><span data-stu-id="27f62-123">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="27f62-124">Имя должно начинаться с буквы, оно может содержать только буквы, цифры и дефисы.</span><span class="sxs-lookup"><span data-stu-id="27f62-124">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="27f62-125">В разделе **Подписка** в раскрывающемся меню выберите подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="27f62-125">In the **Subscription** section, use the drop-down menu to choose the Azure subscription.</span></span> <span data-ttu-id="27f62-126">Если вы используете только одну подписку, она уже отображается и вы можете перейти к следующему шагу.</span><span class="sxs-lookup"><span data-stu-id="27f62-126">If you use only one subscription, that subscription appears and you can skip to the next step.</span></span> <span data-ttu-id="27f62-127">Если неизвестно, какую подписку нужно использовать, оставьте подписку по умолчанию (или предлагаемую подписку).</span><span class="sxs-lookup"><span data-stu-id="27f62-127">If you are not sure which subscription to use, use the default (or suggested) subscription.</span></span> <span data-ttu-id="27f62-128">Вариантов будет несколько только в том случае, если учетная запись вашей организации связана с несколькими подписками Azure.</span><span class="sxs-lookup"><span data-stu-id="27f62-128">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="27f62-129">В разделе **Группа ресурсов** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="27f62-129">In the **Resource group** section:</span></span>

    * <span data-ttu-id="27f62-130">выберите **Создать**, если вы хотите создать группу ресурсов;</span><span class="sxs-lookup"><span data-stu-id="27f62-130">select **Create new** if you want to create a Resource group.</span></span>
    <span data-ttu-id="27f62-131">Или</span><span class="sxs-lookup"><span data-stu-id="27f62-131">Or</span></span>
    * <span data-ttu-id="27f62-132">выберите **Использовать существующий** и просмотрите список доступных групп ресурсов в раскрывающемся меню.</span><span class="sxs-lookup"><span data-stu-id="27f62-132">select **Use existing** and click the drop-down menu to see the available list of Resource groups.</span></span>

  <span data-ttu-id="27f62-133">Дополнительные сведения о группах ресурсов см. в статье [Общие сведения об Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="27f62-133">For complete information on Resource groups, see the [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="27f62-134">В поле **Расположение** выберите географический регион, в котором будет находиться хранилище.</span><span class="sxs-lookup"><span data-stu-id="27f62-134">Click **Location** to select the geographic region for the vault.</span></span> <span data-ttu-id="27f62-135">Этот выбор определяет географический регион, в который будут отправляться данные архивации.</span><span class="sxs-lookup"><span data-stu-id="27f62-135">This choice determines the geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="27f62-136">В нижней части колонки "Хранилище служб восстановления" нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="27f62-136">At the bottom of the Recovery Services vault blade, click **Create**.</span></span>

    <span data-ttu-id="27f62-137">Создание хранилища служб восстановления может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="27f62-137">It can take several minutes for the Recovery Services vault to be created.</span></span> <span data-ttu-id="27f62-138">Следите за уведомлениями о состоянии на портале в верхней правой области.</span><span class="sxs-lookup"><span data-stu-id="27f62-138">Monitor the status notifications in the upper right-hand area of the portal.</span></span> <span data-ttu-id="27f62-139">После создания хранилище появится в списке хранилищ служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="27f62-139">Once your vault is created, it appears in the list of Recovery Services vaults.</span></span> <span data-ttu-id="27f62-140">Если через несколько минут хранилище не отобразилось, нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="27f62-140">If after several minutes you don't see your vault, click **Refresh**.</span></span>

    ![Кнопка "Обновить"](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    <span data-ttu-id="27f62-142">Как только хранилище отобразится в списке хранилищ служб восстановления, для него можно определить избыточность.</span><span class="sxs-lookup"><span data-stu-id="27f62-142">Once you see your vault in the list of Recovery Services vaults, you are ready to set the storage redundancy.</span></span>

### <a name="set-storage-redundancy-for-the-vault"></a><span data-ttu-id="27f62-143">Настройка избыточности хранилища</span><span class="sxs-lookup"><span data-stu-id="27f62-143">Set storage redundancy for the vault</span></span>
<span data-ttu-id="27f62-144">При создании хранилища служб восстановления настройте его избыточность в соответствии со своими потребностями.</span><span class="sxs-lookup"><span data-stu-id="27f62-144">When you create a Recovery Services vault, make sure storage redundancy is configured the way you want.</span></span>

1. <span data-ttu-id="27f62-145">В колонке **Хранилища служб восстановления** щелкните новое хранилище.</span><span class="sxs-lookup"><span data-stu-id="27f62-145">From the **Recovery Services vaults** blade, click the new vault.</span></span>

    ![Выбор нового хранилища в списке хранилищ служб восстановления](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="27f62-147">При выборе хранилища колонка **Хранилище служб восстановления** сужается и открывается колонка параметров (*с именем хранилища вверху*), а также колонка со сведениями о хранилище.</span><span class="sxs-lookup"><span data-stu-id="27f62-147">When you select the vault, the **Recovery Services vault** blade narrows, and the Settings blade (*which has the name of the vault at the top*) and the vault details blade open.</span></span>

    ![Просмотр конфигурации нового хранилища](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. <span data-ttu-id="27f62-149">В колонке параметров нового хранилища прокрутите с помощью вертикального ползунка вниз к разделу "Управление" и щелкните **Инфраструктура резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="27f62-149">In the new vault's Settings blade, use the vertical slide to scroll down to the Manage section, and click **Backup Infrastructure**.</span></span>
    <span data-ttu-id="27f62-150">Откроется колонка инфраструктуры резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="27f62-150">The Backup Infrastructure blade opens.</span></span>
3. <span data-ttu-id="27f62-151">В этой колонке выберите **Инфраструктура резервного копирования**, чтобы открыть колонку **Конфигурация архивации**.</span><span class="sxs-lookup"><span data-stu-id="27f62-151">In the Backup Infrastructure blade, click **Backup Configuration** to open the **Backup Configuration** blade.</span></span>

    ![Настройка конфигурации для нового хранилища](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. <span data-ttu-id="27f62-153">Выберите нужный тип репликации для хранилища.</span><span class="sxs-lookup"><span data-stu-id="27f62-153">Choose the appropriate storage replication option for your vault.</span></span>

    ![Варианты конфигурации хранилища](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    <span data-ttu-id="27f62-155">По умолчанию это геоизбыточное хранилище.</span><span class="sxs-lookup"><span data-stu-id="27f62-155">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="27f62-156">Если в качестве конечной точки основного хранилища службы архивации используется Azure, выберите **геоизбыточное хранилище**,</span><span class="sxs-lookup"><span data-stu-id="27f62-156">If you use Azure as a primary backup storage endpoint, continue to use **Geo-redundant**.</span></span> <span data-ttu-id="27f62-157">а если нет, — **локально избыточное** (это позволит снизить плату за хранилище Azure).</span><span class="sxs-lookup"><span data-stu-id="27f62-157">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces the Azure storage costs.</span></span> <span data-ttu-id="27f62-158">Дополнительные сведения о [геоизбыточном](../storage/common/storage-redundancy.md#geo-redundant-storage) и [локально избыточном](../storage/common/storage-redundancy.md#locally-redundant-storage) хранилищах см. в статье [Репликация службы хранилища Azure](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="27f62-158">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="27f62-159">Теперь, когда вы создали хранилище, настройте в нем резервное копирование состояния системы Windows.</span><span class="sxs-lookup"><span data-stu-id="27f62-159">Now that you've created a vault, configure it for backing up Windows System State.</span></span>

## <a name="configure-the-vault"></a><span data-ttu-id="27f62-160">Настройка хранилища</span><span class="sxs-lookup"><span data-stu-id="27f62-160">Configure the vault</span></span>
1. <span data-ttu-id="27f62-161">В колонке хранилища служб восстановления (хранилища, которое вы только что создали) в разделе "Начало работы" выберите **Резервное копирование**. Затем в колонке **Начало работы с резервным копированием** выберите **Цель резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="27f62-161">On the Recovery Services vault blade (for the vault you just created), in the Getting Started section, click **Backup**, then on the **Getting Started with Backup** blade, select **Backup goal**.</span></span>

    ![Открытая колонка цели резервного копирования](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    <span data-ttu-id="27f62-163">Откроется колонка **Цель резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="27f62-163">The **Backup Goal** blade opens.</span></span>

    ![Открытая колонка цели резервного копирования](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="27f62-165">В раскрывающемся меню **Где выполняется рабочая нагрузка?** выберите **Локально**.</span><span class="sxs-lookup"><span data-stu-id="27f62-165">From the **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

    <span data-ttu-id="27f62-166">Вы выбираете параметр **Локально**, потому что ваш компьютер Windows Server или Windows — это физический компьютер, которые не находится в Azure.</span><span class="sxs-lookup"><span data-stu-id="27f62-166">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="27f62-167">В меню **Что вы хотите резервировать?** выберите **Состояние системы** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="27f62-167">From the **What do you want to backup?** menu, select **System State**, and click **OK**.</span></span>

    ![Настройка резервного копирования файлов и папок](./media/backup-azure-system-state/backup-goal-system-state.png)

    <span data-ttu-id="27f62-169">После того как вы нажмете кнопку "ОК", рядом с параметром **Цель резервного копирования** появится флажок и откроется колонка **Подготовка инфраструктуры**.</span><span class="sxs-lookup"><span data-stu-id="27f62-169">After clicking OK, a checkmark appears next to **Backup goal**, and the **Prepare infrastructure** blade opens.</span></span>

    ![Цель резервного копирования настроена, на очереди подготовка инфраструктуры](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="27f62-171">В колонке **Подготовка инфраструктуры** щелкните **Скачать агент для Windows Server или Windows Client**.</span><span class="sxs-lookup"><span data-stu-id="27f62-171">On the **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

    ![Download Agent for Windows Server or Windows Client](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    <span data-ttu-id="27f62-173">Если вы используете Windows Server Essential, выберите загрузку агента для Windows Server Essential.</span><span class="sxs-lookup"><span data-stu-id="27f62-173">If you are using Windows Server Essential, then choose to download the agent for Windows Server Essential.</span></span> <span data-ttu-id="27f62-174">Во всплывающем меню появится запрос на запуск или сохранение файла MARSAgentInstaller.exe.</span><span class="sxs-lookup"><span data-stu-id="27f62-174">A pop-up menu prompts you to run or save MARSAgentInstaller.exe.</span></span>

    ![Диалоговое окно MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="27f62-176">Во всплывающем окне скачивания нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="27f62-176">In the download pop-up menu, click **Save**.</span></span>

    <span data-ttu-id="27f62-177">По умолчанию файл **MARSagentinstaller.exe** сохраняется в папке для скачивания.</span><span class="sxs-lookup"><span data-stu-id="27f62-177">By default, the **MARSagentinstaller.exe** file is saved to your Downloads folder.</span></span> <span data-ttu-id="27f62-178">После завершения установки появится всплывающее окно с двумя вариантами действий: запустить установщик или открыть папку.</span><span class="sxs-lookup"><span data-stu-id="27f62-178">When the installer completes, you will see a pop-up asking if you want to run the installer, or open the folder.</span></span>

    ![Download Agent for Windows Server or Windows Client](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    <span data-ttu-id="27f62-180">Пока не нужно устанавливать агент.</span><span class="sxs-lookup"><span data-stu-id="27f62-180">You don't need to install the agent yet.</span></span> <span data-ttu-id="27f62-181">Его можно установить после скачивания учетных данных хранилища.</span><span class="sxs-lookup"><span data-stu-id="27f62-181">You can install the agent after you have downloaded the vault credentials.</span></span>

6. <span data-ttu-id="27f62-182">В колонке **Подготовка инфраструктуры** щелкните **Скачать**.</span><span class="sxs-lookup"><span data-stu-id="27f62-182">On the **Prepare infrastructure** blade, click **Download**.</span></span>

    ![Скачивание учетных данных хранилища](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    <span data-ttu-id="27f62-184">Учетные данные хранилища будут сохранены в папке "Загрузки".</span><span class="sxs-lookup"><span data-stu-id="27f62-184">The vault credentials download to your Downloads folder.</span></span> <span data-ttu-id="27f62-185">После этого вы увидите всплывающее окно с двумя вариантами действий: открыть или сохранить учетные данные.</span><span class="sxs-lookup"><span data-stu-id="27f62-185">After the vault credentials finish downloading, you see a pop-up asking if you want to open or save the credentials.</span></span> <span data-ttu-id="27f62-186">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="27f62-186">Click **Save**.</span></span> <span data-ttu-id="27f62-187">Если вы случайно нажали кнопку **Открыть**, подождите, пока попытка открыть учетные данные хранилища закончится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="27f62-187">If you accidentally click **Open**, let the dialog that attempts to open the vault credentials, fail.</span></span> <span data-ttu-id="27f62-188">Вы не можете открыть учетные данные хранилища.</span><span class="sxs-lookup"><span data-stu-id="27f62-188">You cannot open the vault credentials.</span></span> <span data-ttu-id="27f62-189">Перейдите к следующему шагу.</span><span class="sxs-lookup"><span data-stu-id="27f62-189">Proceed to the next step.</span></span> <span data-ttu-id="27f62-190">Учетные данные хранилища находятся в папке "Загрузки".</span><span class="sxs-lookup"><span data-stu-id="27f62-190">The vault credentials are in the Downloads folder.</span></span>   

    ![Загрузка учетных данных хранилища завершена](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-the-agent"></a><span data-ttu-id="27f62-192">Установка и регистрация агента</span><span class="sxs-lookup"><span data-stu-id="27f62-192">Install and register the agent</span></span>

> [!NOTE]
> <span data-ttu-id="27f62-193">Параметр для включения резервного копирования на портале Azure пока недоступен.</span><span class="sxs-lookup"><span data-stu-id="27f62-193">Enabling backup through the Azure portal is not available, yet.</span></span> <span data-ttu-id="27f62-194">Используйте агент служб восстановления Microsoft Azure для резервного копирования состояния системы Windows Server.</span><span class="sxs-lookup"><span data-stu-id="27f62-194">Use the Microsoft Azure Recovery Services Agent to back up Windows Server System State.</span></span>
>

1. <span data-ttu-id="27f62-195">Найдите и дважды щелкните файл **MARSagentinstaller.exe** в папке "Загрузки" (или в другом расположении).</span><span class="sxs-lookup"><span data-stu-id="27f62-195">Locate and double-click the **MARSagentinstaller.exe** from the Downloads folder (or other saved location).</span></span>

    <span data-ttu-id="27f62-196">В установщике будут отображаться соответствующие сообщения по мере извлечения, установки и регистрации агента служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="27f62-196">The installer provides a series of messages as it extracts, installs, and registers the Recovery Services agent.</span></span>

    ![Запуск установщика агента служб восстановления](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="27f62-198">Выполните шаги мастера настройки агента служб восстановления Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="27f62-198">Complete the Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="27f62-199">Для завершения работы с мастерам вам нужно:</span><span class="sxs-lookup"><span data-stu-id="27f62-199">To complete the wizard, you need to:</span></span>

   * <span data-ttu-id="27f62-200">Выбрать папку установки и папку кэша.</span><span class="sxs-lookup"><span data-stu-id="27f62-200">Choose a location for the installation and cache folder.</span></span>
   * <span data-ttu-id="27f62-201">Если для подключения к Интернету используется прокси-сервер, указать данные прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="27f62-201">Provide your proxy server info if you use a proxy server to connect to the internet.</span></span>
   * <span data-ttu-id="27f62-202">Если используется прокси-сервер, прошедший проверку подлинности, ввести имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="27f62-202">Provide your user name and password details if you use an authenticated proxy.</span></span>
   * <span data-ttu-id="27f62-203">Указать скачанные учетные данные хранилища.</span><span class="sxs-lookup"><span data-stu-id="27f62-203">Provide the downloaded vault credentials</span></span>
   * <span data-ttu-id="27f62-204">Сохранить парольную фразу шифрования в безопасном месте.</span><span class="sxs-lookup"><span data-stu-id="27f62-204">Save the encryption passphrase in a secure location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="27f62-205">Если вы потеряли или забыли парольную фразу, корпорация Майкрософт не сможет помочь вам восстановить резервную копию данных.</span><span class="sxs-lookup"><span data-stu-id="27f62-205">If you lose or forget the passphrase, Microsoft cannot help recover the backup data.</span></span> <span data-ttu-id="27f62-206">Сохраните файл в безопасном месте,</span><span class="sxs-lookup"><span data-stu-id="27f62-206">Save the file in a secure location.</span></span> <span data-ttu-id="27f62-207">так как он потребуется для восстановления резервной копии.</span><span class="sxs-lookup"><span data-stu-id="27f62-207">It is required to restore a backup.</span></span>
     >
     >

<span data-ttu-id="27f62-208">Теперь, когда агент установлен и компьютер зарегистрирован в хранилище,</span><span class="sxs-lookup"><span data-stu-id="27f62-208">The agent is now installed and your machine is registered to the vault.</span></span> <span data-ttu-id="27f62-209">вы можете настроить параметры резервного копирования, в том числе расписание.</span><span class="sxs-lookup"><span data-stu-id="27f62-209">You're ready to configure and schedule your backup.</span></span>

## <a name="back-up-windows-server-system-state-preview"></a><span data-ttu-id="27f62-210">Состояние резервного копирования системы Windows Server (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="27f62-210">Back up Windows Server System State (Preview)</span></span>
<span data-ttu-id="27f62-211">Начальное резервное копирование включает в себя три задачи:</span><span class="sxs-lookup"><span data-stu-id="27f62-211">The initial backup includes three tasks:</span></span>

* <span data-ttu-id="27f62-212">включение резервного копирования состояния системы с помощью агента службы Azure Backup;</span><span class="sxs-lookup"><span data-stu-id="27f62-212">Enable System State Backup using the Azure Backup agent</span></span>
* <span data-ttu-id="27f62-213">Планирование архивации</span><span class="sxs-lookup"><span data-stu-id="27f62-213">Schedule the backup</span></span>
* <span data-ttu-id="27f62-214">архивация файлов и папок впервые.</span><span class="sxs-lookup"><span data-stu-id="27f62-214">Back up files and folders for the first time</span></span>

<span data-ttu-id="27f62-215">Чтобы выполнить первоначальное резервное копирование, используйте агент служб восстановления Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="27f62-215">To complete the initial backup, use the Microsoft Azure Recovery Services agent.</span></span>

### <a name="to-enable-system-state-backup-using-the-azure-backup-agent"></a><span data-ttu-id="27f62-216">Включение резервного копирования состояния системы с помощью агента службы Azure Backup</span><span class="sxs-lookup"><span data-stu-id="27f62-216">To enable System State backup using the Azure Backup agent</span></span>

1. <span data-ttu-id="27f62-217">В сеансе PowerShell выполните указанную ниже команду, чтобы остановить работу модуля резервного копирования Azure.</span><span class="sxs-lookup"><span data-stu-id="27f62-217">In a PowerShell session, run the following command to stop the Azure Backup engine.</span></span>

  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="27f62-218">Откройте реестр Windows.</span><span class="sxs-lookup"><span data-stu-id="27f62-218">Open the Windows Registry.</span></span>

  ```
  PS C:\> regedit.exe
  ```

3. <span data-ttu-id="27f62-219">Добавьте следующий раздел реестра с заданным значением DWORD.</span><span class="sxs-lookup"><span data-stu-id="27f62-219">Add the following registry key with the specified DWord Value.</span></span>

  | <span data-ttu-id="27f62-220">Путь к элементу реестра</span><span class="sxs-lookup"><span data-stu-id="27f62-220">Registry path</span></span> | <span data-ttu-id="27f62-221">Раздел реестра</span><span class="sxs-lookup"><span data-stu-id="27f62-221">Registry key</span></span> | <span data-ttu-id="27f62-222">Значение DWORD</span><span class="sxs-lookup"><span data-stu-id="27f62-222">DWord value</span></span> |
  |---------------|--------------|-------------|
  | <span data-ttu-id="27f62-223">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span><span class="sxs-lookup"><span data-stu-id="27f62-223">HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span></span> | <span data-ttu-id="27f62-224">TurnOffSSBFeature</span><span class="sxs-lookup"><span data-stu-id="27f62-224">TurnOffSSBFeature</span></span> | <span data-ttu-id="27f62-225">2</span><span class="sxs-lookup"><span data-stu-id="27f62-225">2</span></span> |

4. <span data-ttu-id="27f62-226">Перезапустите модуль резервного копирования, выполнив следующую команду в командной строке с повышенными привилегиями:</span><span class="sxs-lookup"><span data-stu-id="27f62-226">Restart the Backup engine by executing the following command in an elevated command prompt.</span></span>

  ```
  PS C:\> Net start obengine
  ```

### <a name="to-schedule-the-backup-job"></a><span data-ttu-id="27f62-227">Планирование задания резервного копирования</span><span class="sxs-lookup"><span data-stu-id="27f62-227">To schedule the backup job</span></span>

1. <span data-ttu-id="27f62-228">Откройте агент служб восстановления Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="27f62-228">Open the Microsoft Azure Recovery Services agent.</span></span> <span data-ttu-id="27f62-229">Его можно найти, выполнив поиск строки **служба архивации Microsoft Azure**на компьютере.</span><span class="sxs-lookup"><span data-stu-id="27f62-229">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Запуск агента служб восстановления Azure](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)

2. <span data-ttu-id="27f62-231">В агенте служб восстановления щелкните **Создать расписание архивации**.</span><span class="sxs-lookup"><span data-stu-id="27f62-231">In the Recovery Services agent, click **Schedule Backup**.</span></span>

    ![Планирование архивации Windows Server](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)

3. <span data-ttu-id="27f62-233">На странице "Приступая к работе" в мастере планирования архивации нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="27f62-233">On the Getting started page of the Schedule Backup Wizard, click **Next**.</span></span>

4. <span data-ttu-id="27f62-234">На странице "Выбор элементов для архивации" щелкните **Добавить элементы**.</span><span class="sxs-lookup"><span data-stu-id="27f62-234">On the Select Items to Backup page, click **Add Items**.</span></span>

5. <span data-ttu-id="27f62-235">Выберите **Состояние системы** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="27f62-235">Select **System State** and then click **OK**.</span></span>

6. <span data-ttu-id="27f62-236">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="27f62-236">Click **Next**.</span></span>

7. <span data-ttu-id="27f62-237">Резервное копирование и сохранение состояния системы автоматически выполняется каждое воскресенье в 21:00 по местному времени. Срок хранения составляет 60 дней.</span><span class="sxs-lookup"><span data-stu-id="27f62-237">The System State Backup and Retention schedule is automatically set to back up every Sunday at 9:00 PM local time, and the retention period is set to 60 days.</span></span>

   > [!NOTE]
   > <span data-ttu-id="27f62-238">Политики резервного копирования и хранения состояния системы настраиваются автоматически.</span><span class="sxs-lookup"><span data-stu-id="27f62-238">System State backup and retention policy is automatically configured.</span></span> <span data-ttu-id="27f62-239">Если кроме состояния системы Windows Server вы выполняете резервное копирование файлов и папок, укажите только политику резервного копирования и хранения для резервных копий файлов из мастера.</span><span class="sxs-lookup"><span data-stu-id="27f62-239">If you back up Files and Folders in addition to the Windows Server System State, specify only the Backup and Retention policy for file backups from the wizard.</span></span> 
   >

8. <span data-ttu-id="27f62-240">Проверьте сведения на странице подтверждения и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="27f62-240">On the Confirmation page, review the information, and then click **Finish**.</span></span>

9. <span data-ttu-id="27f62-241">Когда мастер завершит создание расписания архивации, нажмите кнопку **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="27f62-241">After the wizard finishes creating the backup schedule, click **Close**.</span></span>

### <a name="to-back-up-windows-server-system-state-for-the-first-time"></a><span data-ttu-id="27f62-242">Первое резервное копирование состояния системы Windows Server</span><span class="sxs-lookup"><span data-stu-id="27f62-242">To back up Windows Server System State for the first time</span></span>

1. <span data-ttu-id="27f62-243">Убедитесь, что для Windows Server нет незавершенных обновлений, которые требуют перезагрузки.</span><span class="sxs-lookup"><span data-stu-id="27f62-243">Make sure there are no pending updates for Windows Server that require a reboot.</span></span>

2. <span data-ttu-id="27f62-244">В агенте служб восстановления щелкните **Выполнить моментальную архивацию**, чтобы завершить начальное заполнение по сети.</span><span class="sxs-lookup"><span data-stu-id="27f62-244">In the Recovery Services agent, click **Back Up Now** to complete the initial seeding over the network.</span></span>

    ![Моментальная архивация Windows Server](./media/backup-try-azure-backup-in-10-mins/backup-now.png)

3. <span data-ttu-id="27f62-246">На странице "Подтверждение" проверьте параметры, которые мастер будет использовать для архивации данных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="27f62-246">On the Confirmation page, review the settings that the Back Up Now Wizard will use to back up the machine.</span></span> <span data-ttu-id="27f62-247">Затем нажмите кнопку **Архивировать**.</span><span class="sxs-lookup"><span data-stu-id="27f62-247">Then click **Back Up**.</span></span>

4. <span data-ttu-id="27f62-248">Нажмите кнопку **Закрыть**, чтобы закрыть мастер.</span><span class="sxs-lookup"><span data-stu-id="27f62-248">Click **Close** to close the wizard.</span></span> <span data-ttu-id="27f62-249">Если сделать это до завершения архивации, мастер продолжит работу в фоновом режиме.</span><span class="sxs-lookup"><span data-stu-id="27f62-249">If you close the wizard before the backup process finishes, the wizard continues to run in the background.</span></span>

5. <span data-ttu-id="27f62-250">Если кроме резервного копирования состояния системы Windows Server вы выполняете резервное копирование файлов и папок на сервере, мастер моментальной архивации будет создавать только резервные копии файлов.</span><span class="sxs-lookup"><span data-stu-id="27f62-250">If you back up Files and Folders on your server, in addition to the Windows Server System State, the Backup Now wizard will only back up files.</span></span> <span data-ttu-id="27f62-251">Для выполнения нерегламентированного резервного копирования состояния системы выполните следующую команду PowerShell:</span><span class="sxs-lookup"><span data-stu-id="27f62-251">To perform an ad hoc System State back up, use the following PowerShell command:</span></span>

    ```
    PS C:\> Start-OBSystemStateBackup
    ```

  <span data-ttu-id="27f62-252">После завершения начальной архивации в консоли службы архивации отобразится состояние **Задание выполнено**.</span><span class="sxs-lookup"><span data-stu-id="27f62-252">After the initial backup is completed, the **Job completed** status appears in the Backup console.</span></span>

  ![Первоначальное восстановление завершено](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="frequently-asked-questions"></a><span data-ttu-id="27f62-254">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="27f62-254">Frequently asked questions</span></span>

<span data-ttu-id="27f62-255">Чтобы получить дополнительные сведения, ознакомьтесь с указанными ниже вопросами и ответами.</span><span class="sxs-lookup"><span data-stu-id="27f62-255">The following questions and answers provide supplementary information.</span></span>

### <a name="what-is-the-staging-volume"></a><span data-ttu-id="27f62-256">Что такое промежуточный том?</span><span class="sxs-lookup"><span data-stu-id="27f62-256">What is the Staging Volume?</span></span>

<span data-ttu-id="27f62-257">Промежуточный том предоставляет промежуточное расположение, в котором изначально доступная система архивации данных Windows Server размещает резервные копии состояния системы.</span><span class="sxs-lookup"><span data-stu-id="27f62-257">The Staging Volume represents the intermediate location where the natively available, Windows Server Backup stages the System State Backup.</span></span> <span data-ttu-id="27f62-258">Затем агент службы Azure Backup сжимает и шифрует эту промежуточную резервную копию и отправляет ее через защищенный протокол HTTPS в настроенное хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="27f62-258">Azure Backup agent then compresses and encrypts this intermediate backup and sends it via secure HTTPS Protocol to the configured Recovery Services Vault.</span></span> <span data-ttu-id="27f62-259">**Мы настоятельно рекомендуем установить промежуточный том в томе операционной системы, отличной от Windows. Если возникнут проблемы с резервным копированием состояния системы, для устранения неполадок сначала необходимо проверить расположение промежуточного тома.**</span><span class="sxs-lookup"><span data-stu-id="27f62-259">**We strongly recommended you establish the Staging Volume in a non-Windows-OS volume. If you observe problems with System State Backups, checking the location of your Staging Volume is the first troubleshooting step.**</span></span> 

### <a name="how-can-i-change-the-staging-volume-path-specified-in-the-azure-backup-agent"></a><span data-ttu-id="27f62-260">Как изменить путь промежуточного тома, указанный в агенте службы Azure Backup?</span><span class="sxs-lookup"><span data-stu-id="27f62-260">How can I change the Staging Volume Path specified in the Azure Backup agent?</span></span>

<span data-ttu-id="27f62-261">По умолчанию промежуточный том расположен в папке кэша.</span><span class="sxs-lookup"><span data-stu-id="27f62-261">The Staging Volume is located in the cache folder by default.</span></span> 

1. <span data-ttu-id="27f62-262">Чтобы изменить это расположение, выполните следующую команду (в командной строке с повышенными привилегиями):</span><span class="sxs-lookup"><span data-stu-id="27f62-262">To change this location, use the following command (in an elevated command prompt):</span></span>
  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="27f62-263">Затем обновите следующие записи реестра, указав путь к новой папке промежуточного тома.</span><span class="sxs-lookup"><span data-stu-id="27f62-263">Then update the following registry entries with the path to the new Staging Volume folder.</span></span>

  |<span data-ttu-id="27f62-264">Путь к элементу реестра</span><span class="sxs-lookup"><span data-stu-id="27f62-264">Registry path</span></span>|<span data-ttu-id="27f62-265">Раздел реестра</span><span class="sxs-lookup"><span data-stu-id="27f62-265">Registry key</span></span>|<span data-ttu-id="27f62-266">Значение</span><span class="sxs-lookup"><span data-stu-id="27f62-266">Value</span></span>|
  |-------------|------------|-----|
  |<span data-ttu-id="27f62-267">HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span><span class="sxs-lookup"><span data-stu-id="27f62-267">HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config\CloudBackupProvider</span></span> | <span data-ttu-id="27f62-268">SSBStagingPath</span><span class="sxs-lookup"><span data-stu-id="27f62-268">SSBStagingPath</span></span> | <span data-ttu-id="27f62-269">новое расположение промежуточного тома</span><span class="sxs-lookup"><span data-stu-id="27f62-269">new staging volume location</span></span> |

<span data-ttu-id="27f62-270">В промежуточном пути учитывается регистр. Он должен точно соответствовать регистру на сервере.</span><span class="sxs-lookup"><span data-stu-id="27f62-270">The Staging Path is case sensitive and must be the exact same casing as what exists on the server.</span></span> 

3. <span data-ttu-id="27f62-271">Изменив путь промежуточного тома, перезапустите модуль резервного копирования:</span><span class="sxs-lookup"><span data-stu-id="27f62-271">Once you change the Staging volume path, restart the Backup engine:</span></span>
  ```
  PS C:\> Net start obengine
  ```
4. <span data-ttu-id="27f62-272">Чтобы использовать измененный путь, откройте агент служб восстановления Microsoft Azure и активируйте нерегламентированное резервное копирование состояния системы.</span><span class="sxs-lookup"><span data-stu-id="27f62-272">To pick up the changed path, open the Microsoft Azure Recovery Services agent and trigger an ad hoc backup of System State.</span></span>

### <a name="why-is-the-system-state-default-retention-set-to-60-days"></a><span data-ttu-id="27f62-273">Почему срок хранения состояния системы по умолчанию составляет 60 дней?</span><span class="sxs-lookup"><span data-stu-id="27f62-273">Why is the System State default retention set to 60 days?</span></span>

<span data-ttu-id="27f62-274">Срок эксплуатации резервных копий состояния системы равен времени существования отметки полного удаления для роли Windows Server Active Directory.</span><span class="sxs-lookup"><span data-stu-id="27f62-274">The useful life of a system state backup is the same as the "tombstone lifetime" setting for the Windows Server Active Directory role.</span></span> <span data-ttu-id="27f62-275">Значение по умолчанию для записи времени существования отметки полного удаления составляет 60 дней.</span><span class="sxs-lookup"><span data-stu-id="27f62-275">The default value for the tombstone lifetime entry is 60 days.</span></span> <span data-ttu-id="27f62-276">Это значение можно задать в объекте конфигурации службы каталогов (NTDS).</span><span class="sxs-lookup"><span data-stu-id="27f62-276">This value can be set on the Directory Service (NTDS) config object.</span></span>

### <a name="how-do-i-change-the-default-backup-and-retention-policy-for-system-state"></a><span data-ttu-id="27f62-277">Как изменить стандартную политику резервного копирования и хранения состояния системы?</span><span class="sxs-lookup"><span data-stu-id="27f62-277">How do I change the default Backup and Retention Policy for System State?</span></span>

<span data-ttu-id="27f62-278">Для этого сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="27f62-278">To change the default Backup and Retention Policy for System State:</span></span>
1. <span data-ttu-id="27f62-279">Остановите работу модуля резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="27f62-279">Stop the Backup engine.</span></span> <span data-ttu-id="27f62-280">Выполните следующую команду в командной строке с повышенными привилегиями:</span><span class="sxs-lookup"><span data-stu-id="27f62-280">Run the following command from an elevated command prompt.</span></span>

  ```
  PS C:\> Net stop obengine
  ```

2. <span data-ttu-id="27f62-281">Добавьте или обновите следующие записи раздела реестра в HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider.</span><span class="sxs-lookup"><span data-stu-id="27f62-281">Add or update the following registry key entries in HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider.</span></span>

  |<span data-ttu-id="27f62-282">Имя реестра</span><span class="sxs-lookup"><span data-stu-id="27f62-282">Registry Name</span></span>|<span data-ttu-id="27f62-283">Описание</span><span class="sxs-lookup"><span data-stu-id="27f62-283">Description</span></span>|<span data-ttu-id="27f62-284">Значение</span><span class="sxs-lookup"><span data-stu-id="27f62-284">Value</span></span>|
  |-------------|-----------|-----|
  |<span data-ttu-id="27f62-285">SSBScheduleTime</span><span class="sxs-lookup"><span data-stu-id="27f62-285">SSBScheduleTime</span></span>|<span data-ttu-id="27f62-286">Используется для настройки времени резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="27f62-286">Used to configure the time of the backup.</span></span> <span data-ttu-id="27f62-287">Значение по умолчанию — 21:00 по местному времени.</span><span class="sxs-lookup"><span data-stu-id="27f62-287">Default is 9PM local time.</span></span>|<span data-ttu-id="27f62-288">DWORD: формат ЧЧММ (десятичное число), например 2130 для 21:30 по местному времени.</span><span class="sxs-lookup"><span data-stu-id="27f62-288">DWord: Format HHMM (Decimal) for example 2130 for 9:30PM local time</span></span>|
  |<span data-ttu-id="27f62-289">SSBScheduleDays</span><span class="sxs-lookup"><span data-stu-id="27f62-289">SSBScheduleDays</span></span>|<span data-ttu-id="27f62-290">Используется для настройки дней, когда необходимо выполнить резервное копирование состояния системы в определенный промежуток времени.</span><span class="sxs-lookup"><span data-stu-id="27f62-290">Used to configure the days when System State Backup must be performed at the specified time.</span></span> <span data-ttu-id="27f62-291">Дни недели указываются с помощью отдельных цифр.</span><span class="sxs-lookup"><span data-stu-id="27f62-291">Individual digits specify days of the week.</span></span> <span data-ttu-id="27f62-292">0 означает воскресенье, 1 — понедельник и т. д.</span><span class="sxs-lookup"><span data-stu-id="27f62-292">0 represents Sunday, 1 is Monday, and so on.</span></span> <span data-ttu-id="27f62-293">Стандартным днем для резервного копирования является воскресенье.</span><span class="sxs-lookup"><span data-stu-id="27f62-293">Default day for backup is Sunday.</span></span>|<span data-ttu-id="27f62-294">DWORD: дни недели для выполнения резервного копирования (десятичное число), например 1230 планирует резервное копирование на понедельник, вторник, среду и воскресенье.</span><span class="sxs-lookup"><span data-stu-id="27f62-294">DWord: days of the week to run backup (decimal) for example 1230 schedules backups on Monday, Tuesday, Wednesday, and Sunday.</span></span>|
  |<span data-ttu-id="27f62-295">SSBRetentionDays</span><span class="sxs-lookup"><span data-stu-id="27f62-295">SSBRetentionDays</span></span>|<span data-ttu-id="27f62-296">Используется для настройки дней для хранения резервной копии.</span><span class="sxs-lookup"><span data-stu-id="27f62-296">Used to configure the days to retain backup.</span></span> <span data-ttu-id="27f62-297">Значение по умолчанию — 60.</span><span class="sxs-lookup"><span data-stu-id="27f62-297">Default value is 60.</span></span> <span data-ttu-id="27f62-298">Допустимое значение не должно превышать 180.</span><span class="sxs-lookup"><span data-stu-id="27f62-298">Maximum allowed value is 180.</span></span>|<span data-ttu-id="27f62-299">DWORD: дни для хранения резервных копий (десятичное число).</span><span class="sxs-lookup"><span data-stu-id="27f62-299">DWord: Days to retain backup (decimal).</span></span>|

3. <span data-ttu-id="27f62-300">Выполните следующую команду, чтобы перезапустить модуль резервного копирования:</span><span class="sxs-lookup"><span data-stu-id="27f62-300">Use the following command to restart the backup engine.</span></span>
    ```
    PS C:\> Net start obengine
    ```

4. <span data-ttu-id="27f62-301">Откройте агент служб восстановления Microsoft.</span><span class="sxs-lookup"><span data-stu-id="27f62-301">Open the Microsoft Recovery Services agent.</span></span>

5. <span data-ttu-id="27f62-302">Выберите **Создать расписание архивации** и нажимайте кнопку **Далее** пока не увидите изменения.</span><span class="sxs-lookup"><span data-stu-id="27f62-302">Click **Schedule Backup** and then click **Next** until you see the changes reflected.</span></span>

6. <span data-ttu-id="27f62-303">Нажмите кнопку **Готово**, чтобы применить изменения.</span><span class="sxs-lookup"><span data-stu-id="27f62-303">Click **Finish** to apply the changes.</span></span>


## <a name="questions"></a><span data-ttu-id="27f62-304">Вопросы?</span><span class="sxs-lookup"><span data-stu-id="27f62-304">Questions?</span></span>
<span data-ttu-id="27f62-305">Если вы хотите задать вопрос или предложить добавить какие-либо функции, [отправьте нам свой отзыв](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="27f62-305">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="27f62-306">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="27f62-306">Next steps</span></span>
* <span data-ttu-id="27f62-307">См. дополнительные сведения об [архивации компьютеров Windows](backup-configure-vault.md).</span><span class="sxs-lookup"><span data-stu-id="27f62-307">Get more details about [backing up Windows machines](backup-configure-vault.md).</span></span>
* <span data-ttu-id="27f62-308">Теперь, когда вы выполнили резервное копирование файлов и папок, вы можете [управлять хранилищами и серверами](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="27f62-308">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="27f62-309">Если необходимо восстановить резервную копию, см. статью о [восстановлении файлов на компьютере Windows](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="27f62-309">If you need to restore a backup, use this article to [restore files to a Windows machine](backup-azure-restore-windows-server.md).</span></span>
