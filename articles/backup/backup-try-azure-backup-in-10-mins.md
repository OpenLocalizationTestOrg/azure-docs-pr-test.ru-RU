---
title: "Архивация файлов и папок Windows в Azure (Resource Manager) | Документация Майкрософт"
description: "Описание архивации файлов и папок Windows в Azure с использованием модели развертывания с помощью Resource Manager."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "как выполнять резервное копирование, резервное копирование файлов и папок"
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 8/15/2017
ms.author: markgal;
ms.openlocfilehash: b21edb70eca3ec9552dc157ee3bb658d243b8fcd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="first-look-back-up-files-and-folders-in-resource-manager-deployment"></a><span data-ttu-id="7e3af-104">Первое знакомство. Резервное копирование файлов и папок с использованием модели развертывания с помощью Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7e3af-104">First look: back up files and folders in Resource Manager deployment</span></span>
<span data-ttu-id="7e3af-105">В этой статье описывается, как выполнить резервное копирование файлов и папок Windows Server (на компьютере с Windows) в Azure с помощью службы архивации Azure, используя модель развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7e3af-105">This article explains how to back up your Windows Server (or Windows computer) files and folders to Azure using a Resource Manager deployment.</span></span> <span data-ttu-id="7e3af-106">В этом руководстве приведены общие сведения,</span><span class="sxs-lookup"><span data-stu-id="7e3af-106">It's a tutorial intended to walk you through the basics.</span></span> <span data-ttu-id="7e3af-107">и с помощью него вы сможете опробовать службу архивации Azure.</span><span class="sxs-lookup"><span data-stu-id="7e3af-107">If you want to get started using Azure Backup, you're in the right place.</span></span>

