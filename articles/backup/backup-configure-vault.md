---
title: "Использование агента службы архивации Azure для резервного копирования файлов и папок | Документация Майкрософт"
description: "Использование агента службы архивации Microsoft Azure для резервного копирования файлов и папок Windows в Azure. Создание хранилища служб восстановления, установка агента службы архивации, определение политики архивации и начальная архивация файлов и папок."
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
ms.openlocfilehash: b95dc0a83d8e5618effb573353f419e1837d30c5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="back-up-a-windows-server-or-client-to-azure-using-the-resource-manager-deployment-model"></a><span data-ttu-id="7660a-105">Архивация сервера Windows Server или клиента Windows в Azure с использованием модели развертывания с помощью Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7660a-105">Back up a Windows Server or client to Azure using the Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7660a-106">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="7660a-106">Azure portal</span></span>](backup-configure-vault.md)
> * [<span data-ttu-id="7660a-107">Классический портал.</span><span class="sxs-lookup"><span data-stu-id="7660a-107">Classic portal</span></span>](backup-configure-vault-classic.md)
>
>

<span data-ttu-id="7660a-108">В этой статье описывается, как выполнить архивацию файлов и папок Windows Server или клиентского компьютера Windows в Azure с помощью службы архивации Azure, используя модель развертывания Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7660a-108">This article explains how to back up your Windows Server (or Windows client) files and folders to Azure with Azure Backup using the Resource Manager deployment model.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/backup-deployment-models.md)]

![Шаги архивации](./media/backup-configure-vault/initial-backup-process.png)

