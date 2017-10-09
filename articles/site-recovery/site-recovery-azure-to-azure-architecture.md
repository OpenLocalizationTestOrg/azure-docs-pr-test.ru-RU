---
title: "aaaHow ли репликация виртуальной машины Azure между рабочих областей Azure в Azure Site Recovery?  | Документация Майкрософт"
description: "Это статье представлен обзор компонентов и архитектура, используемая при репликации между регионами Azure с помощью службы Azure Site Recovery hello виртуальных машинах Azure."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/29/2017
ms.author: sujayt
ms.openlocfilehash: 01eda83e490821f8afc8a2973c18a19453a2e84a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-vm-replication-work-in-site-recovery"></a><span data-ttu-id="f8e10-104">Как работает репликация виртуальной машины в Site Recovery?</span><span class="sxs-lookup"><span data-stu-id="f8e10-104">How does Azure VM replication work in Site Recovery?</span></span>


<span data-ttu-id="f8e10-105">В этой статье описываются hello компоненты и процессы, задействованные в репликации и восстановление виртуальных машин (ВМ) Azure из одного региона tooanother с помощью hello [Azure Site Recovery](site-recovery-overview.md) службы.</span><span class="sxs-lookup"><span data-stu-id="f8e10-105">This article describes hello components and processes involved in replicating and recovering Azure virtual machines (VMs) from one region tooanother by using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

>[!NOTE]
><span data-ttu-id="f8e10-106">Репликация виртуальной Машины Azure с hello службы Site Recovery в настоящее время находится в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="f8e10-106">Azure VM replication with hello Site Recovery service is currently in preview.</span></span>

<span data-ttu-id="f8e10-107">Отправлять все комментарии hello нижней части этой статьи, или задать вопросы в hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="f8e10-107">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="architectural-components"></a><span data-ttu-id="f8e10-108">Компоненты архитектуры</span><span class="sxs-lookup"><span data-stu-id="f8e10-108">Architectural components</span></span>

<span data-ttu-id="f8e10-109">Следующая схема Hello показано высокоуровневое представление среды виртуальных Машин Azure в определенном регионе (в этом примере hello расположение Восток США).</span><span class="sxs-lookup"><span data-stu-id="f8e10-109">hello following diagram provides a high-level view of an Azure VM environment in a specific region (in this example, hello East US location).</span></span> <span data-ttu-id="f8e10-110">В среде виртуальных машин Azure:</span><span class="sxs-lookup"><span data-stu-id="f8e10-110">In an Azure VM environment:</span></span>
- <span data-ttu-id="f8e10-111">Приложения могут работать на виртуальных машинах с дисками, распределенными между учетными записями хранения.</span><span class="sxs-lookup"><span data-stu-id="f8e10-111">Apps can be running on VMs with disks spread across storage accounts.</span></span>
- <span data-ttu-id="f8e10-112">Hello виртуальные машины могут быть включены в одну или несколько подсетей в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="f8e10-112">hello VMs can be included in one or more subnets within a virtual network.</span></span>

![customer-environment](./media/site-recovery-azure-to-azure-architecture/source-environment.png)

