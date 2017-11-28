---
title: "aaaEnable репликации для виртуальных машин Azure tooanother регион Azure с помощью Azure Site Recovery | Документы Microsoft"
description: "Собраны действия hello необходимо tooanother репликации tooenable регион Azure для виртуальных машин Azure, с помощью службы Azure Site Recovery hello"
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
ms.openlocfilehash: 2fa03db45a18ccb8b9f31ed05589be0dd6d5f031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-enable-replication-for-azure-vms"></a><span data-ttu-id="d6fe8-103">Шаг 5. Включение репликации для виртуальных машин Azure</span><span class="sxs-lookup"><span data-stu-id="d6fe8-103">Step 5: Enable replication for Azure VMs</span></span>


<span data-ttu-id="d6fe8-104">После настройки [хранилище служб восстановления](azure-to-azure-walkthrough-vault.md), используйте репликацию виртуальных машин (ВМ), tooanother регион Azure этой статьи tooenable с [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d6fe8-104">After setting up a [Recovery Services vault](azure-to-azure-walkthrough-vault.md), use this article tooenable replication of virtual machines (VMs), tooanother Azure region, with [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="d6fe8-105">репликация tooenable, можно настроить источника и целевых параметров проверьте политику репликации hello и выберите требуется tooreplicate виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-105">tooenable replication, you set up source and target settings, verify hello replication policy, and select VMs you want tooreplicate.</span></span>

- <span data-ttu-id="d6fe8-106">После завершения hello статьи, виртуальных машин Azure должен репликация toohello вторичный регион Azure.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-106">When you finish hello article, your Azure VMs should be replicating toohello secondary Azure region.</span></span>
- <span data-ttu-id="d6fe8-107">Отправлять все комментарии hello нижней части этой статьи, или задать вопросы в hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="d6fe8-107">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

>[!NOTE]
>
> <span data-ttu-id="d6fe8-108">Репликация виртуальных машин Azure сейчас доступна в режиме предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-108">Azure VM replication is currently in preview.</span></span>


## <a name="select-hello-source"></a><span data-ttu-id="d6fe8-109">Выберите источник hello</span><span class="sxs-lookup"><span data-stu-id="d6fe8-109">Select hello source</span></span> 

1. <span data-ttu-id="d6fe8-110">В хранилищах службы восстановления, щелкните имя хранилища hello > **+ реплицировать**.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-110">In Recovery Services vaults, click hello vault name > **+Replicate**.</span></span>
2. <span data-ttu-id="d6fe8-111">В поле **Источник** выберите **Azure Preview**.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-111">In **Source**, select **Azure - PREVIEW**.</span></span>
2. <span data-ttu-id="d6fe8-112">В **исходное местоположение**выберите источник hello регион Azure, где работающие виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-112">In **Source location**, select hello source Azure region where your VMs are currently running.</span></span>
3. <span data-ttu-id="d6fe8-113">Выберите hello **модель развертывания виртуальной машины Azure** для виртуальных машин: **диспетчера ресурсов** или **классический**.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-113">Select hello **Azure virtual machine deployment model** for VMs: **Resource Manager** or **Classic**.</span></span>
4. <span data-ttu-id="d6fe8-114">Выберите hello **исходная группа ресурсов** для виртуальных машин диспетчера ресурсов, или **облачная служба** для классических виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-114">Select hello **Source resource group** for Resource Manager VMs, or **cloud service** for classic VMs.</span></span>
5. <span data-ttu-id="d6fe8-115">Нажмите кнопку **ОК** toosave hello параметры.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-115">Click **OK** toosave hello settings.</span></span>

    ![Настройка источника hello](./media/azure-to-azure-walkthrough-enable-replication/source.png)

## <a name="select-hello-vms"></a><span data-ttu-id="d6fe8-117">Выберите виртуальные машины hello</span><span class="sxs-lookup"><span data-stu-id="d6fe8-117">Select hello VMs</span></span>

<span data-ttu-id="d6fe8-118">Site Recovery извлекает список виртуальных машин, связанной с подпиской hello и ресурсов группы и облачная служба hello.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-118">Site Recovery retrieves a list of hello VMs associated with hello subscription and resource group/cloud service.</span></span>

1. <span data-ttu-id="d6fe8-119">В **виртуальные машины**, выберите виртуальные машины hello требуется tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-119">In **Virtual Machines**, select hello VMs you want tooreplicate.</span></span>
2. <span data-ttu-id="d6fe8-120">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-120">Click **OK**.</span></span>

    ![Выбор виртуальных машин](./media/azure-to-azure-walkthrough-enable-replication/vms.png)


## <a name="configure-settings"></a><span data-ttu-id="d6fe8-122">Настройка параметров</span><span class="sxs-lookup"><span data-stu-id="d6fe8-122">Configure settings</span></span>

<span data-ttu-id="d6fe8-123">Site Recovery предоставляет параметры по умолчанию для целевой регион hello (с учетом hello источника региональные параметры) и политика репликации hello:</span><span class="sxs-lookup"><span data-stu-id="d6fe8-123">Site Recovery provisions default settings for hello target region (based on hello source region settings), and hello replication policy:</span></span>

   - <span data-ttu-id="d6fe8-124">**Целевое расположение**: hello целевой регион требуется toouse для аварийного восстановления.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-124">**Target location**: hello target region you want toouse for disaster recovery.</span></span> <span data-ttu-id="d6fe8-125">Корпорация Майкрософт рекомендует соответствие hello расположение хранилище Site Recovery hello hello целевое расположение.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-125">We recommend that hello target location matches hello location of hello Site Recovery vault.</span></span>
   - <span data-ttu-id="d6fe8-126">**Целевая группа ресурсов**: toowhich группы ресурсов виртуальных машин Azure в целевой области hello будет принадлежать после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-126">**Target resource group**: Resource group toowhich Azure VMs in hello target region will belong after failover.</span></span> <span data-ttu-id="d6fe8-127">По умолчанию Site Recovery создает новую группу ресурсов в целевой области hello с суффиксом «asr».</span><span class="sxs-lookup"><span data-stu-id="d6fe8-127">By default, Site Recovery creates a new resource group in hello target region with an "asr" suffix.</span></span> 
   - <span data-ttu-id="d6fe8-128">**Целевой виртуальной сети**: hello сети, в которой виртуальные машины Azure в hello целевой регион будет находиться после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-128">**Target virtual network**: hello network in which Azure VMs in hello target region will be located after failover.</span></span> <span data-ttu-id="d6fe8-129">По умолчанию Site Recovery создает новую виртуальную сеть (и подсети) в целевой области hello с суффиксом «asr».</span><span class="sxs-lookup"><span data-stu-id="d6fe8-129">By default, Site Recovery creates a new virtual network (and subnets) in hello target region with an "asr" suffix.</span></span> <span data-ttu-id="d6fe8-130">Эта сеть является сетью сопоставленных tooyour источника.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-130">This network is mapped tooyour source network.</span></span> <span data-ttu-id="d6fe8-131">Обратите внимание, что после отработки отказа виртуальной машины можно назначить конкретный IP-адрес, при необходимости tooretain hello же IP-адрес в исходном и целевом расположении hello.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-131">Note that you can assign a specific IP address after failover of a VM, if you need tooretain hello same IP address in hello source and target locations.</span></span> 
   - <span data-ttu-id="d6fe8-132">**Кэширование учетных записей хранения**: Site Recovery использует учетную запись хранения в регионе источника hello.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-132">**Cache storage accounts**: Site Recovery uses a storage account in hello source region.</span></span> <span data-ttu-id="d6fe8-133">Изменения на исходных виртуальных отправляются toothis учетной записи, прежде чем репликации toohello целевое расположение.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-133">Changes on source VMs are sent toothis account, before replication toohello target location.</span></span> 
   - <span data-ttu-id="d6fe8-134">**Использовать учетные записи хранения**: по умолчанию Site Recovery создает новую учетную запись хранения в целевой регион hello, toomirror hello исходной учетной записи хранилища виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-134">**Target storage accounts**: By default, Site Recovery creates a new storage account in hello target region, toomirror hello source VM storage account.</span></span>
   -  <span data-ttu-id="d6fe8-135">**Целевые группы доступности**: по умолчанию Site Recovery создает новый доступности в целевой области hello с суффиксом «asr» hello.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-135">**Target availability sets**: By default, Site Recovery creates a new availability set in hello target region, with hello "asr" suffix.</span></span> 
   - <span data-ttu-id="d6fe8-136">**Replication policy name** (Имя политики репликации). Имя политики.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-136">**Replication policy name**: Policy name.</span></span>
   - <span data-ttu-id="d6fe8-137">**Хранение точки восстановления.** По умолчанию Site Recovery хранит точки восстановления 24 часа.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-137">**Recovery point retention**: By default Site Recovery keeps recovery points for 24 hours.</span></span> <span data-ttu-id="d6fe8-138">Вы можете задать значение от 1 до 72 часов.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-138">You can configure a value between 1 and 72 hours.</span></span>
   - <span data-ttu-id="d6fe8-139">**Периодичность создания моментальных снимков с согласованием приложений.** По умолчанию Site Recovery выполняет моментальные снимки с согласованием приложений каждые 4 часа.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-139">**App-consistent snapshot frequency**: By default Site Recovery takes an app-consistent snapshot every 4 hours.</span></span> <span data-ttu-id="d6fe8-140">Вы можете задать значение от 1 до 12 часов.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-140">You can configure any value between 1 and 12 hours.</span></span> <span data-ttu-id="d6fe8-141">Данные непрерывно реплицируются.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-141">Data is replicated continuously:</span></span>
    - <span data-ttu-id="d6fe8-142">При создании отказоустойчивые точки восстановления сохраняют согласованный порядок записи данных.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-142">Crash-consistent recovery points maintain consistent data write-order when created.</span></span> <span data-ttu-id="d6fe8-143">Этот тип точки восстановления обычно достаточно, если приложение спроектированный toorecover из аварийных без несогласованности данных</span><span class="sxs-lookup"><span data-stu-id="d6fe8-143">This type of recovery point is usually sufficient if your app is designed toorecover from a crash without data inconsistencies</span></span>
    - <span data-ttu-id="d6fe8-144">Отказоустойчивые точки восстановления создаются каждые пять минут.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-144">Crash-consistent recovery points are generated every few minutes.</span></span> <span data-ttu-id="d6fe8-145">С помощью этих toofail точек восстановления по и восстановление виртуальных машин обеспечивает целевой точки восстановления (RPO) в порядке hello минут.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-145">Using these recovery points toofail over and recover your VMs provides a Recovery Point Objective (RPO) in hello order of minutes.</span></span>
    - <span data-ttu-id="d6fe8-146">Точки восстановления, согласованной приложения (в согласованности toowrite порядок сложения) убедитесь, что работающие приложения выполнить все операции и очистить буферы toodisk (замораживание приложения).</span><span class="sxs-lookup"><span data-stu-id="d6fe8-146">App-consistent recovery points (in addition toowrite-order consistency) ensure that running apps complete all operations and flush buffers toodisk (application quiescing).</span></span> <span data-ttu-id="d6fe8-147">Мы рекомендуем использовать эти точки восстановления для приложений базы данных, таких как SQL Server, Oracle и Exchange.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-147">We recommend you use these recovery points for database apps such as SQL Server, Oracle, and Exchange.</span></span>
        
    ![Настройка параметров](./media/azure-to-azure-walkthrough-enable-replication/settings.png)


### <a name="modify-settings"></a><span data-ttu-id="d6fe8-149">Изменение параметров</span><span class="sxs-lookup"><span data-stu-id="d6fe8-149">Modify settings</span></span>

<span data-ttu-id="d6fe8-150">Если параметры политики toomodify цель и репликации, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="d6fe8-150">If you want toomodify target and replication policy settings, do hello following:</span></span>

1. <span data-ttu-id="d6fe8-151">tooview или изменить целевые параметры, нажмите кнопку **параметры**.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-151">tooview or modify target settings, click **Settings**.</span></span>
2. <span data-ttu-id="d6fe8-152">по умолчанию целевой toooverride hello, параметры, выберите пункт **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-152">toooverride hello default target settings, click **Customize**.</span></span> <span data-ttu-id="d6fe8-153">Вы можете указать целевую группу ресурсов, виртуальную сеть, группу доступности и целевую учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-153">You can specify a target resource group, virtual network, availability set, and target storage account.</span></span> <span data-ttu-id="d6fe8-154">Группы доступности можно добавить только в том случае, если виртуальные машины являются частью набора в области источника hello.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-154">You can only add availability sets if VMs are part of a set in hello source region.</span></span>

    ![Настройка параметров](./media/azure-to-azure-walkthrough-enable-replication/customize-target.png)

3. <span data-ttu-id="d6fe8-156">параметры репликации toooverride точками восстановления и моментальных снимков, приемлемых для приложений, щелкните **Настройка** Далее слишком**политику репликации**.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-156">toooverride replication settings for recovery points and app-consistent snapshots, click **Customize** next too**Replication Policy**.</span></span>
 
    ![Настройка параметров](./media/azure-to-azure-walkthrough-enable-replication/customize-policy.png)

4. <span data-ttu-id="d6fe8-158">Щелкните toostart подготовки hello целевые ресурсы, **создать целевые ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-158">toostart provisioning hello target resources, click **Create target resources**.</span></span> <span data-ttu-id="d6fe8-159">Подготовка занимает несколько минут.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-159">Provisioning takes a minute or so.</span></span> <span data-ttu-id="d6fe8-160">Не закрывайте колонке hello во время инициализации или вы получите toostart по.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-160">Don't close hello blade during provisioning, or you'll have toostart over.</span></span>




## <a name="enable-replication"></a><span data-ttu-id="d6fe8-161">Включение репликации</span><span class="sxs-lookup"><span data-stu-id="d6fe8-161">Enable replication</span></span>

1. <span data-ttu-id="d6fe8-162">В разделе **Параметры** щелкните **Включить репликацию**.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-162">In **Settings**, click **Enable replication**.</span></span> <span data-ttu-id="d6fe8-163">Это позволяет hello виртуальных машин, которые вы выбрали начальную репликацию.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-163">This enables initial replication of hello VMs you selected.</span></span> <span data-ttu-id="d6fe8-164">Состояние начальной репликации может занять некоторое время toorefresh.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-164">Initial replication status might take some time toorefresh.</span></span> <span data-ttu-id="d6fe8-165">Нажмите кнопку **обновление** tooget hello последнее состояние.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-165">Click **Refresh** tooget hello latest status.</span></span>

2. <span data-ttu-id="d6fe8-166">Вы можете отслеживать ход выполнения hello **включить защиту** задания в **параметры** > **заданий** > **задания восстановления сайта**.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-166">You can track progress of hello **Enable protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span>

3. <span data-ttu-id="d6fe8-167">В **параметры** > **реплицируются элементы**, можно просмотреть состояние hello виртуальных машин и hello ход выполнения начальной репликации.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-167">In **Settings** > **Replicated Items**, you can view hello status of VMs and hello initial replication progress.</span></span> <span data-ttu-id="d6fe8-168">Щелкните toodrill ВМ hello его параметры.</span><span class="sxs-lookup"><span data-stu-id="d6fe8-168">Click hello VM toodrill down into its settings.</span></span>



## <a name="next-steps"></a><span data-ttu-id="d6fe8-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d6fe8-169">Next steps</span></span>

<span data-ttu-id="d6fe8-170">Go слишком[шаг 6: запустите тестовую отработку отказа](azure-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="d6fe8-170">Go too[Step 6: Run a test failover](azure-to-azure-walkthrough-test-failover.md)</span></span>