<span data-ttu-id="7e3af-108">Дополнительные сведения о службе архивации Azure см. в этом [обзоре](backup-introduction-to-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="7e3af-108">If you want to know more about Azure Backup, read this [overview](backup-introduction-to-azure-backup.md).</span></span>

<span data-ttu-id="7e3af-109">Если у вас нет подписки Azure, вы можете создать [бесплатную учетную запись](https://azure.microsoft.com/free/), предоставляющую доступ ко всем службам Azure.</span><span class="sxs-lookup"><span data-stu-id="7e3af-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) that lets you access any Azure service.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="7e3af-110">Создание хранилища служб восстановления</span><span class="sxs-lookup"><span data-stu-id="7e3af-110">Create a recovery services vault</span></span>
<span data-ttu-id="7e3af-111">Для резервного копирования файлов и папок нужно создать хранилище служб восстановления в том регионе, в котором планируется хранить данные.</span><span class="sxs-lookup"><span data-stu-id="7e3af-111">To back up your files and folders, you need to create a Recovery Services vault in the region where you want to store the data.</span></span> <span data-ttu-id="7e3af-112">Кроме того, необходимо определить способ репликации хранилища.</span><span class="sxs-lookup"><span data-stu-id="7e3af-112">You also need to determine how you want your storage replicated.</span></span>

### <a name="to-create-a-recovery-services-vault"></a><span data-ttu-id="7e3af-113">Создание хранилища служб восстановления</span><span class="sxs-lookup"><span data-stu-id="7e3af-113">To create a Recovery Services vault</span></span>
1. <span data-ttu-id="7e3af-114">Используя подписку Azure, войдите на [портал Azure](https://portal.azure.com/) (если вы еще этого не сделали).</span><span class="sxs-lookup"><span data-stu-id="7e3af-114">If you haven't already done so, sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="7e3af-115">В главном меню щелкните **Другие службы**, а затем в списке ресурсов введите **Службы восстановления** и щелкните **Хранилища служб восстановления**.</span><span class="sxs-lookup"><span data-stu-id="7e3af-115">On the Hub menu, click **More services** and in the list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Создание хранилища служб восстановления — шаг 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="7e3af-117">Если в подписке есть хранилища служб восстановления, они отобразятся в списке.</span><span class="sxs-lookup"><span data-stu-id="7e3af-117">If there are recovery services vaults in the subscription, the vaults are listed.</span></span>
3. <span data-ttu-id="7e3af-118">В меню **Хранилища служб восстановления** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="7e3af-118">On the **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Создание хранилища служб восстановления — шаг 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="7e3af-120">Откроется колонка хранилища служб восстановления, в которой нужно указать **имя**, **подписку**, **группу ресурсов** и **расположение**.</span><span class="sxs-lookup"><span data-stu-id="7e3af-120">The Recovery Services vault blade opens, prompting you to provide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Создание хранилища служб восстановления — шаг 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="7e3af-122">В поле **Имя**введите понятное имя хранилища.</span><span class="sxs-lookup"><span data-stu-id="7e3af-122">For **Name**, enter a friendly name to identify the vault.</span></span> <span data-ttu-id="7e3af-123">Имя должно быть уникальным в пределах подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="7e3af-123">The name needs to be unique for the Azure subscription.</span></span> <span data-ttu-id="7e3af-124">Введите имя длиной от 2 до 50 знаков.</span><span class="sxs-lookup"><span data-stu-id="7e3af-124">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="7e3af-125">Имя должно начинаться с буквы, оно может содержать только буквы, цифры и дефисы.</span><span class="sxs-lookup"><span data-stu-id="7e3af-125">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="7e3af-126">В разделе **Подписка** в раскрывающемся меню выберите подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="7e3af-126">In the **Subscription** section, use the drop-down menu to choose the Azure subscription.</span></span> <span data-ttu-id="7e3af-127">Если вы используете только одну подписку, она уже отображается и вы можете перейти к следующему шагу.</span><span class="sxs-lookup"><span data-stu-id="7e3af-127">If you use only one subscription, that subscription appears and you can skip to the next step.</span></span> <span data-ttu-id="7e3af-128">Если неизвестно, какую подписку нужно использовать, оставьте подписку по умолчанию (или предлагаемую подписку).</span><span class="sxs-lookup"><span data-stu-id="7e3af-128">If you are not sure which subscription to use, use the default (or suggested) subscription.</span></span> <span data-ttu-id="7e3af-129">Вариантов будет несколько только в том случае, если учетная запись вашей организации связана с несколькими подписками Azure.</span><span class="sxs-lookup"><span data-stu-id="7e3af-129">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="7e3af-130">В разделе **Группа ресурсов** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="7e3af-130">In the **Resource group** section:</span></span>

    * <span data-ttu-id="7e3af-131">выберите **Создать**, если вы хотите создать группу ресурсов;</span><span class="sxs-lookup"><span data-stu-id="7e3af-131">select **Create new** if you want to create a new Resource group.</span></span>
    <span data-ttu-id="7e3af-132">Или</span><span class="sxs-lookup"><span data-stu-id="7e3af-132">Or</span></span>
    * <span data-ttu-id="7e3af-133">выберите **Использовать существующий** и просмотрите список доступных групп ресурсов в раскрывающемся меню.</span><span class="sxs-lookup"><span data-stu-id="7e3af-133">select **Use existing** and click the drop-down menu to see the available list of Resource groups.</span></span>

  <span data-ttu-id="7e3af-134">Дополнительные сведения о группах ресурсов см. в статье [Общие сведения об Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7e3af-134">For complete information on Resource groups, see the [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="7e3af-135">В поле **Расположение** выберите географический регион, в котором будет находиться хранилище.</span><span class="sxs-lookup"><span data-stu-id="7e3af-135">Click **Location** to select the geographic region for the vault.</span></span> <span data-ttu-id="7e3af-136">Этот выбор определяет географический регион, в который будут отправляться данные архивации.</span><span class="sxs-lookup"><span data-stu-id="7e3af-136">This choice determines the geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="7e3af-137">В нижней части колонки "Хранилище служб восстановления" нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7e3af-137">At the bottom of the Recovery Services vault blade, click **Create**.</span></span>

    <span data-ttu-id="7e3af-138">Создание хранилища служб восстановления может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="7e3af-138">It can take several minutes for the Recovery Services vault to be created.</span></span> <span data-ttu-id="7e3af-139">Следите за уведомлениями о состоянии на портале в верхней правой области.</span><span class="sxs-lookup"><span data-stu-id="7e3af-139">Monitor the status notifications in the upper right-hand area of the portal.</span></span> <span data-ttu-id="7e3af-140">После создания хранилище появится в списке хранилищ служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="7e3af-140">Once your vault is created, it appears in the list of Recovery Services vaults.</span></span> <span data-ttu-id="7e3af-141">Если через несколько минут хранилище не отобразилось, нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="7e3af-141">If after several minutes you don't see your vault, click **Refresh**.</span></span>

    ![Кнопка "Обновить"](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    <span data-ttu-id="7e3af-143">Как только хранилище отобразится в списке хранилищ служб восстановления, для него можно определить избыточность.</span><span class="sxs-lookup"><span data-stu-id="7e3af-143">Once you see your vault in the list of Recovery Services vaults, you are ready to set the storage redundancy.</span></span>

### <a name="set-storage-redundancy-for-the-vault"></a><span data-ttu-id="7e3af-144">Настройка избыточности хранилища</span><span class="sxs-lookup"><span data-stu-id="7e3af-144">Set storage redundancy for the vault</span></span>
<span data-ttu-id="7e3af-145">При создании хранилища служб восстановления настройте его избыточность в соответствии со своими потребностями.</span><span class="sxs-lookup"><span data-stu-id="7e3af-145">When you create a Recovery Services vault, make sure storage redundancy is configured the way you want.</span></span>

1. <span data-ttu-id="7e3af-146">В колонке **Хранилища служб восстановления** щелкните новое хранилище.</span><span class="sxs-lookup"><span data-stu-id="7e3af-146">From the **Recovery Services vaults** blade, click the new vault.</span></span>

    ![Выбор нового хранилища в списке хранилищ служб восстановления](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="7e3af-148">При выборе хранилища колонка **Хранилище служб восстановления** сужается и открывается колонка параметров (*с именем хранилища вверху*), а также колонка со сведениями о хранилище.</span><span class="sxs-lookup"><span data-stu-id="7e3af-148">When you select the vault, the **Recovery Services vault** blade narrows, and the Settings blade (*which has the name of the vault at the top*) and the vault details blade open.</span></span>

    ![Просмотр конфигурации нового хранилища](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)
2. <span data-ttu-id="7e3af-150">В колонке параметров нового хранилища прокрутите с помощью вертикального ползунка вниз к разделу "Управление" и щелкните **Инфраструктура резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="7e3af-150">In the new vault's Settings blade, use the vertical slide to scroll down to the Manage section, and click **Backup Infrastructure**.</span></span>
    <span data-ttu-id="7e3af-151">Откроется колонка инфраструктуры резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="7e3af-151">The Backup Infrastructure blade opens.</span></span>
3. <span data-ttu-id="7e3af-152">В этой колонке выберите **Инфраструктура резервного копирования**, чтобы открыть колонку **Конфигурация архивации**.</span><span class="sxs-lookup"><span data-stu-id="7e3af-152">In the Backup Infrastructure blade, click **Backup Configuration** to open the **Backup Configuration** blade.</span></span>

    ![Настройка конфигурации для нового хранилища](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. <span data-ttu-id="7e3af-154">Выберите нужный тип репликации для хранилища.</span><span class="sxs-lookup"><span data-stu-id="7e3af-154">Choose the appropriate storage replication option for your vault.</span></span>

    ![Варианты конфигурации хранилища](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    <span data-ttu-id="7e3af-156">По умолчанию это геоизбыточное хранилище.</span><span class="sxs-lookup"><span data-stu-id="7e3af-156">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="7e3af-157">Если в качестве конечной точки основного хранилища службы архивации используется Azure, выберите **геоизбыточное хранилище**,</span><span class="sxs-lookup"><span data-stu-id="7e3af-157">If you use Azure as a primary backup storage endpoint, continue to use **Geo-redundant**.</span></span> <span data-ttu-id="7e3af-158">а если нет, — **локально избыточное** (это позволит снизить плату за хранилище Azure).</span><span class="sxs-lookup"><span data-stu-id="7e3af-158">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces the Azure storage costs.</span></span> <span data-ttu-id="7e3af-159">Дополнительные сведения о [геоизбыточном](../storage/common/storage-redundancy.md#geo-redundant-storage) и [локально избыточном](../storage/common/storage-redundancy.md#locally-redundant-storage) хранилищах см. в статье [Репликация службы хранилища Azure](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="7e3af-159">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="7e3af-160">Теперь, когда вы создали хранилище, настройте в нем резервное копирование файлов и папок.</span><span class="sxs-lookup"><span data-stu-id="7e3af-160">Now that you've created a vault, configure it for backing up files and folders.</span></span>

## <a name="configure-the-vault"></a><span data-ttu-id="7e3af-161">Настройка хранилища</span><span class="sxs-lookup"><span data-stu-id="7e3af-161">Configure the vault</span></span>
1. <span data-ttu-id="7e3af-162">В колонке хранилища служб восстановления (хранилища, которое вы только что создали) в разделе "Начало работы" выберите **Резервное копирование**. Затем в колонке **Начало работы с резервным копированием** выберите **Цель резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="7e3af-162">On the Recovery Services vault blade (for the vault you just created), in the Getting Started section, click **Backup**, then on the **Getting Started with Backup** blade, select **Backup goal**.</span></span>

    ![Открытая колонка цели резервного копирования](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    <span data-ttu-id="7e3af-164">Откроется колонка **Цель резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="7e3af-164">The **Backup Goal** blade opens.</span></span>

    ![Открытая колонка цели резервного копирования](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="7e3af-166">В раскрывающемся меню **Где выполняется рабочая нагрузка?** выберите **Локально**.</span><span class="sxs-lookup"><span data-stu-id="7e3af-166">From the **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

    <span data-ttu-id="7e3af-167">Вы выбираете параметр **Локально**, потому что ваш компьютер Windows Server или Windows — это физический компьютер, которые не находится в Azure.</span><span class="sxs-lookup"><span data-stu-id="7e3af-167">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="7e3af-168">В меню **Что вы хотите резервировать?** выберите **Файлы и папки** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="7e3af-168">From the **What do you want to backup?** menu, select **Files and folders**, and click **OK**.</span></span>

    ![Настройка резервного копирования файлов и папок](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

    <span data-ttu-id="7e3af-170">После того как вы нажмете кнопку "ОК", рядом с параметром **Цель резервного копирования** появится флажок и откроется колонка **Подготовка инфраструктуры**.</span><span class="sxs-lookup"><span data-stu-id="7e3af-170">After clicking OK, a checkmark appears next to **Backup goal**, and the **Prepare infrastructure** blade opens.</span></span>

    ![Цель резервного копирования настроена, на очереди подготовка инфраструктуры](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="7e3af-172">В колонке **Подготовка инфраструктуры** щелкните **Скачать агент для Windows Server или Windows Client**.</span><span class="sxs-lookup"><span data-stu-id="7e3af-172">On the **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

    ![Download Agent for Windows Server or Windows Client](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

    <span data-ttu-id="7e3af-174">Если вы используете Windows Server Essential, выберите загрузку агента для Windows Server Essential.</span><span class="sxs-lookup"><span data-stu-id="7e3af-174">If you are using Windows Server Essential, then choose to download the agent for Windows Server Essential.</span></span> <span data-ttu-id="7e3af-175">Во всплывающем меню появится запрос на запуск или сохранение файла MARSAgentInstaller.exe.</span><span class="sxs-lookup"><span data-stu-id="7e3af-175">A pop-up menu prompts you to run or save MARSAgentInstaller.exe.</span></span>

    ![Диалоговое окно MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="7e3af-177">Во всплывающем окне скачивания нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="7e3af-177">In the download pop-up menu, click **Save**.</span></span>

    <span data-ttu-id="7e3af-178">По умолчанию файл **MARSagentinstaller.exe** сохраняется в папке для скачивания.</span><span class="sxs-lookup"><span data-stu-id="7e3af-178">By default, the **MARSagentinstaller.exe** file is saved to your Downloads folder.</span></span> <span data-ttu-id="7e3af-179">После завершения установки появится всплывающее окно с двумя вариантами действий: запустить установщик или открыть папку.</span><span class="sxs-lookup"><span data-stu-id="7e3af-179">When the installer completes, you will see a pop-up asking if you want to run the installer, or open the folder.</span></span>

    ![Download Agent for Windows Server or Windows Client](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

    <span data-ttu-id="7e3af-181">Пока не нужно устанавливать агент.</span><span class="sxs-lookup"><span data-stu-id="7e3af-181">You don't need to install the agent yet.</span></span> <span data-ttu-id="7e3af-182">Его можно установить после скачивания учетных данных хранилища.</span><span class="sxs-lookup"><span data-stu-id="7e3af-182">You can install the agent after you have downloaded the vault credentials.</span></span>

6. <span data-ttu-id="7e3af-183">В колонке **Подготовка инфраструктуры** щелкните **Скачать**.</span><span class="sxs-lookup"><span data-stu-id="7e3af-183">On the **Prepare infrastructure** blade, click **Download**.</span></span>

    ![Скачивание учетных данных хранилища](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

    <span data-ttu-id="7e3af-185">Учетные данные хранилища будут сохранены в папке "Загрузки".</span><span class="sxs-lookup"><span data-stu-id="7e3af-185">The vault credentials download to your Downloads folder.</span></span> <span data-ttu-id="7e3af-186">После этого вы увидите всплывающее окно с двумя вариантами действий: открыть или сохранить учетные данные.</span><span class="sxs-lookup"><span data-stu-id="7e3af-186">After the vault credentials finish downloading, you see a pop-up asking if you want to open or save the credentials.</span></span> <span data-ttu-id="7e3af-187">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="7e3af-187">Click **Save**.</span></span> <span data-ttu-id="7e3af-188">Если вы случайно нажали кнопку **Открыть**, подождите, пока попытка открыть учетные данные хранилища закончится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="7e3af-188">If you accidentally click **Open**, let the dialog that attempts to open the vault credentials, fail.</span></span> <span data-ttu-id="7e3af-189">Вы не можете открыть учетные данные хранилища.</span><span class="sxs-lookup"><span data-stu-id="7e3af-189">You cannot open the vault credentials.</span></span> <span data-ttu-id="7e3af-190">Перейдите к следующему шагу.</span><span class="sxs-lookup"><span data-stu-id="7e3af-190">Proceed to the next step.</span></span> <span data-ttu-id="7e3af-191">Учетные данные хранилища находятся в папке "Загрузки".</span><span class="sxs-lookup"><span data-stu-id="7e3af-191">The vault credentials are in the Downloads folder.</span></span>   

    ![Загрузка учетных данных хранилища завершена](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-the-agent"></a><span data-ttu-id="7e3af-193">Установка и регистрация агента</span><span class="sxs-lookup"><span data-stu-id="7e3af-193">Install and register the agent</span></span>

> [!NOTE]
> <span data-ttu-id="7e3af-194">Параметр для включения резервного копирования на портале Azure пока недоступен.</span><span class="sxs-lookup"><span data-stu-id="7e3af-194">Enabling backup through the Azure portal is not available, yet.</span></span> <span data-ttu-id="7e3af-195">Чтобы выполнить резервное копирование файлов и папок, используйте агент служб восстановления Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7e3af-195">Use the Microsoft Azure Recovery Services Agent to back up your files and folders.</span></span>
>

1. <span data-ttu-id="7e3af-196">Найдите и дважды щелкните файл **MARSagentinstaller.exe** в папке "Загрузки" (или в другом расположении).</span><span class="sxs-lookup"><span data-stu-id="7e3af-196">Locate and double-click the **MARSagentinstaller.exe** from the Downloads folder (or other saved location).</span></span>

    <span data-ttu-id="7e3af-197">В установщике будут отображаться соответствующие сообщения по мере извлечения, установки и регистрации агента служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="7e3af-197">The installer provides a series of messages as it extracts, installs, and registers the Recovery Services agent.</span></span>

    ![Запуск установщика агента служб восстановления](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="7e3af-199">Выполните шаги мастера настройки агента служб восстановления Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7e3af-199">Complete the Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="7e3af-200">Для завершения работы с мастерам вам нужно:</span><span class="sxs-lookup"><span data-stu-id="7e3af-200">To complete the wizard, you need to:</span></span>

   * <span data-ttu-id="7e3af-201">Выбрать папку установки и папку кэша.</span><span class="sxs-lookup"><span data-stu-id="7e3af-201">Choose a location for the installation and cache folder.</span></span>
   * <span data-ttu-id="7e3af-202">Если для подключения к Интернету используется прокси-сервер, указать данные прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="7e3af-202">Provide your proxy server info if you use a proxy server to connect to the internet.</span></span>
   * <span data-ttu-id="7e3af-203">Если используется прокси-сервер, прошедший проверку подлинности, ввести имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="7e3af-203">Provide your user name and password details if you use an authenticated proxy.</span></span>
   * <span data-ttu-id="7e3af-204">Указать скачанные учетные данные хранилища.</span><span class="sxs-lookup"><span data-stu-id="7e3af-204">Provide the downloaded vault credentials</span></span>
   * <span data-ttu-id="7e3af-205">Сохранить парольную фразу шифрования в безопасном месте.</span><span class="sxs-lookup"><span data-stu-id="7e3af-205">Save the encryption passphrase in a secure location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="7e3af-206">Если вы потеряли или забыли парольную фразу, корпорация Майкрософт не сможет помочь вам восстановить резервную копию данных.</span><span class="sxs-lookup"><span data-stu-id="7e3af-206">If you lose or forget the passphrase, Microsoft cannot help recover the backup data.</span></span> <span data-ttu-id="7e3af-207">Сохраните файл в безопасном месте,</span><span class="sxs-lookup"><span data-stu-id="7e3af-207">Save the file in a secure location.</span></span> <span data-ttu-id="7e3af-208">так как он потребуется для восстановления резервной копии.</span><span class="sxs-lookup"><span data-stu-id="7e3af-208">It is required to restore a backup.</span></span>
     >
     >

<span data-ttu-id="7e3af-209">Теперь, когда агент установлен и компьютер зарегистрирован в хранилище,</span><span class="sxs-lookup"><span data-stu-id="7e3af-209">The agent is now installed and your machine is registered to the vault.</span></span> <span data-ttu-id="7e3af-210">вы можете настроить параметры резервного копирования, в том числе расписание.</span><span class="sxs-lookup"><span data-stu-id="7e3af-210">You're ready to configure and schedule your backup.</span></span>

## <a name="network-and-connectivity-requirements"></a><span data-ttu-id="7e3af-211">Требования к сети и подключению</span><span class="sxs-lookup"><span data-stu-id="7e3af-211">Network and Connectivity Requirements</span></span>

<span data-ttu-id="7e3af-212">Если компьютер или прокси-сервер имеет ограниченный доступ к Интернету, убедитесь, что параметры брандмауэра на компьютере или прокси разрешают следующие URL-адреса:</span><span class="sxs-lookup"><span data-stu-id="7e3af-212">If your machine/proxy has limited internet access, ensure that firewall settings on the mcahine/proxy are configured to allow the following URLs:</span></span> <br>
    1. <span data-ttu-id="7e3af-213">www.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="7e3af-213">www.msftncsi.com</span></span>
    2. <span data-ttu-id="7e3af-214">*.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="7e3af-214">*.Microsoft.com</span></span>
    3. <span data-ttu-id="7e3af-215">*.WindowsAzure.com</span><span class="sxs-lookup"><span data-stu-id="7e3af-215">*.WindowsAzure.com</span></span>
    4. <span data-ttu-id="7e3af-216">*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="7e3af-216">*.microsoftonline.com</span></span>
    5. <span data-ttu-id="7e3af-217">*.windows.net</span><span class="sxs-lookup"><span data-stu-id="7e3af-217">*.windows.ne</span></span>

## <a name="back-up-your-files-and-folders"></a><span data-ttu-id="7e3af-218">Резервное копирование файлов и папок</span><span class="sxs-lookup"><span data-stu-id="7e3af-218">Back up your files and folders</span></span>
<span data-ttu-id="7e3af-219">Начальная архивация включает в себя две основные задачи:</span><span class="sxs-lookup"><span data-stu-id="7e3af-219">The initial backup includes two key tasks:</span></span>

* <span data-ttu-id="7e3af-220">Планирование архивации</span><span class="sxs-lookup"><span data-stu-id="7e3af-220">Schedule the backup</span></span>
* <span data-ttu-id="7e3af-221">архивация файлов и папок впервые.</span><span class="sxs-lookup"><span data-stu-id="7e3af-221">Back up files and folders for the first time</span></span>

<span data-ttu-id="7e3af-222">Чтобы выполнить первоначальное резервное копирование, используйте агент служб восстановления Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7e3af-222">To complete the initial backup, use the Microsoft Azure Recovery Services agent.</span></span>

### <a name="to-schedule-the-backup-job"></a><span data-ttu-id="7e3af-223">Планирование задания резервного копирования</span><span class="sxs-lookup"><span data-stu-id="7e3af-223">To schedule the backup job</span></span>
1. <span data-ttu-id="7e3af-224">Откройте агент служб восстановления Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7e3af-224">Open the Microsoft Azure Recovery Services agent.</span></span> <span data-ttu-id="7e3af-225">Его можно найти, выполнив поиск строки **служба архивации Microsoft Azure**на компьютере.</span><span class="sxs-lookup"><span data-stu-id="7e3af-225">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Запуск агента служб восстановления Azure](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)
2. <span data-ttu-id="7e3af-227">В агенте служб восстановления щелкните **Создать расписание архивации**.</span><span class="sxs-lookup"><span data-stu-id="7e3af-227">In the Recovery Services agent, click **Schedule Backup**.</span></span>

    ![Планирование архивации Windows Server](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)
3. <span data-ttu-id="7e3af-229">На странице "Приступая к работе" в мастере планирования архивации нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7e3af-229">On the Getting started page of the Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="7e3af-230">На странице "Выбор элементов для архивации" щелкните **Добавить элементы**.</span><span class="sxs-lookup"><span data-stu-id="7e3af-230">On the Select Items to Backup page, click **Add Items**.</span></span>
5. <span data-ttu-id="7e3af-231">Выберите файлы и папки, которые нужно архивировать, и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="7e3af-231">Select the files and folders that you want to back up, and then click **Okay**.</span></span>
6. <span data-ttu-id="7e3af-232">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7e3af-232">Click **Next**.</span></span>
7. <span data-ttu-id="7e3af-233">На странице **Задайте расписание архивации** укажите **расписание резервного копирования** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7e3af-233">On the **Specify Backup Schedule** page, specify the **backup schedule** and click **Next**.</span></span>

    <span data-ttu-id="7e3af-234">Вы можете запланировать ежедневную (не более трех раз в день) или еженедельную архивацию.</span><span class="sxs-lookup"><span data-stu-id="7e3af-234">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Элементы для архивации Windows Server](./media/backup-try-azure-backup-in-10-mins/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="7e3af-236">Дополнительные сведения о настройке расписания резервного копирования см. в статье [Использование службы архивации Azure для замены ленточной инфраструктуры](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="7e3af-236">For more information about how to specify the backup schedule, see the article [Use Azure Backup to replace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >

8. <span data-ttu-id="7e3af-237">На странице **выбора политики хранения** выберите **политику хранения** для резервной копии.</span><span class="sxs-lookup"><span data-stu-id="7e3af-237">On the **Select Retention Policy** page, select the **Retention Policy** for the backup copy.</span></span>

    <span data-ttu-id="7e3af-238">С помощью политики хранения можно определить время хранения резервных копий данных.</span><span class="sxs-lookup"><span data-stu-id="7e3af-238">The retention policy specifies how long the backup data is stored.</span></span> <span data-ttu-id="7e3af-239">Вместо того чтобы настраивать одну политику для всех точек архивации, вы можете настроить разные политики хранения на основе времени создания архива.</span><span class="sxs-lookup"><span data-stu-id="7e3af-239">Rather than specifying a “flat policy” for all backup points, you can specify different retention policies based on when the backup occurs.</span></span> <span data-ttu-id="7e3af-240">Вы можете выбрать ежедневную, еженедельную, ежемесячную или ежегодную политику хранения с учетом своих потребностей.</span><span class="sxs-lookup"><span data-stu-id="7e3af-240">You can modify the daily, weekly, monthly, and yearly retention policies to meet your needs.</span></span>
9. <span data-ttu-id="7e3af-241">На странице "Выберите тип начального архива" выберите тип начального архива.</span><span class="sxs-lookup"><span data-stu-id="7e3af-241">On the Choose Initial Backup Type page, choose the initial backup type.</span></span> <span data-ttu-id="7e3af-242">Не снимайте флажок **Автоматически по сети** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7e3af-242">Leave the option **Automatically over the network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="7e3af-243">Резервное копирование можно выполнять по сети или в автономном режиме.</span><span class="sxs-lookup"><span data-stu-id="7e3af-243">You can back up automatically over the network, or you can back up offline.</span></span> <span data-ttu-id="7e3af-244">В оставшейся части этой статьи описан процесс автоматической архивации.</span><span class="sxs-lookup"><span data-stu-id="7e3af-244">The remainder of this article describes the process for backing up automatically.</span></span> <span data-ttu-id="7e3af-245">Если вы предпочитаете автономное резервное копирование, см. статью [Автономное резервное копирование в службе архивации Azure](backup-azure-backup-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="7e3af-245">If you prefer to do an offline backup, review the article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="7e3af-246">Проверьте сведения на странице подтверждения и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="7e3af-246">On the Confirmation page, review the information, and then click **Finish**.</span></span>
11. <span data-ttu-id="7e3af-247">Когда мастер завершит создание расписания архивации, нажмите кнопку **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="7e3af-247">After the wizard finishes creating the backup schedule, click **Close**.</span></span>

### <a name="to-back-up-files-and-folders-for-the-first-time"></a><span data-ttu-id="7e3af-248">Архивация файлов и папок впервые</span><span class="sxs-lookup"><span data-stu-id="7e3af-248">To back up files and folders for the first time</span></span>
1. <span data-ttu-id="7e3af-249">В агенте служб восстановления щелкните **Выполнить моментальную архивацию** , чтобы завершить начальное заполнение по сети.</span><span class="sxs-lookup"><span data-stu-id="7e3af-249">In the Recovery Services agent, click **Back Up Now** to complete the initial seeding over the network.</span></span>

    ![Моментальная архивация Windows Server](./media/backup-try-azure-backup-in-10-mins/backup-now.png)
2. <span data-ttu-id="7e3af-251">На странице "Подтверждение" проверьте параметры, которые мастер будет использовать для архивации данных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="7e3af-251">On the Confirmation page, review the settings that the Back Up Now Wizard will use to back up the machine.</span></span> <span data-ttu-id="7e3af-252">Затем нажмите кнопку **Архивировать**.</span><span class="sxs-lookup"><span data-stu-id="7e3af-252">Then click **Back Up**.</span></span>
3. <span data-ttu-id="7e3af-253">Нажмите кнопку **Закрыть**, чтобы закрыть мастер.</span><span class="sxs-lookup"><span data-stu-id="7e3af-253">Click **Close** to close the wizard.</span></span> <span data-ttu-id="7e3af-254">Если сделать это до завершения архивации, мастер продолжит работу в фоновом режиме.</span><span class="sxs-lookup"><span data-stu-id="7e3af-254">If you close the wizard before the backup process finishes, the wizard continues to run in the background.</span></span>

<span data-ttu-id="7e3af-255">После завершения начальной архивации в консоли службы архивации отобразится состояние **Задание выполнено** .</span><span class="sxs-lookup"><span data-stu-id="7e3af-255">After the initial backup is completed, the **Job completed** status appears in the Backup console.</span></span>

![Первоначальное восстановление завершено](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="questions"></a><span data-ttu-id="7e3af-257">Вопросы?</span><span class="sxs-lookup"><span data-stu-id="7e3af-257">Questions?</span></span>
<span data-ttu-id="7e3af-258">Если вы хотите задать вопрос или предложить добавить какие-либо функции, [отправьте нам свой отзыв](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="7e3af-258">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e3af-259">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7e3af-259">Next steps</span></span>
* <span data-ttu-id="7e3af-260">См. дополнительные сведения об [архивации компьютеров Windows](backup-configure-vault.md).</span><span class="sxs-lookup"><span data-stu-id="7e3af-260">Get more details about [backing up Windows machines](backup-configure-vault.md).</span></span>
* <span data-ttu-id="7e3af-261">Теперь, когда вы выполнили резервное копирование файлов и папок, вы можете [управлять хранилищами и серверами](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="7e3af-261">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="7e3af-262">Если необходимо восстановить резервную копию, см. статью о [восстановлении файлов на компьютере Windows](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="7e3af-262">If you need to restore a backup, use this article to [restore files to a Windows machine](backup-azure-restore-windows-server.md).</span></span>
