---
title: "Архитектура hello aaaReview для Hyper-V репликации tooa вторичного сайта с помощью Azure Site Recovery | Документы Microsoft"
description: "Также приводятся сведения об архитектуре hello по репликации локальных виртуальных машин Hyper-V tooa вторичного System Center VMM сайта с помощью Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 07099161-4cc7-4f32-8eb9-2a71bbf0750b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 0de4b4e8601116c73e6fd710597ce4e561884368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-hyper-v-replication-tooa-secondary-site"></a><span data-ttu-id="189eb-103">Шаг 1: Проверка hello архитектуры для Hyper-V репликации tooa вторичного сайта</span><span class="sxs-lookup"><span data-stu-id="189eb-103">Step 1: Review hello architecture for Hyper-V replication tooa secondary site</span></span>

<span data-ttu-id="189eb-104">В этой статье описывается hello компонентов и процессов, задействованных при репликации локальных виртуальных машин Hyper-V (ВМ) в облаках диспетчера виртуальных машин System Center (VMM), tooa с помощью hello вторичный сайт VMM [Azure Site Recovery](site-recovery-overview.md)в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="189eb-104">This article describes hello components and processes involved when replicating on-premises Hyper-V virtual machines (VMs) in System Center Virtual Machine Manager (VMM) clouds, tooa secondary VMM site using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="189eb-105">Отправлять все комментарии hello нижней части этой статьи, или в hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="189eb-105">Post any comments at hello bottom of this article, or in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="architectural-components"></a><span data-ttu-id="189eb-106">Компоненты архитектуры</span><span class="sxs-lookup"><span data-stu-id="189eb-106">Architectural components</span></span>

<span data-ttu-id="189eb-107">Вот, что необходимо для репликации виртуальных машин Hyper-V tooa вторичный сайт VMM.</span><span class="sxs-lookup"><span data-stu-id="189eb-107">Here's what you need for replicating Hyper-V VMs tooa secondary VMM site.</span></span>

<span data-ttu-id="189eb-108">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="189eb-108">**Component**</span></span> | <span data-ttu-id="189eb-109">**Расположение**</span><span class="sxs-lookup"><span data-stu-id="189eb-109">**Location**</span></span> | <span data-ttu-id="189eb-110">**Дополнительные сведения**</span><span class="sxs-lookup"><span data-stu-id="189eb-110">**Details**</span></span>
--- | --- | ---
<span data-ttu-id="189eb-111">**Таблицы Azure**</span><span class="sxs-lookup"><span data-stu-id="189eb-111">**Azure**</span></span> | <span data-ttu-id="189eb-112">Подписка в Azure.</span><span class="sxs-lookup"><span data-stu-id="189eb-112">Subscription in Azure.</span></span> | <span data-ttu-id="189eb-113">Создать хранилище служб восстановления в hello подписки Azure tooorchestrate и управление репликацией между расположениями VMM.</span><span class="sxs-lookup"><span data-stu-id="189eb-113">You create a Recovery Services vault in hello Azure subscription, tooorchestrate and manage replication between VMM locations.</span></span>
<span data-ttu-id="189eb-114">**Сервер VMM**</span><span class="sxs-lookup"><span data-stu-id="189eb-114">**VMM server**</span></span> | <span data-ttu-id="189eb-115">Необходимо иметь основное и дополнительное расположение VMM.</span><span class="sxs-lookup"><span data-stu-id="189eb-115">You need a VMM primary and secondary location.</span></span> | <span data-ttu-id="189eb-116">Мы рекомендуем сервера VMM в первичном сайте hello и по одному в hello вторичного сайта</span><span class="sxs-lookup"><span data-stu-id="189eb-116">We recommend a VMM server in hello primary site, and one in hello secondary site</span></span> 
<span data-ttu-id="189eb-117">**Сервер Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="189eb-117">**Hyper-V server**</span></span> |  <span data-ttu-id="189eb-118">Один или несколько Hyper-V серверы на hello Первичное и вторичное облака VMM.</span><span class="sxs-lookup"><span data-stu-id="189eb-118">One or more Hyper-V host servers in hello primary and secondary VMM clouds.</span></span> | <span data-ttu-id="189eb-119">Данные реплицируются между hello первичных и вторичных серверах Hyper-V узла по локальной сети hello или VPN с использованием проверки подлинности Kerberos или сертификат.</span><span class="sxs-lookup"><span data-stu-id="189eb-119">Data is replicated between hello primary and secondary Hyper-V host servers over hello LAN or VPN, using Kerberos or certificate authentication.</span></span>  
<span data-ttu-id="189eb-120">**Виртуальные машины Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="189eb-120">**Hyper-V VMs**</span></span> | <span data-ttu-id="189eb-121">Расположены на сервере узла Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="189eb-121">On Hyper-V host server.</span></span> | <span data-ttu-id="189eb-122">сервер узла Hello источник должен иметь минимум одну виртуальную Машину, что требуется tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="189eb-122">hello source host server should have at least one VM that you want tooreplicate.</span></span>

## <a name="replication-process"></a><span data-ttu-id="189eb-123">Процесс репликации</span><span class="sxs-lookup"><span data-stu-id="189eb-123">Replication process</span></span>