## <a name="before-you-start"></a><span data-ttu-id="7660a-110">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="7660a-110">Before you start</span></span>
<span data-ttu-id="7660a-111">Для архивации сервера или клиента в Azure вам потребуется учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="7660a-111">To back up a server or client to Azure, you need an Azure account.</span></span> <span data-ttu-id="7660a-112">Если ее нет, можно создать [бесплатную учетную запись](https://azure.microsoft.com/free/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="7660a-112">If you don't have one, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="7660a-113">Создание хранилища служб восстановления</span><span class="sxs-lookup"><span data-stu-id="7660a-113">Create a Recovery Services vault</span></span>
<span data-ttu-id="7660a-114">Хранилище служб восстановления — это сущность, в которой хранятся все созданные резервные копии и точки восстановления.</span><span class="sxs-lookup"><span data-stu-id="7660a-114">A Recovery Services vault is an entity that stores all the backups and recovery points you create over time.</span></span> <span data-ttu-id="7660a-115">В нем также содержится политика архивации, которая применяется к защищенным файлам и папкам.</span><span class="sxs-lookup"><span data-stu-id="7660a-115">The Recovery Services vault also contains the backup policy applied to the protected files and folders.</span></span> <span data-ttu-id="7660a-116">При создании хранилища служб восстановления следует также выбрать подходящий параметр избыточности хранилища.</span><span class="sxs-lookup"><span data-stu-id="7660a-116">When you create a Recovery Services vault, you should also select the appropriate storage redundancy option.</span></span>

### <a name="to-create-a-recovery-services-vault"></a><span data-ttu-id="7660a-117">Создание хранилища служб восстановления</span><span class="sxs-lookup"><span data-stu-id="7660a-117">To create a Recovery Services vault</span></span>
1. <span data-ttu-id="7660a-118">Используя подписку Azure, войдите на [портал Azure](https://portal.azure.com/) (если вы еще этого не сделали).</span><span class="sxs-lookup"><span data-stu-id="7660a-118">If you haven't already done so, sign in to the [Azure Portal](https://portal.azure.com/) using your Azure subscription.</span></span>
2. <span data-ttu-id="7660a-119">В главном меню щелкните **Другие службы**, а затем в списке ресурсов введите **Службы восстановления** и щелкните **Хранилища служб восстановления**.</span><span class="sxs-lookup"><span data-stu-id="7660a-119">On the Hub menu, click **More services** and in the list of resources, type **Recovery Services** and click **Recovery Services vaults**.</span></span>

    ![Создание хранилища служб восстановления — шаг 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    <span data-ttu-id="7660a-121">Если в подписке есть хранилища служб восстановления, они отобразятся в списке.</span><span class="sxs-lookup"><span data-stu-id="7660a-121">If there are recovery services vaults in the subscription, the vaults are listed.</span></span>

3. <span data-ttu-id="7660a-122">В меню **Хранилища служб восстановления** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="7660a-122">On the **Recovery Services vaults** menu, click **Add**.</span></span>

    ![Создание хранилища служб восстановления — шаг 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    <span data-ttu-id="7660a-124">Откроется колонка хранилища служб восстановления, в которой нужно указать **имя**, **подписку**, **группу ресурсов** и **расположение**.</span><span class="sxs-lookup"><span data-stu-id="7660a-124">The Recovery Services vault blade opens, prompting you to provide a **Name**, **Subscription**, **Resource group**, and **Location**.</span></span>

    ![Создание хранилища служб восстановления — шаг 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. <span data-ttu-id="7660a-126">В поле **Имя**введите понятное имя хранилища.</span><span class="sxs-lookup"><span data-stu-id="7660a-126">For **Name**, enter a friendly name to identify the vault.</span></span> <span data-ttu-id="7660a-127">Имя должно быть уникальным в пределах подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="7660a-127">The name needs to be unique for the Azure subscription.</span></span> <span data-ttu-id="7660a-128">Введите имя длиной от 2 до 50 знаков.</span><span class="sxs-lookup"><span data-stu-id="7660a-128">Type a name that contains between 2 and 50 characters.</span></span> <span data-ttu-id="7660a-129">Имя должно начинаться с буквы, оно может содержать только буквы, цифры и дефисы.</span><span class="sxs-lookup"><span data-stu-id="7660a-129">It must start with a letter, and can contain only letters, numbers, and hyphens.</span></span>

5. <span data-ttu-id="7660a-130">В разделе **Подписка** в раскрывающемся меню выберите подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="7660a-130">In the **Subscription** section, use the drop-down menu to choose the Azure subscription.</span></span> <span data-ttu-id="7660a-131">Если вы используете только одну подписку, она уже отображается и вы можете перейти к следующему шагу.</span><span class="sxs-lookup"><span data-stu-id="7660a-131">If you use only one subscription, that subscription appears and you can skip to the next step.</span></span> <span data-ttu-id="7660a-132">Если неизвестно, какую подписку нужно использовать, оставьте подписку по умолчанию (или предлагаемую подписку).</span><span class="sxs-lookup"><span data-stu-id="7660a-132">If you are not sure which subscription to use, use the default (or suggested) subscription.</span></span> <span data-ttu-id="7660a-133">Вариантов будет несколько только в том случае, если учетная запись вашей организации связана с несколькими подписками Azure.</span><span class="sxs-lookup"><span data-stu-id="7660a-133">There are multiple choices only if your organizational account is associated with multiple Azure subscriptions.</span></span>

6. <span data-ttu-id="7660a-134">В разделе **Группа ресурсов** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="7660a-134">In the **Resource group** section:</span></span>

    * <span data-ttu-id="7660a-135">выберите **Создать**, если вы хотите создать группу ресурсов;</span><span class="sxs-lookup"><span data-stu-id="7660a-135">select **Create new** if you want to create a new Resource group.</span></span>
    <span data-ttu-id="7660a-136">Или</span><span class="sxs-lookup"><span data-stu-id="7660a-136">Or</span></span>
    * <span data-ttu-id="7660a-137">выберите **Использовать существующий** и просмотрите список доступных групп ресурсов в раскрывающемся меню.</span><span class="sxs-lookup"><span data-stu-id="7660a-137">select **Use existing** and click the drop-down menu to see the available list of Resource groups.</span></span>

  <span data-ttu-id="7660a-138">Дополнительные сведения о группах ресурсов см. в статье [Общие сведения об Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7660a-138">For complete information on Resource groups, see the [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

7. <span data-ttu-id="7660a-139">В поле **Расположение** выберите географический регион, в котором будет находиться хранилище.</span><span class="sxs-lookup"><span data-stu-id="7660a-139">Click **Location** to select the geographic region for the vault.</span></span> <span data-ttu-id="7660a-140">Этот выбор определяет географический регион, в который будут отправляться данные архивации.</span><span class="sxs-lookup"><span data-stu-id="7660a-140">This choice determines the geographic region where your backup data is sent.</span></span>

8. <span data-ttu-id="7660a-141">В нижней части колонки "Хранилище служб восстановления" нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7660a-141">At the bottom of the Recovery Services vault blade, click **Create**.</span></span>

  <span data-ttu-id="7660a-142">Создание хранилища служб восстановления может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="7660a-142">It can take several minutes for the Recovery Services vault to be created.</span></span> <span data-ttu-id="7660a-143">Следите за уведомлениями о состоянии на портале в верхней правой области.</span><span class="sxs-lookup"><span data-stu-id="7660a-143">Monitor the status notifications in the upper right-hand area of the portal.</span></span> <span data-ttu-id="7660a-144">После создания хранилище появится в списке хранилищ служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="7660a-144">Once your vault is created, it appears in the list of Recovery Services vaults.</span></span> <span data-ttu-id="7660a-145">Если через несколько минут хранилище не отобразилось, нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="7660a-145">If after several minutes you don't see your vault, click **Refresh**.</span></span>

  ![Кнопка "Обновить"](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

  <span data-ttu-id="7660a-147">Как только хранилище отобразится в списке хранилищ служб восстановления, для него можно определить избыточность.</span><span class="sxs-lookup"><span data-stu-id="7660a-147">Once you see your vault in the list of Recovery Services vaults, you are ready to set the storage redundancy.</span></span>


### <a name="set-storage-redundancy"></a><span data-ttu-id="7660a-148">Установка избыточности хранилища</span><span class="sxs-lookup"><span data-stu-id="7660a-148">Set storage redundancy</span></span>
<span data-ttu-id="7660a-149">При первом создании хранилища служб восстановления нужно определить способ его репликации.</span><span class="sxs-lookup"><span data-stu-id="7660a-149">When you first create a Recovery Services vault you determine how storage is replicated.</span></span>

1. <span data-ttu-id="7660a-150">В колонке **Хранилища служб восстановления** щелкните новое хранилище.</span><span class="sxs-lookup"><span data-stu-id="7660a-150">From the **Recovery Services vaults** blade, click the new vault.</span></span>

    ![Выбор нового хранилища в списке хранилищ служб восстановления](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    <span data-ttu-id="7660a-152">При выборе хранилища колонка **Хранилище служб восстановления** сужается и открывается колонка параметров (*с именем хранилища вверху*), а также колонка со сведениями о хранилище.</span><span class="sxs-lookup"><span data-stu-id="7660a-152">When you select the vault, the **Recovery Services vault** blade narrows, and the Settings blade (*which has the name of the vault at the top*) and the vault details blade open.</span></span>

    ![Просмотр конфигурации нового хранилища](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)

2. <span data-ttu-id="7660a-154">В колонке параметров нового хранилища прокрутите с помощью вертикального ползунка вниз к разделу "Управление" и щелкните **Инфраструктура резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="7660a-154">In the new vault's Settings blade, use the vertical slide to scroll down to the Manage section, and click **Backup Infrastructure**.</span></span>

  <span data-ttu-id="7660a-155">Откроется колонка инфраструктуры резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="7660a-155">The Backup Infrastructure blade opens.</span></span>

3. <span data-ttu-id="7660a-156">В этой колонке выберите **Инфраструктура резервного копирования**, чтобы открыть колонку **Конфигурация архивации**.</span><span class="sxs-lookup"><span data-stu-id="7660a-156">In the Backup Infrastructure blade, click **Backup Configuration** to open the **Backup Configuration** blade.</span></span>

  ![Настройка конфигурации для нового хранилища](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)

4. <span data-ttu-id="7660a-158">Выберите нужный тип репликации для хранилища.</span><span class="sxs-lookup"><span data-stu-id="7660a-158">Choose the appropriate storage replication option for your vault.</span></span>

  ![Варианты конфигурации хранилища](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

  <span data-ttu-id="7660a-160">По умолчанию это геоизбыточное хранилище.</span><span class="sxs-lookup"><span data-stu-id="7660a-160">By default, your vault has geo-redundant storage.</span></span> <span data-ttu-id="7660a-161">Если в качестве конечной точки основного хранилища службы архивации используется Azure, выберите **геоизбыточное хранилище**,</span><span class="sxs-lookup"><span data-stu-id="7660a-161">If you use Azure as a primary backup storage endpoint, continue to use **Geo-redundant**.</span></span> <span data-ttu-id="7660a-162">а если нет, — **локально избыточное** (это позволит снизить плату за хранилище Azure).</span><span class="sxs-lookup"><span data-stu-id="7660a-162">If you don't use Azure as a primary backup storage endpoint, then choose **Locally-redundant**, which reduces the Azure storage costs.</span></span> <span data-ttu-id="7660a-163">Дополнительные сведения о [геоизбыточном](../storage/common/storage-redundancy.md#geo-redundant-storage) и [локально избыточном](../storage/common/storage-redundancy.md#locally-redundant-storage) хранилищах см. в статье [Репликация службы хранилища Azure](../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="7660a-163">Read more about [geo-redundant](../storage/common/storage-redundancy.md#geo-redundant-storage) and [locally redundant](../storage/common/storage-redundancy.md#locally-redundant-storage) storage options in this [Storage redundancy overview](../storage/common/storage-redundancy.md).</span></span>

<span data-ttu-id="7660a-164">Создав хранилище, подготовьте инфраструктуру к архивации файлов и папок. Для этого сначала скачайте и установите агент служб восстановления Microsoft Azure, а затем скачайте учетные данные хранилища и зарегистрируйте с их помощью агента в хранилище.</span><span class="sxs-lookup"><span data-stu-id="7660a-164">Now that you've created a vault, prepare your infrastructure to back up files and folders by downloading and installing the Microsoft Azure Recovery Services agent, downloading vault credentials, and then using those credentials to register the agent with the vault.</span></span>

## <a name="configure-the-vault"></a><span data-ttu-id="7660a-165">Настройка хранилища</span><span class="sxs-lookup"><span data-stu-id="7660a-165">Configure the vault</span></span>

1. <span data-ttu-id="7660a-166">В колонке хранилища служб восстановления (хранилища, которое вы только что создали) в разделе "Начало работы" выберите **Резервное копирование**. Затем в колонке **Начало работы с резервным копированием** выберите **Цель резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="7660a-166">On the Recovery Services vault blade (for the vault you just created), in the Getting Started section, click **Backup**, then on the **Getting Started with Backup** blade, select **Backup goal**.</span></span>

  ![Открытая колонка цели резервного копирования](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

  <span data-ttu-id="7660a-168">Откроется колонка **Цель резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="7660a-168">The **Backup Goal** blade opens.</span></span> <span data-ttu-id="7660a-169">Если хранилище служб восстановления уже настроено, при нажатии кнопки **Резервное копирование** в колонке хранилища служб восстановления откроется колонка **Цель резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="7660a-169">If the Recovery Services vault has been previously configured, then the **Backup Goal** blades opens when you click **Backup** on the Recovery Services vault blade.</span></span>

  ![Открытая колонка цели резервного копирования](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. <span data-ttu-id="7660a-171">В раскрывающемся меню **Где выполняется рабочая нагрузка?** выберите **Локально**.</span><span class="sxs-lookup"><span data-stu-id="7660a-171">From the **Where is your workload running?** drop-down menu, select **On-premises**.</span></span>

  <span data-ttu-id="7660a-172">Вы выбираете параметр **Локально**, потому что ваш компьютер Windows Server или Windows — это физический компьютер, которые не находится в Azure.</span><span class="sxs-lookup"><span data-stu-id="7660a-172">You choose **On-premises** because your Windows Server or Windows computer is a physical machine that is not in Azure.</span></span>

3. <span data-ttu-id="7660a-173">В меню **Что вы хотите резервировать?** выберите **Файлы и папки** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="7660a-173">From the **What do you want to backup?** menu, select **Files and folders**, and click **OK**.</span></span>

  ![Настройка резервного копирования файлов и папок](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

  <span data-ttu-id="7660a-175">После того как вы нажмете кнопку "ОК", рядом с параметром **Цель резервного копирования** появится флажок и откроется колонка **Подготовка инфраструктуры**.</span><span class="sxs-lookup"><span data-stu-id="7660a-175">After clicking OK, a checkmark appears next to **Backup goal**, and the **Prepare infrastructure** blade opens.</span></span>

  ![Цель резервного копирования настроена, на очереди подготовка инфраструктуры](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. <span data-ttu-id="7660a-177">В колонке **Подготовка инфраструктуры** щелкните **Скачать агент для Windows Server или Windows Client**.</span><span class="sxs-lookup"><span data-stu-id="7660a-177">On the **Prepare infrastructure** blade, click **Download Agent for Windows Server or Windows Client**.</span></span>

  ![Download Agent for Windows Server or Windows Client](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

  <span data-ttu-id="7660a-179">Если вы используете Windows Server Essential, выберите загрузку агента для Windows Server Essential.</span><span class="sxs-lookup"><span data-stu-id="7660a-179">If you are using Windows Server Essential, then choose to download the agent for Windows Server Essential.</span></span> <span data-ttu-id="7660a-180">Во всплывающем меню появится запрос на запуск или сохранение файла MARSAgentInstaller.exe.</span><span class="sxs-lookup"><span data-stu-id="7660a-180">A pop-up menu prompts you to run or save MARSAgentInstaller.exe.</span></span>

  ![Диалоговое окно MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. <span data-ttu-id="7660a-182">Во всплывающем окне скачивания нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="7660a-182">In the download pop-up menu, click **Save**.</span></span>

  <span data-ttu-id="7660a-183">По умолчанию файл **MARSagentinstaller.exe** сохраняется в папке для скачивания.</span><span class="sxs-lookup"><span data-stu-id="7660a-183">By default, the **MARSagentinstaller.exe** file is saved to your Downloads folder.</span></span> <span data-ttu-id="7660a-184">После завершения установки появится всплывающее окно с двумя вариантами действий: запустить установщик или открыть папку.</span><span class="sxs-lookup"><span data-stu-id="7660a-184">When the installer completes, you will see a pop-up asking if you want to run the installer, or open the folder.</span></span>

  ![Download Agent for Windows Server or Windows Client](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

  <span data-ttu-id="7660a-186">Пока не нужно устанавливать агент.</span><span class="sxs-lookup"><span data-stu-id="7660a-186">You don't need to install the agent yet.</span></span> <span data-ttu-id="7660a-187">Его можно установить после скачивания учетных данных хранилища.</span><span class="sxs-lookup"><span data-stu-id="7660a-187">You can install the agent after you have downloaded the vault credentials.</span></span>

6. <span data-ttu-id="7660a-188">В колонке **Подготовка инфраструктуры** щелкните **Скачать**.</span><span class="sxs-lookup"><span data-stu-id="7660a-188">On the **Prepare infrastructure** blade, click **Download**.</span></span>

  ![Скачивание учетных данных хранилища](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

  <span data-ttu-id="7660a-190">Учетные данные хранилища будут сохранены в папке "Загрузки".</span><span class="sxs-lookup"><span data-stu-id="7660a-190">The vault credentials download to your Downloads folder.</span></span> <span data-ttu-id="7660a-191">После этого вы увидите всплывающее окно с двумя вариантами действий: открыть или сохранить учетные данные.</span><span class="sxs-lookup"><span data-stu-id="7660a-191">After the vault credentials finish downloading, you see a pop-up asking if you want to open or save the credentials.</span></span> <span data-ttu-id="7660a-192">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="7660a-192">Click **Save**.</span></span> <span data-ttu-id="7660a-193">Если вы случайно нажали кнопку **Открыть**, подождите, пока попытка открыть учетные данные хранилища закончится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="7660a-193">If you accidentally click **Open**, let the dialog that attempts to open the vault credentials, fail.</span></span> <span data-ttu-id="7660a-194">Вы не можете открыть учетные данные хранилища.</span><span class="sxs-lookup"><span data-stu-id="7660a-194">You cannot open the vault credentials.</span></span> <span data-ttu-id="7660a-195">Перейдите к следующему шагу.</span><span class="sxs-lookup"><span data-stu-id="7660a-195">Proceed to the next step.</span></span> <span data-ttu-id="7660a-196">Учетные данные хранилища находятся в папке "Загрузки".</span><span class="sxs-lookup"><span data-stu-id="7660a-196">The vault credentials are in the Downloads folder.</span></span>   

  ![Загрузка учетных данных хранилища завершена](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-the-agent"></a><span data-ttu-id="7660a-198">Установка и регистрация агента</span><span class="sxs-lookup"><span data-stu-id="7660a-198">Install and register the agent</span></span>

> [!NOTE]
> <span data-ttu-id="7660a-199">Параметр для включения резервного копирования на портале Azure пока недоступен.</span><span class="sxs-lookup"><span data-stu-id="7660a-199">Enabling backup through the Azure portal is not available, yet.</span></span> <span data-ttu-id="7660a-200">Чтобы выполнить резервное копирование файлов и папок, используйте агент служб восстановления Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7660a-200">Use the Microsoft Azure Recovery Services Agent to back up your files and folders.</span></span>
>

1. <span data-ttu-id="7660a-201">Найдите и дважды щелкните файл **MARSagentinstaller.exe** в папке "Загрузки" (или в другом расположении).</span><span class="sxs-lookup"><span data-stu-id="7660a-201">Locate and double-click the **MARSagentinstaller.exe** from the Downloads folder (or other saved location).</span></span>

  <span data-ttu-id="7660a-202">В установщике будут отображаться соответствующие сообщения по мере извлечения, установки и регистрации агента служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="7660a-202">The installer provides a series of messages as it extracts, installs, and registers the Recovery Services agent.</span></span>

  ![Запуск установщика агента служб восстановления](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. <span data-ttu-id="7660a-204">Выполните шаги мастера настройки агента служб восстановления Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7660a-204">Complete the Microsoft Azure Recovery Services Agent Setup Wizard.</span></span> <span data-ttu-id="7660a-205">Для завершения работы с мастерам вам нужно:</span><span class="sxs-lookup"><span data-stu-id="7660a-205">To complete the wizard, you need to:</span></span>

  * <span data-ttu-id="7660a-206">Выбрать папку установки и папку кэша.</span><span class="sxs-lookup"><span data-stu-id="7660a-206">Choose a location for the installation and cache folder.</span></span>
  * <span data-ttu-id="7660a-207">Если для подключения к Интернету используется прокси-сервер, указать данные прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="7660a-207">Provide your proxy server info if you use a proxy server to connect to the internet.</span></span>
  * <span data-ttu-id="7660a-208">Если используется прокси-сервер, прошедший проверку подлинности, ввести имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="7660a-208">Provide your user name and password details if you use an authenticated proxy.</span></span>
  * <span data-ttu-id="7660a-209">Указать скачанные учетные данные хранилища.</span><span class="sxs-lookup"><span data-stu-id="7660a-209">Provide the downloaded vault credentials</span></span>
  * <span data-ttu-id="7660a-210">Сохранить парольную фразу шифрования в безопасном месте.</span><span class="sxs-lookup"><span data-stu-id="7660a-210">Save the encryption passphrase in a secure location.</span></span>

  > [!NOTE]
  > <span data-ttu-id="7660a-211">Если вы потеряли или забыли парольную фразу, корпорация Майкрософт не сможет помочь вам восстановить резервную копию данных.</span><span class="sxs-lookup"><span data-stu-id="7660a-211">If you lose or forget the passphrase, Microsoft cannot help recover the backup data.</span></span> <span data-ttu-id="7660a-212">Сохраните файл в безопасном месте,</span><span class="sxs-lookup"><span data-stu-id="7660a-212">Save the file in a secure location.</span></span> <span data-ttu-id="7660a-213">так как он потребуется для восстановления резервной копии.</span><span class="sxs-lookup"><span data-stu-id="7660a-213">It is required to restore a backup.</span></span>
  >
  >

<span data-ttu-id="7660a-214">Теперь, когда агент установлен и компьютер зарегистрирован в хранилище,</span><span class="sxs-lookup"><span data-stu-id="7660a-214">The agent is now installed and your machine is registered to the vault.</span></span> <span data-ttu-id="7660a-215">вы можете настроить параметры резервного копирования, в том числе расписание.</span><span class="sxs-lookup"><span data-stu-id="7660a-215">You're ready to configure and schedule your backup.</span></span>

## <a name="network-and-connectivity-requirements"></a><span data-ttu-id="7660a-216">Требования к сети и подключению</span><span class="sxs-lookup"><span data-stu-id="7660a-216">Network and Connectivity Requirements</span></span>

<span data-ttu-id="7660a-217">Если компьютер или прокси-сервер имеет ограниченный доступ к Интернету, убедитесь, что параметры брандмауэра на компьютере или прокси разрешают следующие URL-адреса:</span><span class="sxs-lookup"><span data-stu-id="7660a-217">If your machine/proxy has limited internet access, ensure that firewall settings on the machine/proxy are configured to allow the following URLs:</span></span> <br>
    1. <span data-ttu-id="7660a-218">www.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="7660a-218">www.msftncsi.com</span></span>
    2. <span data-ttu-id="7660a-219">*.Microsoft.com</span><span class="sxs-lookup"><span data-stu-id="7660a-219">*.Microsoft.com</span></span>
    3. <span data-ttu-id="7660a-220">*.WindowsAzure.com</span><span class="sxs-lookup"><span data-stu-id="7660a-220">*.WindowsAzure.com</span></span>
    4. <span data-ttu-id="7660a-221">*.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="7660a-221">*.microsoftonline.com</span></span>
    5. <span data-ttu-id="7660a-222">*.windows.net</span><span class="sxs-lookup"><span data-stu-id="7660a-222">*.windows.ne</span></span>


## <a name="create-the-backup-policy"></a><span data-ttu-id="7660a-223">Создание политики архивации</span><span class="sxs-lookup"><span data-stu-id="7660a-223">Create the backup policy</span></span>
<span data-ttu-id="7660a-224">Политика архивации — это расписание, которое определяет частоту и время создания точек восстановления, а также срок хранения каждой резервной копии.</span><span class="sxs-lookup"><span data-stu-id="7660a-224">The backup policy is the schedule when recovery points are taken, and the length of time the recovery points are retained.</span></span> <span data-ttu-id="7660a-225">Используйте агент службы архивации Microsoft Azure для создания политики архивации файлов и папок.</span><span class="sxs-lookup"><span data-stu-id="7660a-225">Use the Microsoft Azure Backup agent to create the backup policy for files and folders.</span></span>

### <a name="to-create-a-backup-schedule"></a><span data-ttu-id="7660a-226">Создание расписания архивации</span><span class="sxs-lookup"><span data-stu-id="7660a-226">To create a backup schedule</span></span>
1. <span data-ttu-id="7660a-227">Откройте агент службы архивации Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7660a-227">Open the Microsoft Azure Backup agent.</span></span> <span data-ttu-id="7660a-228">Его можно найти, выполнив поиск строки **служба архивации Microsoft Azure**на компьютере.</span><span class="sxs-lookup"><span data-stu-id="7660a-228">You can find it by searching your machine for **Microsoft Azure Backup**.</span></span>

    ![Запуск агента службы архивации Azure](./media/backup-configure-vault/snap-in-search.png)
2. <span data-ttu-id="7660a-230">В области **Действия** агента службы архивации щелкните **Создать расписание архивации**, чтобы запустить мастер планирования архивации.</span><span class="sxs-lookup"><span data-stu-id="7660a-230">In the Backup agent's **Actions** pane, click **Schedule Backup** to launch the Schedule Backup Wizard.</span></span>

    ![Планирование архивации Windows Server](./media/backup-configure-vault/schedule-first-backup.png)

3. <span data-ttu-id="7660a-232">На странице **Приступая к работе** в мастере планирования архивации нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7660a-232">On the **Getting started** page of the Schedule Backup Wizard, click **Next**.</span></span>
4. <span data-ttu-id="7660a-233">На странице **Выбор элементов для архивации** щелкните **Добавить элементы**.</span><span class="sxs-lookup"><span data-stu-id="7660a-233">On the **Select Items to Backup** page, click **Add Items**.</span></span>

  <span data-ttu-id="7660a-234">Откроется диалоговое окно выбора элементов.</span><span class="sxs-lookup"><span data-stu-id="7660a-234">The Select Items dialog opens.</span></span>

5. <span data-ttu-id="7660a-235">Выберите файлы и папки, которые нужно защитить, и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="7660a-235">Select the files and folders that you want to protect, and then click **OK**.</span></span>
6. <span data-ttu-id="7660a-236">На странице **Выбор элементов для архивации** щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7660a-236">In the **Select Items to Backup** page, click **Next**.</span></span>
7. <span data-ttu-id="7660a-237">На странице **Задайте расписание архивации** укажите расписание резервного копирования и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7660a-237">On the **Specify Backup Schedule** page, specify the backup schedule and click **Next**.</span></span>

    <span data-ttu-id="7660a-238">Вы можете запланировать ежедневную (не более трех раз в день) или еженедельную архивацию.</span><span class="sxs-lookup"><span data-stu-id="7660a-238">You can schedule daily (at a maximum rate of three times per day) or weekly backups.</span></span>

    ![Элементы для архивации Windows Server](./media/backup-configure-vault/specify-backup-schedule-close.png)

   > [!NOTE]
   > <span data-ttu-id="7660a-240">Дополнительные сведения о настройке расписания резервного копирования см. в статье [Использование службы архивации Azure для замены ленточной инфраструктуры](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="7660a-240">For more information about how to specify the backup schedule, see the article [Use Azure Backup to replace your tape infrastructure](backup-azure-backup-cloud-as-tape.md).</span></span>
   >
   >

8. <span data-ttu-id="7660a-241">На странице **выбора политики хранения** выберите определенную политику хранения для резервной копии и щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7660a-241">On the **Select Retention Policy** page, choose the specific retention policies the for the backup copy and click **Next**.</span></span>

    <span data-ttu-id="7660a-242">Политика хранения определяет время, в течение которого должна храниться резервная копия.</span><span class="sxs-lookup"><span data-stu-id="7660a-242">The retention policy specifies the duration which the backup is stored.</span></span> <span data-ttu-id="7660a-243">Вместо того, чтобы настраивать одну политику для всех точек архивации, вы можете настроить разные политики хранения на основе времени создания архива.</span><span class="sxs-lookup"><span data-stu-id="7660a-243">Rather than just specifying a “flat policy” for all backup points, you can specify different retention policies based on when the backup occurs.</span></span> <span data-ttu-id="7660a-244">Вы можете выбрать ежедневную, еженедельную, ежемесячную или ежегодную политику хранения с учетом своих потребностей.</span><span class="sxs-lookup"><span data-stu-id="7660a-244">You can modify the daily, weekly, monthly, and yearly retention policies to meet your needs.</span></span>
9. <span data-ttu-id="7660a-245">На странице "Выберите тип начального архива" выберите тип начального архива.</span><span class="sxs-lookup"><span data-stu-id="7660a-245">On the Choose Initial Backup Type page, choose the initial backup type.</span></span> <span data-ttu-id="7660a-246">Не снимайте флажок **Автоматически по сети** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="7660a-246">Leave the option **Automatically over the network** selected, and then click **Next**.</span></span>

    <span data-ttu-id="7660a-247">Резервное копирование можно выполнять по сети или в автономном режиме.</span><span class="sxs-lookup"><span data-stu-id="7660a-247">You can back up automatically over the network, or you can back up offline.</span></span> <span data-ttu-id="7660a-248">В оставшейся части этой статьи описан процесс автоматической архивации.</span><span class="sxs-lookup"><span data-stu-id="7660a-248">The remainder of this article describes the process for backing up automatically.</span></span> <span data-ttu-id="7660a-249">Если вы предпочитаете автономное резервное копирование, см. статью [Автономное резервное копирование в службе архивации Azure](backup-azure-backup-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="7660a-249">If you prefer to do an offline backup, review the article [Offline backup workflow in Azure Backup](backup-azure-backup-import-export.md) for additional information.</span></span>
10. <span data-ttu-id="7660a-250">Проверьте сведения на странице подтверждения и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="7660a-250">On the Confirmation page, review the information, and then click **Finish**.</span></span>
11. <span data-ttu-id="7660a-251">Когда мастер завершит создание расписания архивации, нажмите кнопку **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="7660a-251">After the wizard finishes creating the backup schedule, click **Close**.</span></span>

### <a name="enable-network-throttling"></a><span data-ttu-id="7660a-252">Включение регулирования сети</span><span class="sxs-lookup"><span data-stu-id="7660a-252">Enable network throttling</span></span>
<span data-ttu-id="7660a-253">Агент службы архивации Microsoft Azure обеспечивает регулирование сети.</span><span class="sxs-lookup"><span data-stu-id="7660a-253">The Microsoft Azure Backup agent provides network throttling.</span></span> <span data-ttu-id="7660a-254">Регулирование управляет тем, как пропускная способность сети используется во время передачи данных.</span><span class="sxs-lookup"><span data-stu-id="7660a-254">Throttling controls how network bandwidth is used during data transfer.</span></span> <span data-ttu-id="7660a-255">Это полезно, если вам нужно выполнить архивацию в рабочее время так, чтобы данная операция не мешала другим процессам, связанным с обработкой интернет-трафика.</span><span class="sxs-lookup"><span data-stu-id="7660a-255">This control can be helpful if you need to back up data during work hours but do not want the backup process to interfere with other Internet traffic.</span></span> <span data-ttu-id="7660a-256">Регулирование применяется при архивации и восстановлении.</span><span class="sxs-lookup"><span data-stu-id="7660a-256">Throttling applies to back up and restore activities.</span></span>

> [!NOTE]
> <span data-ttu-id="7660a-257">Регулирование сети недоступно в Windows Server 2008 R2 с пакетом обновления 1 (SP1), Windows Server 2008 с пакетом обновления 2 (SP2) или Windows 7 (с пакетами обновления).</span><span class="sxs-lookup"><span data-stu-id="7660a-257">Network throttling is not available on Windows Server 2008 R2 SP1, Windows Server 2008 SP2, or Windows 7 (with service packs).</span></span> <span data-ttu-id="7660a-258">Функция регулирования сети службы архивации Azure обеспечивает качество обслуживания (QoS) в локальной операционной системе.</span><span class="sxs-lookup"><span data-stu-id="7660a-258">The Azure Backup network throttling feature engages Quality of Service (QoS) on the local operating system.</span></span> <span data-ttu-id="7660a-259">Хотя служба архивации Azure может защитить эти операционные системы, версия качества обслуживания, доступная на этих платформах, не работает с регулированием сети службы архивации Azure.</span><span class="sxs-lookup"><span data-stu-id="7660a-259">Though Azure Backup can protect these operating systems, the version of QoS available on these platforms doesn't work with Azure Backup network throttling.</span></span> <span data-ttu-id="7660a-260">Регулирование сети можно использовать во всех остальных [поддерживаемых операционных системах](backup-azure-backup-faq.md).</span><span class="sxs-lookup"><span data-stu-id="7660a-260">Network throttling can be used on all other [supported operating systems](backup-azure-backup-faq.md).</span></span>
>
>

<span data-ttu-id="7660a-261">**Включение регулирования сети**</span><span class="sxs-lookup"><span data-stu-id="7660a-261">**To enable network throttling**</span></span>

1. <span data-ttu-id="7660a-262">В агенте службы архивации Microsoft Azure щелкните **Изменить свойства**.</span><span class="sxs-lookup"><span data-stu-id="7660a-262">In the Microsoft Azure Backup agent, click **Change Properties**.</span></span>

    ![Изменить свойства](./media/backup-configure-vault/change-properties.png)
2. <span data-ttu-id="7660a-264">На вкладке **Регулирование** установите флажок **Разрешить регулирование уровня использования пропускной способности интернет-канала для операций архивации**.</span><span class="sxs-lookup"><span data-stu-id="7660a-264">On the **Throttling** tab, select the **Enable internet bandwidth usage throttling for backup operations** check box.</span></span>

    ![Регулирование сети](./media/backup-configure-vault/throttling-dialog.png)
3. <span data-ttu-id="7660a-266">После включения регулирования укажите допустимую пропускную способность для передачи данных во время резервного копирования в **рабочие** и **нерабочие часы**.</span><span class="sxs-lookup"><span data-stu-id="7660a-266">After you have enabled throttling, specify the allowed bandwidth for backup data transfer during **Work hours** and **Non-work hours**.</span></span>

    <span data-ttu-id="7660a-267">Значения пропускной способности начинаются с 512 килобитов в секунду (Кбит/с) и могут перейти до 1023 мегабайтов в секунду (МБ/с).</span><span class="sxs-lookup"><span data-stu-id="7660a-267">The bandwidth values begin at 512 kilobits per second (Kbps) and can go up to 1,023 megabytes per second (MBps).</span></span> <span data-ttu-id="7660a-268">Можно также назначить время начала и окончания для **рабочих часов**и выбрать, какие дни недели считаются рабочими.</span><span class="sxs-lookup"><span data-stu-id="7660a-268">You can also designate the start and finish for **Work hours**, and which days of the week are considered work days.</span></span> <span data-ttu-id="7660a-269">Время, не входящее в назначенные рабочие часы, считается нерабочим.</span><span class="sxs-lookup"><span data-stu-id="7660a-269">Hours outside of designated work hours are considered non-work hours.</span></span>
4. <span data-ttu-id="7660a-270">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="7660a-270">Click **OK**.</span></span>

### <a name="to-back-up-files-and-folders-for-the-first-time"></a><span data-ttu-id="7660a-271">Архивация файлов и папок впервые</span><span class="sxs-lookup"><span data-stu-id="7660a-271">To back up files and folders for the first time</span></span>
1. <span data-ttu-id="7660a-272">В агенте службы архивации нажмите кнопку **Выполнить моментальную архивацию** , чтобы завершить начальное заполнение по сети.</span><span class="sxs-lookup"><span data-stu-id="7660a-272">In the backup agent, click **Back Up Now** to complete the initial seeding over the network.</span></span>

    ![Моментальная архивация Windows Server](./media/backup-configure-vault/backup-now.png)
2. <span data-ttu-id="7660a-274">На странице "Подтверждение" проверьте параметры, которые мастер будет использовать для архивации данных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="7660a-274">On the Confirmation page, review the settings that the Back Up Now Wizard will use to back up the machine.</span></span> <span data-ttu-id="7660a-275">Затем нажмите кнопку **Архивировать**.</span><span class="sxs-lookup"><span data-stu-id="7660a-275">Then click **Back Up**.</span></span>
3. <span data-ttu-id="7660a-276">Нажмите кнопку **Закрыть** , чтобы закрыть мастер.</span><span class="sxs-lookup"><span data-stu-id="7660a-276">Click **Close** to close the wizard.</span></span> <span data-ttu-id="7660a-277">Если сделать это до завершения архивации, мастер продолжит работу в фоновом режиме.</span><span class="sxs-lookup"><span data-stu-id="7660a-277">If you do this before the backup process finishes, the wizard continues to run in the background.</span></span>

<span data-ttu-id="7660a-278">После завершения начальной архивации в консоли службы архивации отобразится состояние **Задание выполнено** .</span><span class="sxs-lookup"><span data-stu-id="7660a-278">After the initial backup is completed, the **Job completed** status appears in the Backup console.</span></span>

![Первоначальное восстановление завершено](./media/backup-configure-vault/ircomplete.png)

## <a name="questions"></a><span data-ttu-id="7660a-280">Вопросы?</span><span class="sxs-lookup"><span data-stu-id="7660a-280">Questions?</span></span>
<span data-ttu-id="7660a-281">Если вы хотите задать вопрос или предложить добавить какие-либо функции, [отправьте нам свой отзыв](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="7660a-281">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7660a-282">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7660a-282">Next steps</span></span>
<span data-ttu-id="7660a-283">Дополнительные сведения об архивации виртуальных машин и других рабочих нагрузок см. в следующих разделах:</span><span class="sxs-lookup"><span data-stu-id="7660a-283">For additional information about backing up VMs or other workloads, see:</span></span>

* <span data-ttu-id="7660a-284">Теперь, когда вы выполнили резервное копирование файлов и папок, вы можете [управлять хранилищами и серверами](backup-azure-manage-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="7660a-284">Now that you've backed up your files and folders, you can [manage your vaults and servers](backup-azure-manage-windows-server.md).</span></span>
* <span data-ttu-id="7660a-285">Если необходимо восстановить резервную копию, см. статью о [восстановлении файлов на компьютере Windows](backup-azure-restore-windows-server.md).</span><span class="sxs-lookup"><span data-stu-id="7660a-285">If you need to restore a backup, use this article to [restore files to a Windows machine](backup-azure-restore-windows-server.md).</span></span>
