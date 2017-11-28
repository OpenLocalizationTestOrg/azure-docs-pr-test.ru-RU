---
title: "aaaReplicate виртуальных машин Hyper-V tooa вторичный сайт VMM с помощью Azure Site Recovery | Документы Microsoft"
description: "Обзор репликации виртуальных машин Hyper-V tooa вторичный сайт VMM с помощью портала Azure hello."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 476ca82a-8f5c-4498-9dcf-e1011d60ed59
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: raynew
ms.openlocfilehash: 90e44bfc2237dfa7646fb2b7b1e533a7f6d83c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site"></a><span data-ttu-id="418a2-103">Реплицировать виртуальные машины Hyper-V в VMM облаков tooa вторичного сайта, VMM</span><span class="sxs-lookup"><span data-stu-id="418a2-103">Replicate Hyper-V virtual machines in VMM clouds tooa secondary VMM site</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="418a2-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="418a2-104">Azure portal</span></span>](site-recovery-vmm-to-vmm.md)
> * [<span data-ttu-id="418a2-105">Классический портал.</span><span class="sxs-lookup"><span data-stu-id="418a2-105">Classic portal</span></span>](site-recovery-vmm-to-vmm-classic.md)
> * [<span data-ttu-id="418a2-106">PowerShell — Resource Manager</span><span class="sxs-lookup"><span data-stu-id="418a2-106">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

<span data-ttu-id="418a2-107">В этой статье содержится обзор hello действия требуются tooreplicate в локальной среде Hyper-V виртуальных машин (ВМ), управляемых в облаках диспетчера виртуальных машин System Center (VMM), tooa вторичного расположения VMM, с помощью [Azure Site Recovery](site-recovery-overview.md)в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="418a2-107">This article provides an overview of hello steps required tooreplicate on-premises Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds, tooa secondary VMM location, using [Azure Site Recovery](site-recovery-overview.md) in hello Azure portal.</span></span>

<span data-ttu-id="418a2-108">После считывания в этой статье, отправлять любые комментарии, внизу hello, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="418a2-108">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-hello-scenario-architecture"></a><span data-ttu-id="418a2-109">Шаг 1: Просмотрите архитектура сценария hello</span><span class="sxs-lookup"><span data-stu-id="418a2-109">Step 1: Review hello scenario architecture</span></span>

<span data-ttu-id="418a2-110">Прежде чем начать развертывание, просмотрите hello архитектура сценария и убедитесь, что вы понимаете все компоненты hello необходим toodeploy.</span><span class="sxs-lookup"><span data-stu-id="418a2-110">Before you start deployment, review hello scenario architecture, and make sure that you understand all hello components you need toodeploy.</span></span>

<span data-ttu-id="418a2-111">Go слишком[шаг 1: обзор архитектуры hello](vmm-to-vmm-walkthrough-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="418a2-111">Go too[Step 1: Review hello architecture](vmm-to-vmm-walkthrough-architecture.md).</span></span>

## <a name="step-2-review-prerequisites-and-limitations"></a><span data-ttu-id="418a2-112">Шаг 2. Просмотр предварительных условий и ограничений</span><span class="sxs-lookup"><span data-stu-id="418a2-112">Step 2: Review prerequisites and limitations</span></span>

<span data-ttu-id="418a2-113">Убедитесь, что вы понимаете предварительные условия для развертывания hello и ограничения.</span><span class="sxs-lookup"><span data-stu-id="418a2-113">Make sure that you understand hello deployment prerequisites and limitations.</span></span>

<span data-ttu-id="418a2-114">**Необходимые компоненты Azure**: необходима подписка Microsoft Azure и служб восстановления Azure, хранилище, tooorchestrate и управление репликацией.</span><span class="sxs-lookup"><span data-stu-id="418a2-114">**Azure prerequisites**: You need a Microsoft Azure subscription, and Azure Recovery Services vault, tooorchestrate and manage replication.</span></span>
<span data-ttu-id="418a2-115">**Локальные серверы VMM и узлы Hyper-V.** Убедитесь, что серверы VMM и узлы Hyper-V совместимы и подготовлены к развертыванию Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="418a2-115">**On-premises VMM servers and Hyper-V hosts**: Make sure that VMM servers and Hyper-V hosts are compliant and prepared for Site Recovery deployment.</span></span>

<span data-ttu-id="418a2-116">Go слишком[шаг 2: Проверьте предварительные условия и ограничения](vmm-to-vmm-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="418a2-116">Go too[Step 2: Verify prerequisites and limitations](vmm-to-vmm-walkthrough-prerequisites.md).</span></span>

## <a name="step-3-plan-networking"></a><span data-ttu-id="418a2-117">Шаг 3. Планирование сетей</span><span class="sxs-lookup"><span data-stu-id="418a2-117">Step 3: Plan networking</span></span>

<span data-ttu-id="418a2-118">Необходимо toodo какой-либо сети, планирование tooensure, которые можно настроить сетевое сопоставление между сетями виртуальных Машин VMM при развертывании hello сценария.</span><span class="sxs-lookup"><span data-stu-id="418a2-118">You need toodo some network planning tooensure that you can configure network mapping between VMM VM networks when you deploy hello scenario.</span></span>

<span data-ttu-id="418a2-119">Go слишком[Step 3: Планирование сети](vmm-to-vmm-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="418a2-119">Go too[Step 3: Plan networking](vmm-to-vmm-walkthrough-network.md).</span></span>


## <a name="step-4-prepare-vmm-and-hyper-v"></a><span data-ttu-id="418a2-120">Шаг 4. Подготовка VMM и Hyper-V</span><span class="sxs-lookup"><span data-stu-id="418a2-120">Step 4: Prepare VMM and Hyper-V</span></span>

<span data-ttu-id="418a2-121">Подготовка серверов VMM hello и узлов Hyper-V для развертывания службы восстановления сайтов.</span><span class="sxs-lookup"><span data-stu-id="418a2-121">Prepare hello VMM servers and Hyper-V hosts for Site Recovery deployment.</span></span>

<span data-ttu-id="418a2-122">Go слишком[шаг 4: Подготовка локальных серверов](vmm-to-vmm-walkthrough-vmm-hyper-v.md).</span><span class="sxs-lookup"><span data-stu-id="418a2-122">Go too[Step 4: Prepare on-premises servers](vmm-to-vmm-walkthrough-vmm-hyper-v.md).</span></span>

## <a name="step-5-set-up-a-vault"></a><span data-ttu-id="418a2-123">Шаг 5. Настройка хранилища</span><span class="sxs-lookup"><span data-stu-id="418a2-123">Step 5: Set up a vault</span></span>

<span data-ttu-id="418a2-124">Настройте хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="418a2-124">Set up a Recovery Services vault.</span></span> <span data-ttu-id="418a2-125">хранилище Hello содержит параметры конфигурации и управляет репликации.</span><span class="sxs-lookup"><span data-stu-id="418a2-125">hello vault contains configuration settings, and orchestrates replication.</span></span>

<span data-ttu-id="418a2-126">[Шаг 5. Создание хранилища для репликации Hyper-V на дополнительный сайт](vmm-to-vmm-walkthrough-create-vault.md).</span><span class="sxs-lookup"><span data-stu-id="418a2-126">[Step 5: Set up a vault](vmm-to-vmm-walkthrough-create-vault.md).</span></span>

## <a name="step-6-set-up-source-and-target-settings"></a><span data-ttu-id="418a2-127">Шаг 6. Настройка исходной и целевой среды</span><span class="sxs-lookup"><span data-stu-id="418a2-127">Step 6: Set up source and target settings</span></span>

<span data-ttu-id="418a2-128">Настройка hello исходной и целевой репликации VMM местоположений.</span><span class="sxs-lookup"><span data-stu-id="418a2-128">Set up hello source and target replication VMM locations.</span></span> <span data-ttu-id="418a2-129">Добавьте хранилище toohello серверы VMM hello и загружать файлы установки hello для компонентов Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="418a2-129">Add hello VMM servers toohello vault, and download hello installation files for Site Recovery components.</span></span> <span data-ttu-id="418a2-130">Запустите программу установки поставщика Azure Site Recovery на сервере VMM hello.</span><span class="sxs-lookup"><span data-stu-id="418a2-130">Run Azure Site Recovery Provider setup on hello VMM server.</span></span> <span data-ttu-id="418a2-131">Программа установки устанавливает hello поставщика на сервере VMM hello и регистрирует hello сервер в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="418a2-131">Setup installs hello Provider on hello VMM server, and registers hello server in hello vault.</span></span> <span data-ttu-id="418a2-132">Установка агента служб восстановления Microsoft hello на каждом узле Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="418a2-132">You install hello Microsoft Recovery Services agent on each Hyper-V host.</span></span>

<span data-ttu-id="418a2-133">Go слишком[шаг 6: Настройка параметров исходной и целевой hello](vmm-to-vmm-walkthrough-source-target.md).</span><span class="sxs-lookup"><span data-stu-id="418a2-133">Go too[Step 6: Set up hello source and target settings](vmm-to-vmm-walkthrough-source-target.md).</span></span>

## <a name="step-7-configure-network-mapping"></a><span data-ttu-id="418a2-134">Шаг 7. Настройка сетевого сопоставления</span><span class="sxs-lookup"><span data-stu-id="418a2-134">Step 7: Configure network mapping</span></span>

<span data-ttu-id="418a2-135">Сопоставьте сети виртуальных Машин VMM в исходном и целевом расположении hello.</span><span class="sxs-lookup"><span data-stu-id="418a2-135">Map VMM VM networks in hello source and target locations.</span></span> <span data-ttu-id="418a2-136">После отработки отказа виртуальные машины создаются в целевой сети hello, maps toohello исходной сетью виртуальной Машины в какой hello находится исходной виртуальной Машины Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="418a2-136">After failover, VMs are created in hello target network that maps toohello source VM network in which hello source Hyper-V VM is located.</span></span>

<span data-ttu-id="418a2-137">Go слишком[шаг 7: Настройка сетевого сопоставления](vmm-to-vmm-walkthrough-network-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="418a2-137">Go too[Step 7: Configure network mapping](vmm-to-vmm-walkthrough-network-mapping.md).</span></span>


## <a name="step-8-set-up-a-replication-policy"></a><span data-ttu-id="418a2-138">Шаг 8. Настройка политики репликации</span><span class="sxs-lookup"><span data-stu-id="418a2-138">Step 8: Set up a replication policy</span></span>

<span data-ttu-id="418a2-139">Укажите, как виртуальные машины будут реплицироваться между расположениями VMM.</span><span class="sxs-lookup"><span data-stu-id="418a2-139">Specify how  VMs will be replicated between VMM locations.</span></span>

<span data-ttu-id="418a2-140">Go слишком[Step 8: настроить политику репликации](vmm-to-vmm-walkthrough-replication.md).</span><span class="sxs-lookup"><span data-stu-id="418a2-140">Go too[Step 8: Set up a replication policy](vmm-to-vmm-walkthrough-replication.md).</span></span>


## <a name="step-9-enable-replication-for-vms"></a><span data-ttu-id="418a2-141">Шаг 9. Включение репликации для виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="418a2-141">Step 9: Enable replication for VMs</span></span>

<span data-ttu-id="418a2-142">Выберите виртуальные машины hello требуется tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="418a2-142">Select hello VMs you want tooreplicate.</span></span> <span data-ttu-id="418a2-143">Включить виртуальную Машину для репликации триггеры hello начальной репликации toohello вторичного сайта, за которым следует текущих разностной репликации.</span><span class="sxs-lookup"><span data-stu-id="418a2-143">Enabling a VM for replication triggers hello initial replication toohello secondary site, followed by ongoing delta replication.</span></span>

<span data-ttu-id="418a2-144">Go слишком[шаг 9: включить репликацию](vmm-to-vmm-walkthrough-enable-replication.md).</span><span class="sxs-lookup"><span data-stu-id="418a2-144">Go too[Step 9: Enable replication](vmm-to-vmm-walkthrough-enable-replication.md).</span></span>


## <a name="step-10-run-a-test-failover"></a><span data-ttu-id="418a2-145">Шаг 10. Запуск тестовой отработки отказа</span><span class="sxs-lookup"><span data-stu-id="418a2-145">Step 10: Run a test failover</span></span>

<span data-ttu-id="418a2-146">Выполните тест отработки отказа toomake, убедиться, что все работает должным образом.</span><span class="sxs-lookup"><span data-stu-id="418a2-146">Run a test failover toomake sure everything's working as expected.</span></span>

<span data-ttu-id="418a2-147">Go слишком[шаг 10: запустите тестовую отработку отказа](vmm-to-vmm-walkthrough-test-failover.md).</span><span class="sxs-lookup"><span data-stu-id="418a2-147">Go too[Step 10: Run a test failover](vmm-to-vmm-walkthrough-test-failover.md).</span></span>
