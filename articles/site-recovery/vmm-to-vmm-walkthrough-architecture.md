---
title: "Просмотр архитектуры для репликации Hyper-V на дополнительный сайт с использованием Azure Site Recovery | Документация Майкрософт"
description: "В этой статье представлен обзор архитектуры для репликации локальных виртуальных машин Hyper-V на дополнительный сайт System Center VMM с помощью Azure Site Recovery."
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
ms.openlocfilehash: b78cd0d5a5395873afaddc8856004775f447e8ea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="step-1-review-the-architecture-for-hyper-v-replication-to-a-secondary-site"></a><span data-ttu-id="bb273-103">Шаг 1. Обзор архитектуры для репликации Hyper-V на дополнительный сайт</span><span class="sxs-lookup"><span data-stu-id="bb273-103">Step 1: Review the architecture for Hyper-V replication to a secondary site</span></span>

<span data-ttu-id="bb273-104">В этой статье описываются компоненты и процессы, задействованные при репликации локальных виртуальных машин Hyper-V в облаках System Center Virtual Machine Manager (VMM) на дополнительный сайт VMM с помощью службы [Azure Site Recovery](site-recovery-overview.md) на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="bb273-104">This article describes the components and processes involved when replicating on-premises Hyper-V virtual machines (VMs) in System Center Virtual Machine Manager (VMM) clouds, to a secondary VMM site using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="bb273-105">Комментарии можно добавить в конце этой статьи или на [форуме по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="bb273-105">Post any comments at the bottom of this article, or in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="architectural-components"></a><span data-ttu-id="bb273-106">Компоненты архитектуры</span><span class="sxs-lookup"><span data-stu-id="bb273-106">Architectural components</span></span>

<span data-ttu-id="bb273-107">Для репликации виртуальных машин Hyper-V на дополнительный сайт VMM вам потребуется следующее.</span><span class="sxs-lookup"><span data-stu-id="bb273-107">Here's what you need for replicating Hyper-V VMs to a secondary VMM site.</span></span>

<span data-ttu-id="bb273-108">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="bb273-108">**Component**</span></span> | <span data-ttu-id="bb273-109">**Расположение**</span><span class="sxs-lookup"><span data-stu-id="bb273-109">**Location**</span></span> | <span data-ttu-id="bb273-110">**Дополнительные сведения**</span><span class="sxs-lookup"><span data-stu-id="bb273-110">**Details**</span></span>
--- | --- | ---
<span data-ttu-id="bb273-111">**Таблицы Azure**</span><span class="sxs-lookup"><span data-stu-id="bb273-111">**Azure**</span></span> | <span data-ttu-id="bb273-112">Подписка в Azure.</span><span class="sxs-lookup"><span data-stu-id="bb273-112">Subscription in Azure.</span></span> | <span data-ttu-id="bb273-113">Создайте хранилище служб восстановления в подписке Azure для координации процесса репликации между расположениями VMM и управления им.</span><span class="sxs-lookup"><span data-stu-id="bb273-113">You create a Recovery Services vault in the Azure subscription, to orchestrate and manage replication between VMM locations.</span></span>
<span data-ttu-id="bb273-114">**Сервер VMM**</span><span class="sxs-lookup"><span data-stu-id="bb273-114">**VMM server**</span></span> | <span data-ttu-id="bb273-115">Необходимо иметь основное и дополнительное расположение VMM.</span><span class="sxs-lookup"><span data-stu-id="bb273-115">You need a VMM primary and secondary location.</span></span> | <span data-ttu-id="bb273-116">Мы рекомендуем сервер VMM на основном и дополнительном сайтах.</span><span class="sxs-lookup"><span data-stu-id="bb273-116">We recommend a VMM server in the primary site, and one in the secondary site</span></span> 
<span data-ttu-id="bb273-117">**Сервер Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="bb273-117">**Hyper-V server**</span></span> |  <span data-ttu-id="bb273-118">Понадобится один или несколько серверов узлов Hyper-V в основном и дополнительном облаках VMM.</span><span class="sxs-lookup"><span data-stu-id="bb273-118">One or more Hyper-V host servers in the primary and secondary VMM clouds.</span></span> | <span data-ttu-id="bb273-119">Данные реплицируются между основным и дополнительным серверами узлов Hyper-V через локальную сеть или VPN-подключение с использованием проверки подлинности Kerberos или на основе сертификатов.</span><span class="sxs-lookup"><span data-stu-id="bb273-119">Data is replicated between the primary and secondary Hyper-V host servers over the LAN or VPN, using Kerberos or certificate authentication.</span></span>  
<span data-ttu-id="bb273-120">**Виртуальные машины Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="bb273-120">**Hyper-V VMs**</span></span> | <span data-ttu-id="bb273-121">Расположены на сервере узла Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="bb273-121">On Hyper-V host server.</span></span> | <span data-ttu-id="bb273-122">На исходном сервере узла должна быть установлена как минимум одна виртуальная машина, которую необходимо реплицировать.</span><span class="sxs-lookup"><span data-stu-id="bb273-122">The source host server should have at least one VM that you want to replicate.</span></span>

## <a name="replication-process"></a><span data-ttu-id="bb273-123">Процесс репликации</span><span class="sxs-lookup"><span data-stu-id="bb273-123">Replication process</span></span>

1. <span data-ttu-id="bb273-124">Необходимо настроить учетную запись Azure, создать хранилище служб восстановления и указать целевые объекты для репликации.</span><span class="sxs-lookup"><span data-stu-id="bb273-124">You set up the Azure account, create a Recovery Services vault, and specify what you want to replicate.</span></span>
2. <span data-ttu-id="bb273-125">Настройте исходные и целевые параметры репликации, в том числе установите поставщик Azure Site Recovery на серверах VMM и агент служб восстановления Microsoft Azure на каждом узле Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="bb273-125">You configure the source and target replication settings, which includes installing the Azure Site Recovery Provider on VMM servers, and the Microsoft Azure Recovery Services agent on each Hyper-V host.</span></span>
3. <span data-ttu-id="bb273-126">Создайте политику репликации для исходного облака VMM.</span><span class="sxs-lookup"><span data-stu-id="bb273-126">You create a replication policy for the source VMM cloud.</span></span> <span data-ttu-id="bb273-127">Политика применяется ко всем виртуальным машинам, расположенным на узлах в облаке.</span><span class="sxs-lookup"><span data-stu-id="bb273-127">The policy is applied to all VMs located on hosts in the cloud.</span></span>
4. <span data-ttu-id="bb273-128">Включите репликацию для каждой VMM, чтобы выполнить начальную репликацию виртуальной машины, используя выбранные параметры.</span><span class="sxs-lookup"><span data-stu-id="bb273-128">You enable replication for each VMM, and initial replication of a VM occurs in accordance with the settings you choose.</span></span>
5. <span data-ttu-id="bb273-129">После начальной репликации начинается репликация разностных изменений.</span><span class="sxs-lookup"><span data-stu-id="bb273-129">After initial replication, replication of delta changes begins.</span></span> <span data-ttu-id="bb273-130">Отслеживаемые изменения для элемента хранятся в HRL-файле.</span><span class="sxs-lookup"><span data-stu-id="bb273-130">Tracked changes for an item are held in a .hrl file.</span></span>


![Из локальной среды в локальную среду](./media/vmm-to-vmm-walkthrough-architecture/arch-onprem-onprem.png)

## <a name="failover-and-failback-process"></a><span data-ttu-id="bb273-132">Процесс отработки отказа и восстановления размещения</span><span class="sxs-lookup"><span data-stu-id="bb273-132">Failover and failback process</span></span>

1. <span data-ttu-id="bb273-133">Вы можете запустить плановую или внеплановую [отработку отказа](site-recovery-failover.md) между локальными сайтами.</span><span class="sxs-lookup"><span data-stu-id="bb273-133">You can run a planned or unplanned [failover](site-recovery-failover.md) between on-premises sites.</span></span> <span data-ttu-id="bb273-134">Чтобы не допустить потери данных при выполнении плановой отработки отказа, выключите исходные виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="bb273-134">If you run a planned failover, then source VMs are shut down to ensure no data loss.</span></span>
2. <span data-ttu-id="bb273-135">Вы можете выполнить отработку отказа одного компьютера или создать [планы восстановления](site-recovery-create-recovery-plans.md) для координации отработки отказа нескольких компьютеров.</span><span class="sxs-lookup"><span data-stu-id="bb273-135">You can fail over a single machine, or create [recovery plans](site-recovery-create-recovery-plans.md) to orchestrate failover of multiple machines.</span></span>
4. <span data-ttu-id="bb273-136">Если вы выполнили внеплановую отработку отказа с переносом на дополнительный сайт, то после этого компьютеры в дополнительном расположении не будут защищены и для них не будет выполняться репликация.</span><span class="sxs-lookup"><span data-stu-id="bb273-136">If you perform an unplanned failover to a secondary site, after the failover machines in the secondary location aren't enabled for protection or replication.</span></span> <span data-ttu-id="bb273-137">Если вы выполнили плановую отработку отказа, то после этого компьютеры в дополнительном расположении будут защищены.</span><span class="sxs-lookup"><span data-stu-id="bb273-137">If you ran a planned failover, after the failover, machines in the secondary location are protected.</span></span>
5. <span data-ttu-id="bb273-138">Затем необходимо зафиксировать отработку отказа для получения доступа к рабочей нагрузке из виртуальной машины реплики.</span><span class="sxs-lookup"><span data-stu-id="bb273-138">Then, you commit the failover to start accessing the workload from the replica VM.</span></span>
6. <span data-ttu-id="bb273-139">Когда основной сайт снова станет доступным, необходимо запустить обратную репликацию, чтобы она выполнялась с дополнительного сайта на основной.</span><span class="sxs-lookup"><span data-stu-id="bb273-139">When your primary site is available again, you initiate reverse replication to replicate from the secondary site to the primary.</span></span> <span data-ttu-id="bb273-140">При обратной репликации виртуальные машины будут переведены в защищенное состояние, но при этом активным расположением по-прежнему останется дополнительный центр обработки данных.</span><span class="sxs-lookup"><span data-stu-id="bb273-140">Reverse replication brings the virtual machines into a protected state, but the secondary datacenter is still the active location.</span></span>
7. <span data-ttu-id="bb273-141">Чтобы сделать активным расположением основной сайт, необходимо запустить плановую отработку отказа с переносом из дополнительного расположения в основное, а затем выполнить еще одну обратную репликацию.</span><span class="sxs-lookup"><span data-stu-id="bb273-141">To make the primary site into the active location again, you initiate a planned failover from secondary to primary, followed by another reverse replication.</span></span>



## <a name="next-steps"></a><span data-ttu-id="bb273-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bb273-142">Next steps</span></span>

<span data-ttu-id="bb273-143">Перейдите к статье [Step 2: Review the prerequisites and limitations for Hyper-V VM replication to a secondary VMM site](vmm-to-vmm-walkthrough-prerequisites.md) (Шаг 2. Просмотр предварительных требований и ограничений для репликации виртуальной машины Hyper-V на дополнительный сайт VMM).</span><span class="sxs-lookup"><span data-stu-id="bb273-143">Go to [Step 2: Review the prerequisites and limitations](vmm-to-vmm-walkthrough-prerequisites.md).</span></span>
