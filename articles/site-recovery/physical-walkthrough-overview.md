---
title: "aaaReplicate физической локальной tooAzure серверов с Azure Site Recovery | Документы Microsoft"
description: "Общие шаги hello репликации рабочих нагрузок на локальных tooAzure физических серверов Windows и Linux с hello службы Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 20122f01-929a-4675-b85b-a9b99d2618bc
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: f801b9544072d4029ec06cc1abfd4ff370e852e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-physical-servers-tooazure-with-site-recovery"></a><span data-ttu-id="a2172-103">Репликация физических серверов tooAzure с Site Recovery</span><span class="sxs-lookup"><span data-stu-id="a2172-103">Replicate physical servers tooAzure with Site Recovery</span></span>

<span data-ttu-id="a2172-104">В этой статье содержится обзор hello действия требуется tooreplicate в локальной среде Windows и Linux физических серверов tooAzure, с помощью hello [Azure Site Recovery](site-recovery-overview.md) в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a2172-104">This article provides an overview of hello steps required tooreplicate on-premises Windows/Linux physical servers tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="a2172-105">Шаг 1. Проверка архитектуры и предварительных требований</span><span class="sxs-lookup"><span data-stu-id="a2172-105">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="a2172-106">Прежде чем начать развертывание, просмотрите hello архитектура сценария и убедитесь, что вы понимаете все компоненты hello необходим tooset hello развертывания.</span><span class="sxs-lookup"><span data-stu-id="a2172-106">Before you start deployment, review hello scenario architecture, and make sure you understand all hello components you need tooset up hello deployment.</span></span>