1. <span data-ttu-id="189eb-124">Настройка hello учетная запись Azure, создайте хранилище служб восстановления и укажите, какие действия tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="189eb-124">You set up hello Azure account, create a Recovery Services vault, and specify what you want tooreplicate.</span></span>
2. <span data-ttu-id="189eb-125">Можно настроить hello исходной и целевой настройки репликации, включая установки hello поставщика Azure Site Recovery на серверы VMM и агента служб восстановления Microsoft Azure hello на каждом узле Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="189eb-125">You configure hello source and target replication settings, which includes installing hello Azure Site Recovery Provider on VMM servers, and hello Microsoft Azure Recovery Services agent on each Hyper-V host.</span></span>
3. <span data-ttu-id="189eb-126">Можно создать политику репликации для источника hello облака VMM.</span><span class="sxs-lookup"><span data-stu-id="189eb-126">You create a replication policy for hello source VMM cloud.</span></span> <span data-ttu-id="189eb-127">политика Hello — примененных tooall виртуальными машинами, размещенными на узлах в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="189eb-127">hello policy is applied tooall VMs located on hosts in hello cloud.</span></span>
4. <span data-ttu-id="189eb-128">Включить репликацию для каждой VMM и начальная репликация виртуальной машины выполняется в соответствии с выбранных настроек hello.</span><span class="sxs-lookup"><span data-stu-id="189eb-128">You enable replication for each VMM, and initial replication of a VM occurs in accordance with hello settings you choose.</span></span>
5. <span data-ttu-id="189eb-129">После начальной репликации начинается репликация разностных изменений.</span><span class="sxs-lookup"><span data-stu-id="189eb-129">After initial replication, replication of delta changes begins.</span></span> <span data-ttu-id="189eb-130">Отслеживаемые изменения для элемента хранятся в HRL-файле.</span><span class="sxs-lookup"><span data-stu-id="189eb-130">Tracked changes for an item are held in a .hrl file.</span></span>


![Локальный tooon в локальной среде](./media/vmm-to-vmm-walkthrough-architecture/arch-onprem-onprem.png)

## <a name="failover-and-failback-process"></a><span data-ttu-id="189eb-132">Процесс отработки отказа и восстановления размещения</span><span class="sxs-lookup"><span data-stu-id="189eb-132">Failover and failback process</span></span>

1. <span data-ttu-id="189eb-133">Вы можете запустить плановую или внеплановую [отработку отказа](site-recovery-failover.md) между локальными сайтами.</span><span class="sxs-lookup"><span data-stu-id="189eb-133">You can run a planned or unplanned [failover](site-recovery-failover.md) between on-premises sites.</span></span> <span data-ttu-id="189eb-134">Если запустить плановую отработку отказа, то источник виртуальных машин, завершают работу tooensure без потери данных.</span><span class="sxs-lookup"><span data-stu-id="189eb-134">If you run a planned failover, then source VMs are shut down tooensure no data loss.</span></span>
2. <span data-ttu-id="189eb-135">При сбое одного компьютера или создайте [планы восстановления](site-recovery-create-recovery-plans.md) tooorchestrate отработки отказа нескольких машин.</span><span class="sxs-lookup"><span data-stu-id="189eb-135">You can fail over a single machine, or create [recovery plans](site-recovery-create-recovery-plans.md) tooorchestrate failover of multiple machines.</span></span>
4. <span data-ttu-id="189eb-136">При выполнении внеплановой отработки отказа tooa вторичного сайта после hello отработка отказа машин в дополнительное расположение hello не включена для защиты или репликации.</span><span class="sxs-lookup"><span data-stu-id="189eb-136">If you perform an unplanned failover tooa secondary site, after hello failover machines in hello secondary location aren't enabled for protection or replication.</span></span> <span data-ttu-id="189eb-137">Если вы запустили плановой отработки отказа, после отработки отказа hello, защищенных машин в дополнительное расположение hello.</span><span class="sxs-lookup"><span data-stu-id="189eb-137">If you ran a planned failover, after hello failover, machines in hello secondary location are protected.</span></span>
5. <span data-ttu-id="189eb-138">Затем доступ к нагрузки hello hello отработки отказа toostart фиксации из hello реплики виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="189eb-138">Then, you commit hello failover toostart accessing hello workload from hello replica VM.</span></span>
6. <span data-ttu-id="189eb-139">Когда на первичном сайте снова станет доступной, необходимо инициировать tooreplicate обратная репликация из первичного toohello вторичного сайта hello.</span><span class="sxs-lookup"><span data-stu-id="189eb-139">When your primary site is available again, you initiate reverse replication tooreplicate from hello secondary site toohello primary.</span></span> <span data-ttu-id="189eb-140">Обратная репликация приводит hello виртуальных машин в защищенное состояние, но hello вторичный центр обработки данных по-прежнему активное расположение hello.</span><span class="sxs-lookup"><span data-stu-id="189eb-140">Reverse replication brings hello virtual machines into a protected state, but hello secondary datacenter is still hello active location.</span></span>
7. <span data-ttu-id="189eb-141">toomake hello первичного сайта в активное расположение hello, инициируется плановую отработку отказа из вторичного tooprimary, следуют другой обратной репликации.</span><span class="sxs-lookup"><span data-stu-id="189eb-141">toomake hello primary site into hello active location again, you initiate a planned failover from secondary tooprimary, followed by another reverse replication.</span></span>



## <a name="next-steps"></a><span data-ttu-id="189eb-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="189eb-142">Next steps</span></span>

<span data-ttu-id="189eb-143">Go слишком[шаг 2: просмотрите hello предварительные условия и ограничения](vmm-to-vmm-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="189eb-143">Go too[Step 2: Review hello prerequisites and limitations](vmm-to-vmm-walkthrough-prerequisites.md).</span></span>
