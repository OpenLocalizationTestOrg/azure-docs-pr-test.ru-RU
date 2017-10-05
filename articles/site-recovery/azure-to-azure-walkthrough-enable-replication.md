---
title: "Включение репликации виртуальных машин Azure в другой регион Azure с помощью Azure Site Recovery | Документация Майкрософт"
description: "В этой статье кратко описаны шаги для включения репликации виртуальных машин Azure в другой регион Azure с помощью службы Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a309644f-d36b-4188-bba7-ad45a2d9bede
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 8/01/2017
ms.author: raynew
ms.openlocfilehash: f426ba4341e61d3c7da820d7d5097b217e94ca0e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="step-5-enable-replication-for-azure-vms"></a><span data-ttu-id="4488f-103">Шаг 5. Включение репликации для виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="4488f-103">Step 5: Enable replication for Azure VMs</span></span>


<span data-ttu-id="4488f-104">После настройки [хранилища служб восстановления](azure-to-azure-walkthrough-vault.md) используйте сведения в этой статье, чтобы включить репликацию виртуальных машин в другой регион Azure с помощью [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4488f-104">After setting up a [Recovery Services vault](azure-to-azure-walkthrough-vault.md), use this article to enable replication of virtual machines (VMs), to another Azure region, with [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="4488f-105">Чтобы включить репликацию, настройте исходные и целевые параметры, проверьте политику репликации и выберите виртуальные машины, которые необходимо реплицировать.</span><span class="sxs-lookup"><span data-stu-id="4488f-105">To enable replication, you set up source and target settings, verify the replication policy, and select VMs you want to replicate.</span></span>

- <span data-ttu-id="4488f-106">Изучив эту статью, вы сможете реплицировать виртуальные машины Azure в дополнительный регион Azure.</span><span class="sxs-lookup"><span data-stu-id="4488f-106">When you finish the article, your Azure VMs should be replicating to the secondary Azure region.</span></span>
- <span data-ttu-id="4488f-107">Все комментарии можно добавить в конце этой статьи. Вопросы можно задать на [форуме по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="4488f-107">Post any comments at the bottom of this article, or ask questions in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

>[!NOTE]
>
> <span data-ttu-id="4488f-108">Репликация виртуальных машин Azure сейчас доступна в режиме предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="4488f-108">Azure VM replication is currently in preview.</span></span>


## <a name="select-the-source"></a><span data-ttu-id="4488f-109">Выбор источника</span><span class="sxs-lookup"><span data-stu-id="4488f-109">Select the source</span></span> 

1. <span data-ttu-id="4488f-110">В хранилище служб восстановления щелкните имя хранилища и выберите **Реплицировать**.</span><span class="sxs-lookup"><span data-stu-id="4488f-110">In Recovery Services vaults, click the vault name > **+Replicate**.</span></span>
2. <span data-ttu-id="4488f-111">В поле **Источник** выберите **Azure Preview**.</span><span class="sxs-lookup"><span data-stu-id="4488f-111">In **Source**, select **Azure - PREVIEW**.</span></span>
2. <span data-ttu-id="4488f-112">В поле **Исходное расположение** выберите исходный регион Azure, в котором сейчас запущены виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="4488f-112">In **Source location**, select the source Azure region where your VMs are currently running.</span></span>
3. <span data-ttu-id="4488f-113">Для виртуальных машин **Resource Manager** или **классических** виртуальных машин выберите **модель развертывания виртуальной машины Azure**.</span><span class="sxs-lookup"><span data-stu-id="4488f-113">Select the **Azure virtual machine deployment model** for VMs: **Resource Manager** or **Classic**.</span></span>
4. <span data-ttu-id="4488f-114">Выберите **исходную группу ресурсов** для виртуальных машин Resource Manager или **облачную службу** для классических виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="4488f-114">Select the **Source resource group** for Resource Manager VMs, or **cloud service** for classic VMs.</span></span>
5. <span data-ttu-id="4488f-115">Нажмите кнопку **ОК**, чтобы сохранить настройки.</span><span class="sxs-lookup"><span data-stu-id="4488f-115">Click **OK** to save the settings.</span></span>

    ![Настройка источника](./media/azure-to-azure-walkthrough-enable-replication/source.png)

## <a name="select-the-vms"></a><span data-ttu-id="4488f-117">Выбор виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="4488f-117">Select the VMs</span></span>

<span data-ttu-id="4488f-118">Site Recovery получает список виртуальных машин, связанных с подпиской и группой ресурсов или облачной службой.</span><span class="sxs-lookup"><span data-stu-id="4488f-118">Site Recovery retrieves a list of the VMs associated with the subscription and resource group/cloud service.</span></span>

1. <span data-ttu-id="4488f-119">В разделе **Виртуальные машины** выберите виртуальные машины, которые необходимо реплицировать.</span><span class="sxs-lookup"><span data-stu-id="4488f-119">In **Virtual Machines**, select the VMs you want to replicate.</span></span>
2. <span data-ttu-id="4488f-120">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="4488f-120">Click **OK**.</span></span>

    ![Выбор виртуальных машин](./media/azure-to-azure-walkthrough-enable-replication/vms.png)


## <a name="configure-settings"></a><span data-ttu-id="4488f-122">Настройка параметров</span><span class="sxs-lookup"><span data-stu-id="4488f-122">Configure settings</span></span>

<span data-ttu-id="4488f-123">Site Recovery подготавливает параметры по умолчанию для целевого региона (на основе параметров исходного региона) и политику репликации.</span><span class="sxs-lookup"><span data-stu-id="4488f-123">Site Recovery provisions default settings for the target region (based on the source region settings), and the replication policy:</span></span>

   - <span data-ttu-id="4488f-124">**Целевое расположение.** Целевой регион, который будет использоваться для аварийного восстановления.</span><span class="sxs-lookup"><span data-stu-id="4488f-124">**Target location**: The target region you want to use for disaster recovery.</span></span> <span data-ttu-id="4488f-125">Мы рекомендуем, чтобы целевое расположение соответствовало расположению хранилища Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="4488f-125">We recommend that the target location matches the location of the Site Recovery vault.</span></span>
   - <span data-ttu-id="4488f-126">**Группа целевых ресурсов.** Группа ресурсов, к которой будут принадлежать виртуальные машины Azure в целевом регионе после выполнения отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="4488f-126">**Target resource group**: Resource group to which Azure VMs in the target region will belong after failover.</span></span> <span data-ttu-id="4488f-127">По умолчанию Site Recovery создает группу ресурсов в целевом регионе с суффиксом asr.</span><span class="sxs-lookup"><span data-stu-id="4488f-127">By default, Site Recovery creates a new resource group in the target region with an "asr" suffix.</span></span> 
   - <span data-ttu-id="4488f-128">**Target virtual network** (Целевая виртуальная сеть). Сеть, в которой будут размещаться виртуальные машины Azure в целевом регионе после выполнения отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="4488f-128">**Target virtual network**: The network in which Azure VMs in the target region will be located after failover.</span></span> <span data-ttu-id="4488f-129">По умолчанию Site Recovery создает виртуальную сеть (и подсети) в целевом регионе с суффиксом asr.</span><span class="sxs-lookup"><span data-stu-id="4488f-129">By default, Site Recovery creates a new virtual network (and subnets) in the target region with an "asr" suffix.</span></span> <span data-ttu-id="4488f-130">Эта сеть сопоставляется с исходной сетью.</span><span class="sxs-lookup"><span data-stu-id="4488f-130">This network is mapped to your source network.</span></span> <span data-ttu-id="4488f-131">Чтобы сохранить тот же IP-адрес в исходном и целевом расположении, можно назначить определенный IP-адрес после выполнения отработки отказа виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="4488f-131">Note that you can assign a specific IP address after failover of a VM, if you need to retain the same IP address in the source and target locations.</span></span> 
   - <span data-ttu-id="4488f-132">**Cache storage accounts** (Учетные записи хранения кэша). Site Recovery использует учетную запись хранения в исходном регионе.</span><span class="sxs-lookup"><span data-stu-id="4488f-132">**Cache storage accounts**: Site Recovery uses a storage account in the source region.</span></span> <span data-ttu-id="4488f-133">Изменения в исходных виртуальных машинах отправляются в эту учетную запись перед репликацией в целевое расположение.</span><span class="sxs-lookup"><span data-stu-id="4488f-133">Changes on source VMs are sent to this account, before replication to the target location.</span></span> 
   - <span data-ttu-id="4488f-134">**Target storage accounts** (Целевые учетные записи хранения). По умолчанию Site Recovery создает учетную запись хранения в целевом регионе, чтобы отобразить учетную запись хранения исходной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="4488f-134">**Target storage accounts**: By default, Site Recovery creates a new storage account in the target region, to mirror the source VM storage account.</span></span>
   -  <span data-ttu-id="4488f-135">**Target availability sets** (Целевые группы доступности). По умолчанию Site Recovery создает группу доступности в целевом регионе с суффиксом asr.</span><span class="sxs-lookup"><span data-stu-id="4488f-135">**Target availability sets**: By default, Site Recovery creates a new availability set in the target region, with the "asr" suffix.</span></span> 
   - <span data-ttu-id="4488f-136">**Replication policy name** (Имя политики репликации). Имя политики.</span><span class="sxs-lookup"><span data-stu-id="4488f-136">**Replication policy name**: Policy name.</span></span>
   - <span data-ttu-id="4488f-137">**Хранение точки восстановления.** По умолчанию Site Recovery хранит точки восстановления 24 часа.</span><span class="sxs-lookup"><span data-stu-id="4488f-137">**Recovery point retention**: By default Site Recovery keeps recovery points for 24 hours.</span></span> <span data-ttu-id="4488f-138">Вы можете задать значение от 1 до 72 часов.</span><span class="sxs-lookup"><span data-stu-id="4488f-138">You can configure a value between 1 and 72 hours.</span></span>
   - <span data-ttu-id="4488f-139">**Периодичность создания моментальных снимков с согласованием приложений.** По умолчанию Site Recovery выполняет моментальные снимки с согласованием приложений каждые 4 часа.</span><span class="sxs-lookup"><span data-stu-id="4488f-139">**App-consistent snapshot frequency**: By default Site Recovery takes an app-consistent snapshot every 4 hours.</span></span> <span data-ttu-id="4488f-140">Вы можете задать значение от 1 до 12 часов.</span><span class="sxs-lookup"><span data-stu-id="4488f-140">You can configure any value between 1 and 12 hours.</span></span> <span data-ttu-id="4488f-141">Данные непрерывно реплицируются.</span><span class="sxs-lookup"><span data-stu-id="4488f-141">Data is replicated continuously:</span></span>
    - <span data-ttu-id="4488f-142">При создании отказоустойчивые точки восстановления сохраняют согласованный порядок записи данных.</span><span class="sxs-lookup"><span data-stu-id="4488f-142">Crash-consistent recovery points maintain consistent data write-order when created.</span></span> <span data-ttu-id="4488f-143">Этого типа точки восстановления обычно достаточно, если ваше приложение позволяет восстанавливать данные после сбоя, избегая их несогласованности.</span><span class="sxs-lookup"><span data-stu-id="4488f-143">This type of recovery point is usually sufficient if your app is designed to recover from a crash without data inconsistencies</span></span>
    - <span data-ttu-id="4488f-144">Отказоустойчивые точки восстановления создаются каждые пять минут.</span><span class="sxs-lookup"><span data-stu-id="4488f-144">Crash-consistent recovery points are generated every few minutes.</span></span> <span data-ttu-id="4488f-145">Использование этих точек восстановления для выполнения отработки отказа и восстановления виртуальных машин предоставляет целевую точку восстановления (RPO) каждые несколько минут.</span><span class="sxs-lookup"><span data-stu-id="4488f-145">Using these recovery points to fail over and recover your VMs provides a Recovery Point Objective (RPO) in the order of minutes.</span></span>
    - <span data-ttu-id="4488f-146">Согласованные с приложениями точки восстановления (в дополнение к согласованному порядку записи данных) гарантируют, что запущенные приложения завершают все операции и сбрасывают буферы на диск (замораживают приложение).</span><span class="sxs-lookup"><span data-stu-id="4488f-146">App-consistent recovery points (in addition to write-order consistency) ensure that running apps complete all operations and flush buffers to disk (application quiescing).</span></span> <span data-ttu-id="4488f-147">Мы рекомендуем использовать эти точки восстановления для приложений базы данных, таких как SQL Server, Oracle и Exchange.</span><span class="sxs-lookup"><span data-stu-id="4488f-147">We recommend you use these recovery points for database apps such as SQL Server, Oracle, and Exchange.</span></span>
        
    ![Настройка параметров](./media/azure-to-azure-walkthrough-enable-replication/settings.png)


### <a name="modify-settings"></a><span data-ttu-id="4488f-149">Изменение параметров</span><span class="sxs-lookup"><span data-stu-id="4488f-149">Modify settings</span></span>

<span data-ttu-id="4488f-150">Если вы хотите изменить параметры целевого объекта и параметры политики репликации, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="4488f-150">If you want to modify target and replication policy settings, do the following:</span></span>

1. <span data-ttu-id="4488f-151">Щелкните **Параметры**, чтобы просмотреть или изменить параметры целевого объекта.</span><span class="sxs-lookup"><span data-stu-id="4488f-151">To view or modify target settings, click **Settings**.</span></span>
2. <span data-ttu-id="4488f-152">Чтобы переопределить стандартные параметры целевого объекта, щелкните **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="4488f-152">To override the default target settings, click **Customize**.</span></span> <span data-ttu-id="4488f-153">Вы можете указать целевую группу ресурсов, виртуальную сеть, группу доступности и целевую учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="4488f-153">You can specify a target resource group, virtual network, availability set, and target storage account.</span></span> <span data-ttu-id="4488f-154">Группы доступности можно добавить, только если виртуальные машины входят в состав исходного региона.</span><span class="sxs-lookup"><span data-stu-id="4488f-154">You can only add availability sets if VMs are part of a set in the source region.</span></span>

    ![Настройка параметров](./media/azure-to-azure-walkthrough-enable-replication/customize-target.png)

3. <span data-ttu-id="4488f-156">Чтобы переопределить параметры репликации точек восстановления и моментальных снимков с согласованием приложений, щелкните **Настройка** рядом с **Политика репликации**.</span><span class="sxs-lookup"><span data-stu-id="4488f-156">To override replication settings for recovery points and app-consistent snapshots, click **Customize** next to **Replication Policy**.</span></span>
 
    ![Настройка параметров](./media/azure-to-azure-walkthrough-enable-replication/customize-policy.png)

4. <span data-ttu-id="4488f-158">Чтобы начать подготовку целевых ресурсов, щелкните **Create target resources** (Создать целевые ресурсы).</span><span class="sxs-lookup"><span data-stu-id="4488f-158">To start provisioning the target resources, click **Create target resources**.</span></span> <span data-ttu-id="4488f-159">Подготовка занимает несколько минут.</span><span class="sxs-lookup"><span data-stu-id="4488f-159">Provisioning takes a minute or so.</span></span> <span data-ttu-id="4488f-160">Не закрывайте колонку во время подготовки, в противном случае нужно будет начать все сначала.</span><span class="sxs-lookup"><span data-stu-id="4488f-160">Don't close the blade during provisioning, or you'll have to start over.</span></span>




## <a name="enable-replication"></a><span data-ttu-id="4488f-161">Включение репликации</span><span class="sxs-lookup"><span data-stu-id="4488f-161">Enable replication</span></span>

1. <span data-ttu-id="4488f-162">В разделе **Параметры** щелкните **Включить репликацию**.</span><span class="sxs-lookup"><span data-stu-id="4488f-162">In **Settings**, click **Enable replication**.</span></span> <span data-ttu-id="4488f-163">Это позволяет включить начальную репликацию выбранных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="4488f-163">This enables initial replication of the VMs you selected.</span></span> <span data-ttu-id="4488f-164">Обновление состояния начальной репликации может занять некоторое время.</span><span class="sxs-lookup"><span data-stu-id="4488f-164">Initial replication status might take some time to refresh.</span></span> <span data-ttu-id="4488f-165">Щелкните **Обновить**, чтобы вывести актуальное состояние.</span><span class="sxs-lookup"><span data-stu-id="4488f-165">Click **Refresh** to get the latest status.</span></span>

2. <span data-ttu-id="4488f-166">Ход выполнения задания **включения защиты** можно отслеживать, выбрав **Параметры** > **Задания** > **Site Recovery Jobs** (Задания Site Recovery).</span><span class="sxs-lookup"><span data-stu-id="4488f-166">You can track progress of the **Enable protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span>

3. <span data-ttu-id="4488f-167">Выберите **Параметры** > **Реплицированные элементы**, чтобы просмотреть состояние виртуальных машин и ход выполнения начальной репликации.</span><span class="sxs-lookup"><span data-stu-id="4488f-167">In **Settings** > **Replicated Items**, you can view the status of VMs and the initial replication progress.</span></span> <span data-ttu-id="4488f-168">Выберите виртуальную машину, чтобы просмотреть ее параметры.</span><span class="sxs-lookup"><span data-stu-id="4488f-168">Click the VM to drill down into its settings.</span></span>



## <a name="next-steps"></a><span data-ttu-id="4488f-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4488f-169">Next steps</span></span>

<span data-ttu-id="4488f-170">См. [раздел о выполнении тестовой отработки отказа (шаг 6)](azure-to-azure-walkthrough-test-failover.md).</span><span class="sxs-lookup"><span data-stu-id="4488f-170">Go to [Step 6: Run a test failover](azure-to-azure-walkthrough-test-failover.md)</span></span>
