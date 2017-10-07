---
title: "Реплицировать виртуальные машины Azure между регионами Azure для аварийного восстановления: Azure tooAzure | Документы Microsoft"
description: "Собраны действия hello, необходимо, чтобы виртуальные машины Azure tooreplicate между регионами Azure (Azure в Azure) со службой Azure Site Recovery hello для аварийного восстановления."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: raynew
ms.openlocfilehash: c4c425af260a9bcc3dd4dcc13da26109e20f03bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a><span data-ttu-id="fb43b-103">Репликация виртуальных машин Azure между регионами с помощью Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="fb43b-103">Replicate Azure VMs between regions with Azure Site Recovery</span></span>

>[!NOTE]
>
> <span data-ttu-id="fb43b-104">Репликация Azure Site Recovery для виртуальных машин Azure сейчас доступна в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="fb43b-104">Azure Site Recovery replication for Azure virtual machines (VMs) is currently in preview.</span></span>

<span data-ttu-id="fb43b-105">В этой статье описывается, как hello tooreplicate виртуальных машинах Azure между регионами Azure с помощью [Site Recovery](site-recovery-overview.md) в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="fb43b-105">This article describes how tooreplicate Azure VMs between Azure regions by using hello [Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="fb43b-106">Учет комментарии и вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="fb43b-106">Post comments and questions at hello bottom of this article or on hello [Azure Recovery Services forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="disaster-recovery-in-azure"></a><span data-ttu-id="fb43b-107">Аварийное восстановление в Azure</span><span class="sxs-lookup"><span data-stu-id="fb43b-107">Disaster recovery in Azure</span></span>

<span data-ttu-id="fb43b-108">Встроенные инфраструктуры Azure и функции contribute стратегии доступности надежной и гибкой tooa для рабочих нагрузок, работающих на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="fb43b-108">Built-in Azure infrastructure capabilities and features contribute tooa robust and resilient availability strategy for workloads that run on Azure VMs.</span></span> <span data-ttu-id="fb43b-109">Тем не менее существует множество причин, почему вам необходимо tooplan аварийного восстановления между регионами Azure самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="fb43b-109">However, there are many reasons why you need tooplan for disaster recovery between Azure regions yourself:</span></span>

- <span data-ttu-id="fb43b-110">Необходимо toomeet рекомендациям по соответствию для конкретных приложений и рабочих нагрузок, требующих непрерывность бизнес-процессов и стратегии аварийного восстановления (BCDR).</span><span class="sxs-lookup"><span data-stu-id="fb43b-110">You need toomeet compliance guidelines for specific apps and workloads that require a business continuity and disaster recovery (BCDR) strategy.</span></span>
- <span data-ttu-id="fb43b-111">Требуется возможность tooprotect hello и восстановить виртуальные машины Azure на основе на ваш бизнес-решений, а не только на основе встроенных функциональности Azure.</span><span class="sxs-lookup"><span data-stu-id="fb43b-111">You want hello ability tooprotect and recover Azure VMs based on your business decisions, and not only based on inbuilt Azure functionality.</span></span>
- <span data-ttu-id="fb43b-112">Необходимо tootest отработки отказа и восстановления в соответствии с потребностями бизнеса и соответствия требованиям без влияния на производство.</span><span class="sxs-lookup"><span data-stu-id="fb43b-112">You need tootest failover and recovery in accordance with your business and compliance needs, with no impact on production.</span></span>
- <span data-ttu-id="fb43b-113">Требуется toofail над областью восстановления toohello hello для события сбоя и легко ошибкой задней toohello исходного источника области.</span><span class="sxs-lookup"><span data-stu-id="fb43b-113">You need toofail over toohello recovery region in hello event of a disaster and fail back toohello original source region seamlessly.</span></span>

<span data-ttu-id="fb43b-114">Используйте службу восстановления сайтов для toohelp репликации виртуальной Машины Azure в Azure можно выполнить все эти задачи.</span><span class="sxs-lookup"><span data-stu-id="fb43b-114">Use Site Recovery for Azure-to-Azure VM replication toohelp you do all these tasks.</span></span>


## <a name="why-use-site-recovery"></a><span data-ttu-id="fb43b-115">Зачем использовать Site Recovery?</span><span class="sxs-lookup"><span data-stu-id="fb43b-115">Why use Site Recovery?</span></span>      

<span data-ttu-id="fb43b-116">Site Recovery предоставляет tooreplicate простой способ виртуальных машинах Azure между регионами.</span><span class="sxs-lookup"><span data-stu-id="fb43b-116">Site Recovery provides a simple way tooreplicate Azure VMs between regions:</span></span>

- <span data-ttu-id="fb43b-117">**Автоматическое развертывание**.</span><span class="sxs-lookup"><span data-stu-id="fb43b-117">**Automatic deployment**.</span></span> <span data-ttu-id="fb43b-118">В отличие от репликации активных модели нет необходимости дорогостоящим и сложным инфраструктуры hello дополнительный регион.</span><span class="sxs-lookup"><span data-stu-id="fb43b-118">Unlike an active-active replication model, there's no need for an expensive and complex infrastructure in hello secondary region.</span></span> <span data-ttu-id="fb43b-119">При включении репликации Site Recovery автоматически создает hello необходимые ресурсы в hello целевой области, на основе параметров исходной области.</span><span class="sxs-lookup"><span data-stu-id="fb43b-119">When you enable replication, Site Recovery automatically creates hello required resources in hello target region, based on source region settings.</span></span>
- <span data-ttu-id="fb43b-120">**Управление регионами**.</span><span class="sxs-lookup"><span data-stu-id="fb43b-120">**Control regions**.</span></span> <span data-ttu-id="fb43b-121">С помощью Site Recovery можно реплицировать из какой-либо областью tooany области континент.</span><span class="sxs-lookup"><span data-stu-id="fb43b-121">With Site Recovery, you can replicate from any region tooany region within a continent.</span></span> <span data-ttu-id="fb43b-122">Сравните это с геоизбыточным хранилищем с доступом для чтения, которое выполняет асинхронную репликацию только между стандартными [парами регионов](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).</span><span class="sxs-lookup"><span data-stu-id="fb43b-122">Compare this with read-access geo-redundant storage, which replicates asynchronously between standard [paired regions](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) only.</span></span> <span data-ttu-id="fb43b-123">Географически избыточное хранилище с доступом на чтение предоставляет доступ только для чтения toohello данные в целевой области hello.</span><span class="sxs-lookup"><span data-stu-id="fb43b-123">Read-access geo-redundant storage provides read-only access toohello data in hello target region.</span></span>
- <span data-ttu-id="fb43b-124">**Автоматическая репликация**.</span><span class="sxs-lookup"><span data-stu-id="fb43b-124">**Automated replication**.</span></span> <span data-ttu-id="fb43b-125">Site Recovery предоставляет автоматическую непрерывную репликацию.</span><span class="sxs-lookup"><span data-stu-id="fb43b-125">Site Recovery provides automated continuous replication.</span></span> <span data-ttu-id="fb43b-126">Отработку отказа и восстановление размещения можно активировать одним щелчком мыши.</span><span class="sxs-lookup"><span data-stu-id="fb43b-126">Failover and failback can be triggered with a single click.</span></span>
- <span data-ttu-id="fb43b-127">**RTO и RPO**.</span><span class="sxs-lookup"><span data-stu-id="fb43b-127">**RTO and RPO**.</span></span> <span data-ttu-id="fb43b-128">Site Recovery позволяет пользоваться преимуществами hello Azure сетевой инфраструктуре, соединяющей tookeep областей RTO и RPO очень мало.</span><span class="sxs-lookup"><span data-stu-id="fb43b-128">Site Recovery takes advantage of hello Azure network infrastructure that connects regions tookeep RTO and RPO very low.</span></span>
- <span data-ttu-id="fb43b-129">**Тестирование**.</span><span class="sxs-lookup"><span data-stu-id="fb43b-129">**Testing**.</span></span> <span data-ttu-id="fb43b-130">Вы можете выполнять отработку аварийного восстановления с тестовой отработкой отказа по запросу по мере необходимости, не влияя на производственные рабочие нагрузки или текущую репликацию.</span><span class="sxs-lookup"><span data-stu-id="fb43b-130">You can run disaster-recovery drills with on-demand test failovers, as and when needed, without affecting your production workloads or ongoing replication.</span></span>
- <span data-ttu-id="fb43b-131">**Планы восстановления**.</span><span class="sxs-lookup"><span data-stu-id="fb43b-131">**Recovery plans**.</span></span> <span data-ttu-id="fb43b-132">Можно использовать планы восстановления tooorchestrate при отработке отказа и восстановлением размещения hello всего приложения, запущенного на несколько виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="fb43b-132">You can use recovery plans tooorchestrate failover and failback of hello entire application running on multiple VMs.</span></span> <span data-ttu-id="fb43b-133">Hello функциональные возможности плана восстановления имеет широкие возможности первого класса интеграции с модулями Runbook службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="fb43b-133">hello recovery plan feature has rich first-class integration with Azure automation runbooks.</span></span>


## <a name="deployment-summary"></a><span data-ttu-id="fb43b-134">Сводка по развертыванию</span><span class="sxs-lookup"><span data-stu-id="fb43b-134">Deployment summary</span></span>

<span data-ttu-id="fb43b-135">Ниже приведена сводка необходимых tooset toodo репликацию виртуальных машин между регионах Azure:</span><span class="sxs-lookup"><span data-stu-id="fb43b-135">Here's a summary of what you need toodo tooset up replication of VMs between Azure regions:</span></span>

1. <span data-ttu-id="fb43b-136">Создайте хранилище служб восстановления,</span><span class="sxs-lookup"><span data-stu-id="fb43b-136">Create a Recovery Services vault.</span></span> <span data-ttu-id="fb43b-137">хранилище Hello содержит параметры конфигурации и управляет репликации.</span><span class="sxs-lookup"><span data-stu-id="fb43b-137">hello vault contains configuration settings and orchestrates replication.</span></span>
2. <span data-ttu-id="fb43b-138">Включите репликацию hello виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="fb43b-138">Enable replication for hello Azure VMs.</span></span>
3. <span data-ttu-id="fb43b-139">Выполните тест отработки отказа toomake, убедиться, что все работает должным образом.</span><span class="sxs-lookup"><span data-stu-id="fb43b-139">Run a test failover toomake sure that everything's working as expected.</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="fb43b-140">Вы можете проверить hello [Матрица поддержки репликации виртуальной Машины Azure](./site-recovery-support-matrix-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="fb43b-140">You can check hello [support matrix for Azure VM replication](./site-recovery-support-matrix-azure-to-azure.md).</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="fb43b-141">Сведения о как tooconfigure hello исходящие подключения к сети для виртуальных машин Azure для восстановления сайта репликации требуется разделе hello [сети документ руководства по](./site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="fb43b-141">For information on how tooconfigure hello required network outbound connectivity for Azure VMs for Site Recovery replication, see hello [networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md).</span></span>

### <a name="before-you-start"></a><span data-ttu-id="fb43b-142">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="fb43b-142">Before you start</span></span>

* <span data-ttu-id="fb43b-143">Учетная запись пользователя Azure должен toohave определенных [разрешений](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable репликацию виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="fb43b-143">Your Azure user account needs toohave certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of an Azure virtual machine.</span></span>
* <span data-ttu-id="fb43b-144">Ваша подписка Azure должно быть включено toocreate виртуальные машины в целевом расположении hello, что требуется toouse как hello аварийного восстановления область.</span><span class="sxs-lookup"><span data-stu-id="fb43b-144">Your Azure subscription should be enabled toocreate VMs in hello target location that you want toouse as hello disaster recovery region.</span></span> <span data-ttu-id="fb43b-145">Обратитесь в службу поддержки tooenable hello требуется квота.</span><span class="sxs-lookup"><span data-stu-id="fb43b-145">Contact support tooenable hello required quota.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="fb43b-146">Создание хранилища служб восстановления</span><span class="sxs-lookup"><span data-stu-id="fb43b-146">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> <span data-ttu-id="fb43b-147">Рекомендуется создать хранилище служб восстановления hello в hello место хранения вашей tooreplicate виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="fb43b-147">We recommend that you create hello Recovery Services vault in hello location where you want your VMs tooreplicate.</span></span> <span data-ttu-id="fb43b-148">Например, если в целевом расположении hello центральный нам, создайте хранилище hello в **центральной части США**.</span><span class="sxs-lookup"><span data-stu-id="fb43b-148">For example, if your target location is hello central US, create hello vault in **Central US**.</span></span>

## <a name="enable-replication"></a><span data-ttu-id="fb43b-149">Включение репликации</span><span class="sxs-lookup"><span data-stu-id="fb43b-149">Enable replication</span></span>

<span data-ttu-id="fb43b-150">В **хранилищ служб восстановления**, щелкните имя хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="fb43b-150">In **Recovery Services vaults**, click hello vault name.</span></span> <span data-ttu-id="fb43b-151">В хранилище hello щелкните hello **+ реплицировать** кнопки.</span><span class="sxs-lookup"><span data-stu-id="fb43b-151">In hello vault, click hello **+Replicate** button.</span></span>

### <a name="step-1-configure-hello-source"></a><span data-ttu-id="fb43b-152">Шаг 1.</span><span class="sxs-lookup"><span data-stu-id="fb43b-152">Step 1.</span></span> <span data-ttu-id="fb43b-153">Настройка источника hello</span><span class="sxs-lookup"><span data-stu-id="fb43b-153">Configure hello source</span></span>
1. <span data-ttu-id="fb43b-154">В поле **Источник** выберите **Azure Preview**.</span><span class="sxs-lookup"><span data-stu-id="fb43b-154">In **Source**, select **Azure - PREVIEW**.</span></span>
2. <span data-ttu-id="fb43b-155">В **исходное местоположение**выберите источник hello регион Azure, где работающие виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="fb43b-155">In **Source location**, select hello source Azure region where your VMs are currently running.</span></span>
3. <span data-ttu-id="fb43b-156">Выберите hello модель развертывания виртуальных машин: **диспетчера ресурсов** или **классический**.</span><span class="sxs-lookup"><span data-stu-id="fb43b-156">Select hello deployment model of your VMs: **Resource Manager** or **Classic**.</span></span>
4. <span data-ttu-id="fb43b-157">Выберите hello **исходная группа ресурсов** для виртуальных машин диспетчера ресурсов или **облачная служба** для классических виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="fb43b-157">Select hello **Source resource group** for Resource Manager VMs or **cloud service** for classic VMs.</span></span>

    ![Настройка источника hello](./media/site-recovery-azure-to-azure/source.png)

### <a name="step-2-select-virtual-machines"></a><span data-ttu-id="fb43b-159">Шаг 2.</span><span class="sxs-lookup"><span data-stu-id="fb43b-159">Step 2.</span></span> <span data-ttu-id="fb43b-160">Выбор виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="fb43b-160">Select virtual machines</span></span>

* <span data-ttu-id="fb43b-161">Выберите виртуальные машины hello tooreplicate и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="fb43b-161">Select hello VMs you want tooreplicate, and then click **OK**.</span></span>

    ![Выбор виртуальных машин](./media/site-recovery-azure-to-azure/vms.png)

### <a name="step-3-configure-settings"></a><span data-ttu-id="fb43b-163">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="fb43b-163">Step 3.</span></span> <span data-ttu-id="fb43b-164">Настройка параметров</span><span class="sxs-lookup"><span data-stu-id="fb43b-164">Configure settings</span></span>

1. <span data-ttu-id="fb43b-165">по умолчанию hello toooverride целевые параметры и укажите параметры hello по своему усмотрению выберите **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="fb43b-165">toooverride hello default target settings and specify hello settings of your choice, click **Customize**.</span></span> <span data-ttu-id="fb43b-166">Дополнительные сведения см. в разделе [Настройка целевых ресурсов](site-recovery-replicate-azure-to-azure.md##customize-target-resources).</span><span class="sxs-lookup"><span data-stu-id="fb43b-166">For more information, see [Customize target resources](site-recovery-replicate-azure-to-azure.md##customize-target-resources).</span></span>

    ![Настройка параметров](./media/site-recovery-azure-to-azure/settings.png)


2. <span data-ttu-id="fb43b-168">По умолчанию Site Recovery создает политику репликации, которая выполняет моментальные снимки с согласованием каждые 4 часа и хранит точки восстановления 24 часа.</span><span class="sxs-lookup"><span data-stu-id="fb43b-168">By default, Site Recovery creates a replication policy that takes app-consistent snapshots every 4 hours and retains recovery points for 24 hours.</span></span> <span data-ttu-id="fb43b-169">Щелкните toocreate политики с различными параметрами **Настройка** Далее слишком**политику репликации**.</span><span class="sxs-lookup"><span data-stu-id="fb43b-169">toocreate a policy with different settings, click **Customize** next too**Replication Policy**.</span></span>

    ![Настройка политики](./media/site-recovery-azure-to-azure/customize-policy.png)

3. <span data-ttu-id="fb43b-171">Щелкните toostart подготовки hello целевые ресурсы, **создать целевые ресурсы**.</span><span class="sxs-lookup"><span data-stu-id="fb43b-171">toostart provisioning hello target resources, click **Create target resources**.</span></span> <span data-ttu-id="fb43b-172">Подготовка занимает несколько минут.</span><span class="sxs-lookup"><span data-stu-id="fb43b-172">Provisioning takes a minute or so.</span></span> <span data-ttu-id="fb43b-173">Не закрывайте колонке hello во время инициализации или требуется toostart по сравнению с.</span><span class="sxs-lookup"><span data-stu-id="fb43b-173">Don't close hello blade during provisioning, or you need toostart over.</span></span>

4. <span data-ttu-id="fb43b-174">репликация tootrigger hello виртуальной Машины, щелкните **включить репликацию**.</span><span class="sxs-lookup"><span data-stu-id="fb43b-174">tootrigger replication of hello selected VM, click **Enable replication**.</span></span>

5. <span data-ttu-id="fb43b-175">Вы можете отслеживать ход выполнения hello **включить защиту** задания в **параметры** > **заданий** > **задания восстановления сайта**.</span><span class="sxs-lookup"><span data-stu-id="fb43b-175">You can track progress of hello **Enable protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span>

6. <span data-ttu-id="fb43b-176">В **параметры** > **реплицируются элементы**, можно просмотреть состояние hello виртуальных машин и hello ход выполнения начальной репликации.</span><span class="sxs-lookup"><span data-stu-id="fb43b-176">In **Settings** > **Replicated Items**, you can view hello status of VMs and hello initial replication progress.</span></span> <span data-ttu-id="fb43b-177">Щелкните toodrill ВМ hello его параметры.</span><span class="sxs-lookup"><span data-stu-id="fb43b-177">Click hello VM toodrill down into its settings.</span></span>

## <a name="run-a-test-failover"></a><span data-ttu-id="fb43b-178">Запуск тестовой отработки отказа</span><span class="sxs-lookup"><span data-stu-id="fb43b-178">Run a test failover</span></span>

<span data-ttu-id="fb43b-179">После настройки все компоненты, выполните тест отработки отказа toomake, убедиться, что все работает должным образом:</span><span class="sxs-lookup"><span data-stu-id="fb43b-179">After you set up everything, run a test failover toomake sure everything's working as expected:</span></span>

1. <span data-ttu-id="fb43b-180">toofail на одном компьютере, в **параметры** > **реплицируются элементы**, щелкните hello ВМ **+ тестовой отработки отказа** значок.</span><span class="sxs-lookup"><span data-stu-id="fb43b-180">toofail over a single machine, in **Settings** > **Replicated Items**, click hello VM **+Test Failover** icon.</span></span>

2. <span data-ttu-id="fb43b-181">Планирование toofail через во время операции восстановления, в **параметры** > **планы восстановления**, щелкните правой кнопкой мыши план hello **тестовой отработки отказа**.</span><span class="sxs-lookup"><span data-stu-id="fb43b-181">toofail over a recovery plan, in **Settings** > **Recovery Plans**, right-click hello plan **Test Failover**.</span></span> <span data-ttu-id="fb43b-182">план восстановления toocreate [следуйте этим инструкциям](site-recovery-create-recovery-plans.md).</span><span class="sxs-lookup"><span data-stu-id="fb43b-182">toocreate a recovery plan, [follow these instructions](site-recovery-create-recovery-plans.md).</span></span> 

3. <span data-ttu-id="fb43b-183">В **тестовой отработки отказа**выберите hello целевой виртуальной сети Azure toowhich виртуальных машинах Azure подключены после hello переход на другой ресурс.</span><span class="sxs-lookup"><span data-stu-id="fb43b-183">In **Test Failover**, select hello target Azure virtual network toowhich Azure VMs are connected after hello failover occurs.</span></span>

4. <span data-ttu-id="fb43b-184">toostart Здравствуйте перехода на другой ресурс, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="fb43b-184">toostart hello failover, click **OK**.</span></span> <span data-ttu-id="fb43b-185">tootrack хода выполнения, нажмите кнопку tooopen ВМ hello его свойства.</span><span class="sxs-lookup"><span data-stu-id="fb43b-185">tootrack progress, click hello VM tooopen its properties.</span></span> <span data-ttu-id="fb43b-186">Или можно щелкнуть hello **тестовой отработки отказа** задания в hello имя хранилища > **параметры** > **заданий** > **задания Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="fb43b-186">Or you can click hello **Test Failover** job in hello vault name > **Settings** > **Jobs** > **Site Recovery jobs**.</span></span>

5. <span data-ttu-id="fb43b-187">После hello завершения перехода на другой ресурс, реплика hello Azure машины появится в hello портала Azure > **виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="fb43b-187">After hello failover finishes, hello replica Azure machine appears in hello Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="fb43b-188">Убедитесь, что этот hello виртуальной Машины — hello соответствующего размера, он подключенный toohello соответствующий сетевой и что он работает.</span><span class="sxs-lookup"><span data-stu-id="fb43b-188">Make sure that hello VM is hello appropriate size, that it's connected toohello appropriate network, and that it's running.</span></span>

6. <span data-ttu-id="fb43b-189">Щелкните toodelete hello виртуальных машин, которые были созданы во время тестовой отработки отказа hello **очистку тестовой отработки отказа** на hello репликация плана восстановления hello или элемента.</span><span class="sxs-lookup"><span data-stu-id="fb43b-189">toodelete hello VMs that were created during hello test failover, click **Cleanup test failover** on hello replicated item or hello recovery plan.</span></span> <span data-ttu-id="fb43b-190">В **заметки**, записать и сохранить все наблюдения, связанные с тестовой отработки отказа hello.</span><span class="sxs-lookup"><span data-stu-id="fb43b-190">In **Notes**, record and save any observations associated with hello test failover.</span></span> 

<span data-ttu-id="fb43b-191">[Узнайте больше](site-recovery-test-failover-to-azure.md) о выполнении тестовой отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="fb43b-191">[Learn more](site-recovery-test-failover-to-azure.md) about test failovers.</span></span>


## <a name="next-steps"></a><span data-ttu-id="fb43b-192">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fb43b-192">Next steps</span></span>

<span data-ttu-id="fb43b-193">По окончании теста hello развертывания:</span><span class="sxs-lookup"><span data-stu-id="fb43b-193">After you test hello deployment:</span></span>

- <span data-ttu-id="fb43b-194">[Дополнительные сведения](site-recovery-failover.md) о различных типов отработки отказа и каким образом toorun их.</span><span class="sxs-lookup"><span data-stu-id="fb43b-194">[Learn more](site-recovery-failover.md) about different types of failovers and how toorun them.</span></span>
- <span data-ttu-id="fb43b-195">Дополнительные сведения о [с использованием планов восстановления](site-recovery-create-recovery-plans.md) tooreduce RTO.</span><span class="sxs-lookup"><span data-stu-id="fb43b-195">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) tooreduce RTO.</span></span>