<span data-ttu-id="a2172-107">Go слишком[шаг 1: обзор архитектуры hello](physical-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="a2172-107">Go too[Step 1: Review hello architecture](physical-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="a2172-108">Шаг 2. Проверка предварительных требований</span><span class="sxs-lookup"><span data-stu-id="a2172-108">Step 2: Review prerequisites</span></span>

<span data-ttu-id="a2172-109">Убедитесь, что установлены необходимые компоненты hello на месте для каждого компонента развертывания:</span><span class="sxs-lookup"><span data-stu-id="a2172-109">Make sure you have hello prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="a2172-110">**Предварительные требования Azure**: учетная запись Microsoft Azure, сети Azure и учетные записи хранения.</span><span class="sxs-lookup"><span data-stu-id="a2172-110">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="a2172-111">**Локальные компоненты Site Recovery**: компьютер, на котором запущены локальные компоненты Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="a2172-111">**On-premises Site Recovery components**: You need a machine running on-premises Site Recovery components.</span></span>
- <span data-ttu-id="a2172-112">**Реплицировать машины**: серверы, требуется tooreplicate должны toocomply с локальной и требования к Azure.</span><span class="sxs-lookup"><span data-stu-id="a2172-112">**Replicated machines**: Servers you want tooreplicate need toocomply with on-premises and Azure requirements.</span></span>

<span data-ttu-id="a2172-113">Go слишком[шаг 2: Проверьте предварительные условия и ограничения](physical-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="a2172-113">Go too[Step 2: Review prerequisites and limitations](physical-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="a2172-114">Шаг 3. Планирование ресурсов</span><span class="sxs-lookup"><span data-stu-id="a2172-114">Step 3: Plan capacity</span></span>

<span data-ttu-id="a2172-115">При выполнении полного развертывания необходимо toofigure какие ресурсы репликации необходимо.</span><span class="sxs-lookup"><span data-stu-id="a2172-115">If you're doing a full deployment you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="a2172-116">Если вы выполняете быстро настроить среду tootest hello, этот шаг можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="a2172-116">If you're doing a quick set up tootest hello environment, you can skip this step.</span></span>

<span data-ttu-id="a2172-117">Go слишком[Step 3: Планирование емкости](physical-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="a2172-117">Go too[Step 3: Plan capacity](physical-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="a2172-118">Шаг 4. Планирование сетей</span><span class="sxs-lookup"><span data-stu-id="a2172-118">Step 4: Plan networking</span></span>

<span data-ttu-id="a2172-119">Необходимо toodo какой-либо сети, планирование tooensure виртуальных машинах Azure, подключенной toonetworks после отработки отказа, и что у hello правой IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="a2172-119">You need toodo some network planning tooensure that Azure VMs are connected toonetworks after failover occurs, and  that that they have hello right IP addresses.</span></span>

<span data-ttu-id="a2172-120">Go слишком[шаг 4: Планирование сети](physical-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="a2172-120">Go too[Step 4: Plan networking](physical-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="a2172-121">Шаг 5. Подготовка ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="a2172-121">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="a2172-122">Прежде чем начать, настройте сети и хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="a2172-122">Set up Azure networks and storage before you start.</span></span> 

<span data-ttu-id="a2172-123">Go слишком[шаг 5: Подготовка Azure](physical-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="a2172-123">Go too[Step 5: Prepare Azure](physical-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-set-up-a-vault"></a><span data-ttu-id="a2172-124">Шаг 6. Настройка хранилища</span><span class="sxs-lookup"><span data-stu-id="a2172-124">Step 6: Set up a vault</span></span>

<span data-ttu-id="a2172-125">Настройка tooorchestrate хранилище служб восстановления и управление репликацией.</span><span class="sxs-lookup"><span data-stu-id="a2172-125">You set up a Recovery Services vault tooorchestrate and manage replication.</span></span> <span data-ttu-id="a2172-126">При настройке хранилища hello, укажите, что должно tooreplicate, и когда необходимо tooreplicate его.</span><span class="sxs-lookup"><span data-stu-id="a2172-126">When you set up hello vault, you specify what you want tooreplicate, and where you want tooreplicate it to.</span></span>

<span data-ttu-id="a2172-127">Go слишком[шаг 6: Настройка хранилища](physical-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="a2172-127">Go too[Step 6: Set up a vault](physical-walkthrough-create-vault.md)</span></span>

## <a name="step-7-configure-source-and-target-settings"></a><span data-ttu-id="a2172-128">Шаг 7. Настройка параметров исходной и целевой среды</span><span class="sxs-lookup"><span data-stu-id="a2172-128">Step 7: Configure source and target settings</span></span>

<span data-ttu-id="a2172-129">Настройте параметры для hello исходный и конечный сайт (Azure).</span><span class="sxs-lookup"><span data-stu-id="a2172-129">Configure settings for hello source and target (Azure) site.</span></span> <span data-ttu-id="a2172-130">Параметры источника включает в себя под управлением tooinstall единой установки hello локальных компонентов Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="a2172-130">Source settings includes running Unified Setup tooinstall hello on-premises Site Recovery components.</span></span>

<span data-ttu-id="a2172-131">Go слишком[шаг 7: Настройка hello исходной и целевой](physical-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="a2172-131">Go too[Step 7: Set up hello source and target](physical-walkthrough-source-target.md)</span></span>

## <a name="step-8-set-up-a-replication-policy"></a><span data-ttu-id="a2172-132">Шаг 8. Настройка политики репликации</span><span class="sxs-lookup"><span data-stu-id="a2172-132">Step 8: Set up a replication policy</span></span>

<span data-ttu-id="a2172-133">Настройки toospecify политики физических серверов должны быть реплицированы.</span><span class="sxs-lookup"><span data-stu-id="a2172-133">You set up a policy toospecify how physical servers should replicate.</span></span>

<span data-ttu-id="a2172-134">Go слишком[Step 8: настроить политику репликации](physical-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="a2172-134">Go too[Step 8: Set up a replication policy](physical-walkthrough-replication.md)</span></span>

## <a name="step-9-install-hello-mobility-service"></a><span data-ttu-id="a2172-135">Шаг 9: Установка службы Mobility hello</span><span class="sxs-lookup"><span data-stu-id="a2172-135">Step 9: Install hello Mobility service</span></span>

<span data-ttu-id="a2172-136">Hello службы Mobility service необходимо установить на каждом сервере требуется tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="a2172-136">hello Mobility service must be installed on each server you want tooreplicate.</span></span> <span data-ttu-id="a2172-137">Существует несколько способов tooset hello службы, с установкой Принудительная или по запросу.</span><span class="sxs-lookup"><span data-stu-id="a2172-137">There are a few ways tooset up hello service, with push or pull installation.</span></span>

<span data-ttu-id="a2172-138">Go слишком[шаг 9: Установка службы Mobility hello](physical-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="a2172-138">Go too[Step 9: Install hello Mobility service](physical-walkthrough-install-mobility.md)</span></span>

## <a name="step-10-enable-replication"></a><span data-ttu-id="a2172-139">Шаг 10. Включение репликации</span><span class="sxs-lookup"><span data-stu-id="a2172-139">Step 10: Enable replication</span></span>

<span data-ttu-id="a2172-140">После запуска hello службы Mobility service на сервере, можно включить для него репликацию.</span><span class="sxs-lookup"><span data-stu-id="a2172-140">After hello Mobility service is running on a server, you can enable replication for it.</span></span> <span data-ttu-id="a2172-141">После включения, происходит начальной репликации hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a2172-141">After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="a2172-142">Go слишком[шаг 10: включение репликации](physical-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="a2172-142">Go too[Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>

## <a name="step-11-run-a-test-failover"></a><span data-ttu-id="a2172-143">Шаг 11. Запуск тестовой отработки отказа</span><span class="sxs-lookup"><span data-stu-id="a2172-143">Step 11: Run a test failover</span></span>

<span data-ttu-id="a2172-144">После завершения начальной репликации и разностная репликация выполняется, можно запустить тест отработки отказа toomake, убедиться, что все работает правильно.</span><span class="sxs-lookup"><span data-stu-id="a2172-144">After initial replication finishes and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="a2172-145">Go слишком[шаг 11: запустите тестовую отработку отказа](physical-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="a2172-145">Go too[Step 11: Run a test failover](physical-walkthrough-test-failover.md)</span></span>

