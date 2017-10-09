---
title: "aaaReplicate tooAzure виртуальных машин Hyper-V с помощью Azure Site Recovery | Документы Microsoft"
description: "Описывает способ tooorchestrate репликации, отработки отказа и восстановления локальных Hyper-V виртуальных машин tooAzure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: efddd986-bc13-4a1d-932d-5484cdc7ad8d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: ab9cd14149ef32a416428d0f4327aa18b042e9c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-tooazure"></a><span data-ttu-id="ada6d-103">TooAzure виртуальных машин (без VMM) реплицировать Hyper-V</span><span class="sxs-lookup"><span data-stu-id="ada6d-103">Replicate Hyper-V virtual machines (without VMM) tooAzure</span></span> 

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ada6d-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="ada6d-104">Azure portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="ada6d-105">Классическая модель Azure</span><span class="sxs-lookup"><span data-stu-id="ada6d-105">Azure classic</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
> * [<span data-ttu-id="ada6d-106">PowerShell — Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ada6d-106">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

<span data-ttu-id="ada6d-107">В этой статье содержится обзор hello шаги, необходимые tooreplicate в локальной среде Hyper-V виртуальных машин tooAzure, с помощью hello [Azure Site Recovery](site-recovery-overview.md) в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ada6d-107">This article provides an overview of hello steps required tooreplicate on-premises Hyper-V virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) in hello Azure portal.</span></span> <span data-ttu-id="ada6d-108">В этом развертывании Hyper-V виртуальные машины не передаются под управление System Center Virtual Machine Manager (VMM).</span><span class="sxs-lookup"><span data-stu-id="ada6d-108">In this deployment Hyper-V VMs aren't managed by System Center Virtual Machine Manager (VMM).</span></span>


<span data-ttu-id="ada6d-109">После считывания в этой статье, отправлять любые комментарии внизу hello или задавайте технические вопросы на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="ada6d-109">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="ada6d-110">Шаг 1. Проверка архитектуры и предварительных требований</span><span class="sxs-lookup"><span data-stu-id="ada6d-110">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="ada6d-111">Чтобы начать развертывание, просмотрите hello архитектура сценария и убедитесь, что вы понимаете все компоненты hello требуется toodeploy</span><span class="sxs-lookup"><span data-stu-id="ada6d-111">Before you start deployment, review hello scenario architecture, and make sure you understand all hello components you need toodeploy</span></span>

<span data-ttu-id="ada6d-112">Go слишком[шаг 1: обзор архитектуры hello](hyper-v-site-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="ada6d-112">Go too[Step 1: Review hello architecture](hyper-v-site-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="ada6d-113">Шаг 2. Проверка предварительных требований</span><span class="sxs-lookup"><span data-stu-id="ada6d-113">Step 2: Review prerequisites</span></span>

<span data-ttu-id="ada6d-114">Убедитесь, что установлены необходимые компоненты hello на месте для каждого компонента развертывания:</span><span class="sxs-lookup"><span data-stu-id="ada6d-114">Make sure you have hello prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="ada6d-115">**Предварительные требования Azure**: учетная запись Microsoft Azure, сети Azure и учетные записи хранения.</span><span class="sxs-lookup"><span data-stu-id="ada6d-115">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="ada6d-116">**Предварительные требования локальной среды Hyper-V**: убедитесь, что узлы Hyper-V подготовлены к развертыванию Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="ada6d-116">**On-premises Hyper-V prerequisites**: Make sure Hyper-V hosts are prepared for Site Recovery deployment.</span></span>
- <span data-ttu-id="ada6d-117">**Репликация виртуальных машин**: виртуальные машины, нужно tooreplicate требуется toocomply требованиям Azure.</span><span class="sxs-lookup"><span data-stu-id="ada6d-117">**Replicated VMs**: VMs you want tooreplicate need toocomply with Azure requirements.</span></span>

<span data-ttu-id="ada6d-118">Go слишком[шаг 2: Проверьте предварительные условия и ограничения](hyper-v-site-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="ada6d-118">Go too[Step 2: Verify prerequisites and limitations](hyper-v-site-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="ada6d-119">Шаг 3. Планирование ресурсов</span><span class="sxs-lookup"><span data-stu-id="ada6d-119">Step 3: Plan capacity</span></span>

<span data-ttu-id="ada6d-120">При выполнении полного развертывания необходимо toofigure какие ресурсы репликации необходимо.</span><span class="sxs-lookup"><span data-stu-id="ada6d-120">If you're doing a full deployment you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="ada6d-121">Существует несколько из доступных toohelp средства это сделать.</span><span class="sxs-lookup"><span data-stu-id="ada6d-121">There are a couple of tools available toohelp you do this.</span></span> <span data-ttu-id="ada6d-122">Go tooStep 2.</span><span class="sxs-lookup"><span data-stu-id="ada6d-122">Go tooStep 2.</span></span> <span data-ttu-id="ada6d-123">Этот шаг можно пропустить, если вы выполняете быстро настроить среду tootest hello.</span><span class="sxs-lookup"><span data-stu-id="ada6d-123">If you're doing a quick set up tootest hello environment you can skip this step.</span></span>

<span data-ttu-id="ada6d-124">Go слишком[Step 3: Планирование емкости](hyper-v-site-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="ada6d-124">Go too[Step 3: Plan capacity](hyper-v-site-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="ada6d-125">Шаг 4. Планирование сетей</span><span class="sxs-lookup"><span data-stu-id="ada6d-125">Step 4: Plan networking</span></span>

<span data-ttu-id="ada6d-126">Необходимо toodo какой-либо сети, планирование tooensure виртуальных машинах Azure, подключенной toonetworks после отработки отказа, и что у hello правой IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="ada6d-126">You need toodo some network planning tooensure that Azure VMs are connected toonetworks after failover occurs, and  that that they have hello right IP addresses.</span></span>

<span data-ttu-id="ada6d-127">Go слишком[шаг 4: Планирование сети](hyper-v-site-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="ada6d-127">Go too[Step 4: Plan networking](hyper-v-site-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="ada6d-128">Шаг 5. Подготовка ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="ada6d-128">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="ada6d-129">Прежде чем начать, настройте сети и хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="ada6d-129">Set up Azure networks and storage before you start.</span></span> <span data-ttu-id="ada6d-130">Это можно сделать при развертывании, но мы рекомендуем это сделать до начала процесса.</span><span class="sxs-lookup"><span data-stu-id="ada6d-130">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="ada6d-131">Go слишком[шаг 5: Подготовка Azure](hyper-v-site-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="ada6d-131">Go too[Step 5: Prepare Azure](hyper-v-site-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-prepare-hyper-v"></a><span data-ttu-id="ada6d-132">Шаг 6. Подготовка Hyper-V</span><span class="sxs-lookup"><span data-stu-id="ada6d-132">Step 6: Prepare Hyper-V</span></span>

<span data-ttu-id="ada6d-133">Убедитесь, что серверы Hyper-V соответствуют требованиям к развертыванию Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="ada6d-133">Make sure that Hyper-V servers meet Site Recovery deployment requirements.</span></span>

<span data-ttu-id="ada6d-134">Go слишком[шаг 6: Подготовка Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="ada6d-134">Go too[Step 6: Prepare Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="ada6d-135">Шаг 7. Настройка хранилища</span><span class="sxs-lookup"><span data-stu-id="ada6d-135">Step 7: Set up a vault</span></span>

<span data-ttu-id="ada6d-136">Требуется tooset копирование tooorchestrate хранилище служб восстановления и управление репликацией.</span><span class="sxs-lookup"><span data-stu-id="ada6d-136">You need tooset up a Recovery Services vault tooorchestrate and manage replication.</span></span> <span data-ttu-id="ada6d-137">При настройке хранилища hello, укажите, что должно tooreplicate, и когда необходимо tooreplicate его.</span><span class="sxs-lookup"><span data-stu-id="ada6d-137">When you set up hello vault, you specify what you want tooreplicate, and where you want tooreplicate it to.</span></span>

<span data-ttu-id="ada6d-138">Go слишком[шаг 7: Создание хранилища](hyper-v-site-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="ada6d-138">Go too[Step 7: Create a vault](hyper-v-site-walkthrough-create-vault.md)</span></span>

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="ada6d-139">Шаг 8. Настройка параметров исходной и целевой среды</span><span class="sxs-lookup"><span data-stu-id="ada6d-139">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="ada6d-140">Настройка hello исходной и целевой объект, который используется для репликации.</span><span class="sxs-lookup"><span data-stu-id="ada6d-140">Set up hello source and target that's used for replication.</span></span> <span data-ttu-id="ada6d-141">Настройка параметров источника включает в себя добавление Hyper-V hosts tooa сайт Hyper-V, установка hello поставщика Site Recovery и агента служб восстановления на каждом узле Hyper-V и регистрации узла hello в hello в хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="ada6d-141">Setting up source settings includes adding Hyper-V hosts tooa Hyper-V site, installing hello Site Recovery Provider and Recovery Services agent on each Hyper-V host, and registering hello site in hello Recovery Services vault.</span></span>

<span data-ttu-id="ada6d-142">Go слишком[Step 8: Настройка hello исходной и целевой](hyper-v-site-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="ada6d-142">Go too[Step 8: Set up hello source and target](hyper-v-site-walkthrough-source-target.md)</span></span>

## <a name="step-9-set-up-a-replication-policy"></a><span data-ttu-id="ada6d-143">Шаг 9. Настройка политики репликации</span><span class="sxs-lookup"><span data-stu-id="ada6d-143">Step 9: Set up a replication policy</span></span>

<span data-ttu-id="ada6d-144">Вы настроили параметры политики toospecify репликации для виртуальных машин Hyper-V в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="ada6d-144">You set up a policy toospecify replication settings for Hyper-V VMs in hello vault.</span></span>

<span data-ttu-id="ada6d-145">Go слишком[шаг 9: настроить политику репликации](hyper-v-site-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="ada6d-145">Go too[Step 9: Set up a replication policy](hyper-v-site-walkthrough-replication.md)</span></span>


## <a name="step-10-enable-replication"></a><span data-ttu-id="ada6d-146">Шаг 10. Включение репликации</span><span class="sxs-lookup"><span data-stu-id="ada6d-146">Step 10: Enable replication</span></span>

<span data-ttu-id="ada6d-147">После того как вы политику репликации на месте, после включения, происходит начальной репликации hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="ada6d-147">After you have a replication policy in place,  After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="ada6d-148">Go слишком[шаг 10: включение репликации](hyper-v-site-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="ada6d-148">Go too[Step 10: Enable replication](hyper-v-site-walkthrough-enable-replication.md)</span></span>

## <a name="step-11-run-a-test-failover"></a><span data-ttu-id="ada6d-149">Шаг 11. Запуск тестовой отработки отказа</span><span class="sxs-lookup"><span data-stu-id="ada6d-149">Step 11: Run a test failover</span></span>

<span data-ttu-id="ada6d-150">После завершения первоначальной репликации, а разностная репликация выполняется, можно запустить тест отработки отказа toomake, убедиться, что все работает правильно.</span><span class="sxs-lookup"><span data-stu-id="ada6d-150">After initial replication finishes, and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="ada6d-151">Go слишком[шаг 11: запустите тестовую отработку отказа](hyper-v-site-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="ada6d-151">Go too[Step 11: Run a test failover](hyper-v-site-walkthrough-test-failover.md)</span></span>