<span data-ttu-id="f8e10-114">Дополнительные сведения о hello необходимые условия для развертывания и требований в hello [Матрица поддержки](site-recovery-support-matrix-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="f8e10-114">Learn about hello deployment prerequisites and requirements in hello [support matrix](site-recovery-support-matrix-azure-to-azure.md).</span></span>

## <a name="replication-process"></a><span data-ttu-id="f8e10-115">Процесс репликации</span><span class="sxs-lookup"><span data-stu-id="f8e10-115">Replication process</span></span>

### <a name="step-1"></a><span data-ttu-id="f8e10-116">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="f8e10-116">Step 1</span></span>

<span data-ttu-id="f8e10-117">При включении репликации виртуальной Машины Azure в hello портал Azure hello ресурсов, перечисленных в следующих hello, что схема и таблица, будут автоматически созданы в целевой области hello.</span><span class="sxs-lookup"><span data-stu-id="f8e10-117">When you enable Azure VM replication in hello Azure portal, hello resources shown in hello following diagram and table are automatically created in hello target region.</span></span> <span data-ttu-id="f8e10-118">По умолчанию ресурсы создаются на основе настроек исходного региона.</span><span class="sxs-lookup"><span data-stu-id="f8e10-118">By default, resources are created based on source region settings.</span></span> <span data-ttu-id="f8e10-119">Можно настроить параметры целевой hello по необходимости.</span><span class="sxs-lookup"><span data-stu-id="f8e10-119">You can customize hello target settings as required.</span></span> <span data-ttu-id="f8e10-120">[Подробнее](site-recovery-replicate-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="f8e10-120">[Learn more](site-recovery-replicate-azure-to-azure.md).</span></span>

![Включение процесса репликации, шаг 1](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-1.png)

<span data-ttu-id="f8e10-122">**Ресурс**</span><span class="sxs-lookup"><span data-stu-id="f8e10-122">**Resource**</span></span> | <span data-ttu-id="f8e10-123">**Дополнительные сведения**</span><span class="sxs-lookup"><span data-stu-id="f8e10-123">**Details**</span></span>
--- | ---
<span data-ttu-id="f8e10-124">**Целевая группа ресурсов**</span><span class="sxs-lookup"><span data-stu-id="f8e10-124">**Target resource group**</span></span> | <span data-ttu-id="f8e10-125">Здравствуйте, toowhich группы ресурсов, принадлежащих реплицированных виртуальных машин после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="f8e10-125">hello resource group toowhich replicated VMs belong after failover.</span></span>
<span data-ttu-id="f8e10-126">**Целевая виртуальная сеть**</span><span class="sxs-lookup"><span data-stu-id="f8e10-126">**Target virtual network**</span></span> | <span data-ttu-id="f8e10-127">Hello виртуальной сети, в котором реплицированные виртуальные машины находятся после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="f8e10-127">hello virtual network in which replicated VMs are located after failover.</span></span> <span data-ttu-id="f8e10-128">Сетевое сопоставление создается между исходными и целевыми виртуальными сетями и наоборот.</span><span class="sxs-lookup"><span data-stu-id="f8e10-128">A network mapping is created between source and target virtual networks, and vice versa.</span></span>
<span data-ttu-id="f8e10-129">**Учетная запись хранения**</span><span class="sxs-lookup"><span data-stu-id="f8e10-129">**Cache storage accounts**</span></span> | <span data-ttu-id="f8e10-130">Прежде чем изменения в источнике, виртуальные машины реплицированы toohello целевой учетной записи хранения, отслеживаются и отправляются toohello учетной записи хранилища кэша в целевом расположении hello.</span><span class="sxs-lookup"><span data-stu-id="f8e10-130">Before changes on source VMs are replicated toohello target storage account, they are tracked and sent toohello cache storage account in hello target location.</span></span> <span data-ttu-id="f8e10-131">Это обеспечивает минимальное воздействие на производственных приложений, выполняющихся в hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="f8e10-131">This ensures minimal impact on production apps running on hello VM.</span></span>
<span data-ttu-id="f8e10-132">**Целевые учетные записи хранения**</span><span class="sxs-lookup"><span data-stu-id="f8e10-132">**Target storage accounts**</span></span>  | <span data-ttu-id="f8e10-133">Учетные записи хранения в hello целевые расположения toowhich hello данные реплицируются.</span><span class="sxs-lookup"><span data-stu-id="f8e10-133">Storage accounts in hello target location toowhich hello data is replicated.</span></span>
<span data-ttu-id="f8e10-134">**Целевая группа доступности**</span><span class="sxs-lookup"><span data-stu-id="f8e10-134">**Target availability sets**</span></span>  | <span data-ttu-id="f8e10-135">В какой hello реплицированных виртуальных машин находятся после отработки отказа группы доступности.</span><span class="sxs-lookup"><span data-stu-id="f8e10-135">Availability sets in which hello replicated VMs are located after failover.</span></span>

### <a name="step-2"></a><span data-ttu-id="f8e10-136">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="f8e10-136">Step 2</span></span>

<span data-ttu-id="f8e10-137">Как репликация включена, hello расширения Site Recovery Mobility службы автоматически устанавливается на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="f8e10-137">As replication is enabled, hello Site Recovery extension Mobility service is automatically installed on hello VM.</span></span> <span data-ttu-id="f8e10-138">происходит Hello следующее:</span><span class="sxs-lookup"><span data-stu-id="f8e10-138">hello following occurs:</span></span>

1. <span data-ttu-id="f8e10-139">Hello ВМ регистрируется с Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="f8e10-139">hello VM is registered with Site Recovery.</span></span>

2. <span data-ttu-id="f8e10-140">Непрерывная репликация настроена для hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="f8e10-140">Continuous replication is configured for hello VM.</span></span> <span data-ttu-id="f8e10-141">Записывает данные на hello ВМ диски, постоянно передаются toohello учетной записи хранилища кэша в исходное расположение hello.</span><span class="sxs-lookup"><span data-stu-id="f8e10-141">Data writes on hello VM disks are continuously transferred toohello cache storage account in hello source location.</span></span>

   ![Включение процесса репликации, шаг 2](./media/site-recovery-azure-to-azure-architecture/enable-replication-step-2.png)

   >[!IMPORTANT]
   > <span data-ttu-id="f8e10-143">Site Recovery никогда не должна toohello входящие подключения к виртуальной Машине.</span><span class="sxs-lookup"><span data-stu-id="f8e10-143">Site Recovery never needs inbound connectivity toohello VM.</span></span> <span data-ttu-id="f8e10-144">Hello виртуальной Машины должен только исходящие подключения tooSite восстановления URL-адреса и IP-адресов службы Office 365 authentication URL-адреса или IP-адреса и кэша хранилища учетной записи IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="f8e10-144">hello VM needs only outbound connectivity tooSite Recovery service URLs/IP addresses, Office 365 authentication URLs/IP addresses, and cache storage account IP addresses.</span></span> <span data-ttu-id="f8e10-145">Дополнительные сведения см. в разделе hello [руководство по сетям для репликации виртуальных машин Azure](site-recovery-azure-to-azure-networking-guidance.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="f8e10-145">For more information, see hello [Networking guidance for replicating Azure virtual machines](site-recovery-azure-to-azure-networking-guidance.md) article.</span></span>

## <a name="continuous-replication-process"></a><span data-ttu-id="f8e10-146">Процесс непрерывной репликации</span><span class="sxs-lookup"><span data-stu-id="f8e10-146">Continuous replication process</span></span>

<span data-ttu-id="f8e10-147">После работы с непрерывной репликацией диск, который производит запись немедленно являются передать toohello учетной записи хранилища кэша.</span><span class="sxs-lookup"><span data-stu-id="f8e10-147">After continuous replication is working, disk writes are immediately transferred toohello cache storage account.</span></span> <span data-ttu-id="f8e10-148">Site Recovery обрабатывает данные hello и отправляет его toohello целевой учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="f8e10-148">Site Recovery processes hello data and sends it toohello target storage account.</span></span> <span data-ttu-id="f8e10-149">После обработки данных hello точки восстановления создаются в целевой учетной записи хранения hello каждые несколько минут.</span><span class="sxs-lookup"><span data-stu-id="f8e10-149">After hello data is processed, recovery points are generated in hello target storage account every few minutes.</span></span>

## <a name="failover-process"></a><span data-ttu-id="f8e10-150">Процесс отработки отказа</span><span class="sxs-lookup"><span data-stu-id="f8e10-150">Failover process</span></span>

<span data-ttu-id="f8e10-151">При запуске отработки отказа виртуальные машины создаются в hello целевой группы ресурсов, целевой виртуальной сети, целевой подсети hello и hello доступности набор целей.</span><span class="sxs-lookup"><span data-stu-id="f8e10-151">When you initiate a failover, hello VMs are created in hello target resource group, target virtual network, target subnet, and hello target availability set.</span></span> <span data-ttu-id="f8e10-152">Во время отработки отказа можно использовать любую точку восстановления.</span><span class="sxs-lookup"><span data-stu-id="f8e10-152">During a failover, you can use any recovery point.</span></span>

![Процесс отработки отказа](./media/site-recovery-azure-to-azure-architecture/failover.png)

## <a name="next-steps"></a><span data-ttu-id="f8e10-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f8e10-154">Next steps</span></span>

- <span data-ttu-id="f8e10-155">Дополнительные сведения о [сети](site-recovery-azure-to-azure-networking-guidance.md) для репликации виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="f8e10-155">Learn about [networking](site-recovery-azure-to-azure-networking-guidance.md) for Azure VM replication.</span></span>
- <span data-ttu-id="f8e10-156">Выполните пошаговое руководство слишком[реплицировать виртуальные машины Azure.](site-recovery-azure-to-azure.md)</span><span class="sxs-lookup"><span data-stu-id="f8e10-156">Follow a walkthrough too[replicate Azure VMs.](site-recovery-azure-to-azure.md)</span></span>
