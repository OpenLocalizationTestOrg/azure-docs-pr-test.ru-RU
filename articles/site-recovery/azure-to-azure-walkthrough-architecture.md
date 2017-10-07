---
title: "Архитектура hello aaaReview для репликации виртуальных машин Azure между регионами Azure | Документы Microsoft"
description: "Это статье представлен обзор компонентов и архитектура, используемая при репликации между регионами Azure, с помощью службы Azure Site Recovery hello виртуальных машинах Azure."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/12/2017
ms.author: raynew
ms.openlocfilehash: 4caab4e7a764040f317201d1345c40c73f836d81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-azure-vm-replication-between-azure-regions"></a><span data-ttu-id="313ba-103">Шаг 1: Обзор архитектуры hello для репликации виртуальной Машины Azure между регионами Azure</span><span class="sxs-lookup"><span data-stu-id="313ba-103">Step 1: Review hello architecture for Azure VM replication between Azure regions</span></span>


<span data-ttu-id="313ba-104">После просмотра hello [действия Обзор](azure-to-azure-walkthrough-overview.md) чтение этой статьи toounderstand hello компоненты и процессы, которые используются при репликации и восстановление виртуальных машин (ВМ) Azure с tooanother один регион Azure, используя для этого развертывания [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="313ba-104">After reviewing hello [overview steps](azure-to-azure-walkthrough-overview.md) for this deployment, read this article toounderstand hello components and processes used when replicating and recovering Azure virtual machines (VMs) from one Azure region tooanother, using [Azure Site Recovery](site-recovery-overview.md).</span></span>

- <span data-ttu-id="313ba-105">Завершив статьи hello, должны иметь четко понимать, как работает область tooanother репликации виртуальной Машины Azure.</span><span class="sxs-lookup"><span data-stu-id="313ba-105">When you finish hello article, you should have a clear understanding of how Azure VM replication tooanother region works.</span></span>
- <span data-ttu-id="313ba-106">Отправлять все комментарии hello нижней части этой статьи, или задать вопросы в hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="313ba-106">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

>[!NOTE]
><span data-ttu-id="313ba-107">Репликация виртуальной Машины Azure с hello службы Site Recovery в настоящее время находится в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="313ba-107">Azure VM replication with hello Site Recovery service is currently in preview.</span></span>



## <a name="architectural-components"></a><span data-ttu-id="313ba-108">Компоненты архитектуры</span><span class="sxs-lookup"><span data-stu-id="313ba-108">Architectural components</span></span>

<span data-ttu-id="313ba-109">Следующая схема Hello показано высокоуровневое представление среды виртуальных Машин Azure в определенном регионе (в этом примере hello расположение Восток США).</span><span class="sxs-lookup"><span data-stu-id="313ba-109">hello following diagram provides a high-level view of an Azure VM environment in a specific region (in this example, hello East US location).</span></span> <span data-ttu-id="313ba-110">В среде виртуальных машин Azure:</span><span class="sxs-lookup"><span data-stu-id="313ba-110">In an Azure VM environment:</span></span>
- <span data-ttu-id="313ba-111">Приложения могут работать на виртуальных машинах с дисками, распределенными между учетными записями хранения.</span><span class="sxs-lookup"><span data-stu-id="313ba-111">Apps can be running on VMs with disks spread across storage accounts.</span></span>
- <span data-ttu-id="313ba-112">Hello виртуальные машины могут быть включены в одну или несколько подсетей в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="313ba-112">hello VMs can be included in one or more subnets within a virtual network.</span></span>

![customer-environment](./media/azure-to-azure-walkthrough-architecture/source-environment.png)

## <a name="replication-process"></a><span data-ttu-id="313ba-114">Процесс репликации</span><span class="sxs-lookup"><span data-stu-id="313ba-114">Replication process</span></span>

### <a name="step-1"></a><span data-ttu-id="313ba-115">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="313ba-115">Step 1</span></span>

<span data-ttu-id="313ba-116">При включении репликации виртуальной Машины Azure в hello портал Azure hello ресурсов, перечисленных в следующих hello, что схема и таблица, будут автоматически созданы в целевой области hello.</span><span class="sxs-lookup"><span data-stu-id="313ba-116">When you enable Azure VM replication in hello Azure portal, hello resources shown in hello following diagram and table are automatically created in hello target region.</span></span> <span data-ttu-id="313ba-117">По умолчанию ресурсы создаются на основе настроек исходного региона.</span><span class="sxs-lookup"><span data-stu-id="313ba-117">By default, resources are created based on source region settings.</span></span> <span data-ttu-id="313ba-118">Можно настроить параметры целевой hello по необходимости.</span><span class="sxs-lookup"><span data-stu-id="313ba-118">You can customize hello target settings as required.</span></span> <span data-ttu-id="313ba-119">[Подробнее](site-recovery-replicate-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="313ba-119">[Learn more](site-recovery-replicate-azure-to-azure.md).</span></span>

![Включение процесса репликации, шаг 1](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-1.png)

<span data-ttu-id="313ba-121">**Ресурс**</span><span class="sxs-lookup"><span data-stu-id="313ba-121">**Resource**</span></span> | <span data-ttu-id="313ba-122">**Дополнительные сведения**</span><span class="sxs-lookup"><span data-stu-id="313ba-122">**Details**</span></span>
--- | ---
<span data-ttu-id="313ba-123">**Целевая группа ресурсов**</span><span class="sxs-lookup"><span data-stu-id="313ba-123">**Target resource group**</span></span> | <span data-ttu-id="313ba-124">Здравствуйте, toowhich группы ресурсов, принадлежащих реплицированных виртуальных машин после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="313ba-124">hello resource group toowhich replicated VMs belong after failover.</span></span>
<span data-ttu-id="313ba-125">**Целевая виртуальная сеть**</span><span class="sxs-lookup"><span data-stu-id="313ba-125">**Target virtual network**</span></span> | <span data-ttu-id="313ba-126">Hello виртуальной сети, в котором реплицированные виртуальные машины находятся после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="313ba-126">hello virtual network in which replicated VMs are located after failover.</span></span> <span data-ttu-id="313ba-127">Сетевое сопоставление создается между исходными и целевыми виртуальными сетями и наоборот.</span><span class="sxs-lookup"><span data-stu-id="313ba-127">A network mapping is created between source and target virtual networks, and vice versa.</span></span>
<span data-ttu-id="313ba-128">**Учетная запись хранения**</span><span class="sxs-lookup"><span data-stu-id="313ba-128">**Cache storage accounts**</span></span> | <span data-ttu-id="313ba-129">Прежде чем изменения в источнике, виртуальные машины реплицированы toohello целевой учетной записи хранения, отслеживаются и отправляются toohello учетной записи хранилища кэша в целевом расположении hello.</span><span class="sxs-lookup"><span data-stu-id="313ba-129">Before changes on source VMs are replicated toohello target storage account, they are tracked and sent toohello cache storage account in hello target location.</span></span> <span data-ttu-id="313ba-130">Это обеспечивает минимальное воздействие на производственных приложений, выполняющихся в hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="313ba-130">This ensures minimal impact on production apps running on hello VM.</span></span>
<span data-ttu-id="313ba-131">**Целевые учетные записи хранения**</span><span class="sxs-lookup"><span data-stu-id="313ba-131">**Target storage accounts**</span></span>  | <span data-ttu-id="313ba-132">Учетные записи хранения в hello целевые расположения toowhich hello данные реплицируются.</span><span class="sxs-lookup"><span data-stu-id="313ba-132">Storage accounts in hello target location toowhich hello data is replicated.</span></span>
<span data-ttu-id="313ba-133">**Целевая группа доступности**</span><span class="sxs-lookup"><span data-stu-id="313ba-133">**Target availability sets**</span></span>  | <span data-ttu-id="313ba-134">В какой hello реплицированных виртуальных машин находятся после отработки отказа группы доступности.</span><span class="sxs-lookup"><span data-stu-id="313ba-134">Availability sets in which hello replicated VMs are located after failover.</span></span>

### <a name="step-2"></a><span data-ttu-id="313ba-135">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="313ba-135">Step 2</span></span>

<span data-ttu-id="313ba-136">Как репликация включена, hello расширения Site Recovery Mobility службы автоматически устанавливается на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="313ba-136">As replication is enabled, hello Site Recovery extension Mobility service is automatically installed on hello VM.</span></span> <span data-ttu-id="313ba-137">происходит Hello следующее:</span><span class="sxs-lookup"><span data-stu-id="313ba-137">hello following occurs:</span></span>

1. <span data-ttu-id="313ba-138">Hello ВМ регистрируется с Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="313ba-138">hello VM is registered with Site Recovery.</span></span>

2. <span data-ttu-id="313ba-139">Непрерывная репликация настроена для hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="313ba-139">Continuous replication is configured for hello VM.</span></span> <span data-ttu-id="313ba-140">Записывает данные на hello ВМ диски, постоянно передаются toohello учетной записи хранилища кэша в исходное расположение hello.</span><span class="sxs-lookup"><span data-stu-id="313ba-140">Data writes on hello VM disks are continuously transferred toohello cache storage account in hello source location.</span></span>

   ![Включение процесса репликации, шаг 2](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-2.png)

  
  <span data-ttu-id="313ba-142">Обратите внимание, что Site Recovery никогда не должна входящих toohello подключения к виртуальной Машине.</span><span class="sxs-lookup"><span data-stu-id="313ba-142">Note that Site Recovery never needs inbound connectivity toohello VM.</span></span> <span data-ttu-id="313ba-143">Только исходящие подключения к службе восстановления tooSite URL-адреса и IP-адресов, проверки подлинности Office 365 URL-адреса и IP-адресов и необходимости кэша хранилища учетной записи IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="313ba-143">Only outbound connectivity tooSite Recovery service URLs/IP addresses, Office 365 authentication URLs/IP addresses, and cache storage account IP addresses is needed.</span></span> 

## <a name="continuous-replication-process"></a><span data-ttu-id="313ba-144">Процесс непрерывной репликации</span><span class="sxs-lookup"><span data-stu-id="313ba-144">Continuous replication process</span></span>

<span data-ttu-id="313ba-145">После работы с непрерывной репликацией диск, который производит запись немедленно являются передать toohello учетной записи хранилища кэша.</span><span class="sxs-lookup"><span data-stu-id="313ba-145">After continuous replication is working, disk writes are immediately transferred toohello cache storage account.</span></span> <span data-ttu-id="313ba-146">Site Recovery обрабатывает данные hello и отправляет его toohello целевой учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="313ba-146">Site Recovery processes hello data and sends it toohello target storage account.</span></span> <span data-ttu-id="313ba-147">После обработки данных hello точки восстановления создаются в целевой учетной записи хранения hello каждые несколько минут.</span><span class="sxs-lookup"><span data-stu-id="313ba-147">After hello data is processed, recovery points are generated in hello target storage account every few minutes.</span></span>

## <a name="failover-process"></a><span data-ttu-id="313ba-148">Процесс отработки отказа</span><span class="sxs-lookup"><span data-stu-id="313ba-148">Failover process</span></span>

<span data-ttu-id="313ba-149">При запуске отработки отказа виртуальные машины создаются в hello целевой группы ресурсов, целевой виртуальной сети, целевой подсети hello и hello доступности набор целей.</span><span class="sxs-lookup"><span data-stu-id="313ba-149">When you initiate a failover, hello VMs are created in hello target resource group, target virtual network, target subnet, and hello target availability set.</span></span> <span data-ttu-id="313ba-150">Во время отработки отказа можно использовать любую точку восстановления.</span><span class="sxs-lookup"><span data-stu-id="313ba-150">During a failover, you can use any recovery point.</span></span>

![Процесс отработки отказа](./media/azure-to-azure-walkthrough-architecture/failover.png)

## <a name="next-steps"></a><span data-ttu-id="313ba-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="313ba-152">Next steps</span></span>

<span data-ttu-id="313ba-153">Go слишком[шаг 2: Проверьте предварительные условия и ограничения](azure-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="313ba-153">Go too[Step 2: Verify prerequisites and limitations](azure-to-azure-walkthrough-prerequisites.md)</span></span>
