---
title: "aaaReplicate tooAzure виртуальных машин VMware с Azure Site Recovery | Документы Microsoft"
description: "Общие сведения о hello действия для рабочих нагрузок на виртуальных машин VMware tooAzure репликации"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 7104f67a3635b916048dcb61bca770c89f0c77fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-vms-tooazure-with-site-recovery"></a><span data-ttu-id="6622b-103">Репликация виртуальных машин VMware tooAzure с Site Recovery</span><span class="sxs-lookup"><span data-stu-id="6622b-103">Replicate VMware VMs tooAzure with Site Recovery</span></span>

<span data-ttu-id="6622b-104">В этой статье содержится обзор hello действия требуется tooreplicate локальной VMware виртуальные машины tooAzure, с помощью hello [Azure Site Recovery](site-recovery-overview.md) в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="6622b-104">This article provides an overview of hello steps required tooreplicate on-premises VMware virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


![Процесс развертывания](./media/vmware-walkthrough-overview/vmware-to-azure-process.png)

<span data-ttu-id="6622b-106">**Рис. 1. Общие сведения о процессе развертывания**</span><span class="sxs-lookup"><span data-stu-id="6622b-106">**Figure 1: Deployment process summary**</span></span>

## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="6622b-107">Шаг 1. Проверка архитектуры и предварительных требований</span><span class="sxs-lookup"><span data-stu-id="6622b-107">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="6622b-108">Чтобы начать развертывание, просмотрите hello архитектура сценария и убедитесь, что вы понимаете все компоненты hello требуется toodeploy</span><span class="sxs-lookup"><span data-stu-id="6622b-108">Before you start deployment, review hello scenario architecture, and make sure you understand all hello components you need toodeploy</span></span>

<span data-ttu-id="6622b-109">Go слишком[шаг 1: обзор архитектуры hello](vmware-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="6622b-109">Go too[Step 1: Review hello architecture](vmware-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="6622b-110">Шаг 2. Проверка предварительных требований</span><span class="sxs-lookup"><span data-stu-id="6622b-110">Step 2: Review prerequisites</span></span>

<span data-ttu-id="6622b-111">Убедитесь, что установлены необходимые компоненты hello на месте для каждого компонента развертывания:</span><span class="sxs-lookup"><span data-stu-id="6622b-111">Make sure you have hello prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="6622b-112">**Предварительные требования Azure**: учетная запись Microsoft Azure, сети Azure и учетные записи хранения.</span><span class="sxs-lookup"><span data-stu-id="6622b-112">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="6622b-113">**Локальные компоненты Site Recovery**: компьютер, на котором запущены локальные компоненты Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="6622b-113">**On-premises Site Recovery components**: You need a machine running on-premises Site Recovery components.</span></span>
- <span data-ttu-id="6622b-114">**В локальной среде VMware предварительные требования**: требуется tooset учетных записей, чтобы Site Recovery можно обращаться к серверов VMware и виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="6622b-114">**On-premises VMware prerequisites**: You need tooset up accounts so that Site Recovery can access VMware servers and VMs.</span></span>
- <span data-ttu-id="6622b-115">**Репликация виртуальных машин**: виртуальные машины должны toocomply необходимость tooreplicate требованиям Azure и установлен компонент службы мобильности hello.</span><span class="sxs-lookup"><span data-stu-id="6622b-115">**Replicated VMs**: VMs you want tooreplicate need toocomply with Azure requirements, and have hello Mobility service component installed.</span></span>

<span data-ttu-id="6622b-116">Go слишком[шаг 2: Проверьте предварительные условия и ограничения](vmware-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="6622b-116">Go too[Step 2: Review prerequisites and limitations](vmware-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="6622b-117">Шаг 3. Планирование ресурсов</span><span class="sxs-lookup"><span data-stu-id="6622b-117">Step 3: Plan capacity</span></span>

<span data-ttu-id="6622b-118">При выполнении полного развертывания необходимо toofigure какие ресурсы репликации необходимо.</span><span class="sxs-lookup"><span data-stu-id="6622b-118">If you're doing a full deployment you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="6622b-119">Существует несколько из доступных toohelp средства это сделать.</span><span class="sxs-lookup"><span data-stu-id="6622b-119">There are a couple of tools available toohelp you do this.</span></span> <span data-ttu-id="6622b-120">Go tooStep 2.</span><span class="sxs-lookup"><span data-stu-id="6622b-120">Go tooStep 2.</span></span> <span data-ttu-id="6622b-121">Этот шаг можно пропустить, если вы выполняете быстро настроить среду tootest hello.</span><span class="sxs-lookup"><span data-stu-id="6622b-121">If you're doing a quick set up tootest hello environment you can skip this step.</span></span>

<span data-ttu-id="6622b-122">Go слишком[Step 3: Планирование емкости](vmware-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="6622b-122">Go too[Step 3: Plan capacity](vmware-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="6622b-123">Шаг 4. Планирование сетей</span><span class="sxs-lookup"><span data-stu-id="6622b-123">Step 4: Plan networking</span></span>

<span data-ttu-id="6622b-124">Необходимо toodo какой-либо сети, планирование tooensure виртуальных машинах Azure, подключенной toonetworks после отработки отказа, и что у hello правой IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="6622b-124">You need toodo some network planning tooensure that Azure VMs are connected toonetworks after failover occurs, and  that that they have hello right IP addresses.</span></span>

<span data-ttu-id="6622b-125">Go слишком[шаг 4: Планирование сети](vmware-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="6622b-125">Go too[Step 4: Plan networking](vmware-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="6622b-126">Шаг 5. Подготовка ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="6622b-126">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="6622b-127">Прежде чем начать, настройте сети и хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="6622b-127">Set up Azure networks and storage before you start.</span></span> <span data-ttu-id="6622b-128">Это можно сделать при развертывании, но мы рекомендуем это сделать до начала процесса.</span><span class="sxs-lookup"><span data-stu-id="6622b-128">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="6622b-129">Go слишком[шаг 5: Подготовка Azure](vmware-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="6622b-129">Go too[Step 5: Prepare Azure](vmware-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-prepare-vmware"></a><span data-ttu-id="6622b-130">Шаг 6. Подготовка VMware</span><span class="sxs-lookup"><span data-stu-id="6622b-130">Step 6: Prepare VMware</span></span>

<span data-ttu-id="6622b-131">Необходимые tooset учетные записи, используемые для восстановления сайта.</span><span class="sxs-lookup"><span data-stu-id="6622b-131">You need tooset up accounts that Site Recovery will use to:</span></span>

- <span data-ttu-id="6622b-132">Tooautomatically серверов виртуализации VMware доступа обнаружения виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="6622b-132">Access VMware virtualization servers tooautomatically detect VMs.</span></span>
- <span data-ttu-id="6622b-133">Доступ к службе Mobility hello tooinstall виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="6622b-133">Access VMs tooinstall hello Mobility service.</span></span> <span data-ttu-id="6622b-134">Каждая виртуальная машина, требуется tooreplicate должен быть установлен прежде чем агент службы Mobility hello можно включить для него репликацию.</span><span class="sxs-lookup"><span data-stu-id="6622b-134">Each VM you want tooreplicate must have hello Mobility service agent installed before you can enable replication for it.</span></span>

<span data-ttu-id="6622b-135">Go слишком[шаг 6: Подготовка VMware](vmware-walkthrough-prepare-vmware.md)</span><span class="sxs-lookup"><span data-stu-id="6622b-135">Go too[Step 6: Prepare VMware](vmware-walkthrough-prepare-vmware.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="6622b-136">Шаг 7. Настройка хранилища</span><span class="sxs-lookup"><span data-stu-id="6622b-136">Step 7: Set up a vault</span></span>

<span data-ttu-id="6622b-137">Требуется tooset копирование tooorchestrate хранилище служб восстановления и управление репликацией.</span><span class="sxs-lookup"><span data-stu-id="6622b-137">You need tooset up a Recovery Services vault tooorchestrate and manage replication.</span></span> <span data-ttu-id="6622b-138">При настройке хранилища hello, укажите, что должно tooreplicate, и когда необходимо tooreplicate его.</span><span class="sxs-lookup"><span data-stu-id="6622b-138">When you set up hello vault, you specify what you want tooreplicate, and where you want tooreplicate it to.</span></span>

<span data-ttu-id="6622b-139">Go слишком[шаг 7: Настройка хранилища](vmware-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="6622b-139">Go too[Step 7: Set up a vault](vmware-walkthrough-create-vault.md)</span></span>

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="6622b-140">Шаг 8. Настройка параметров исходной и целевой среды</span><span class="sxs-lookup"><span data-stu-id="6622b-140">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="6622b-141">Настройка hello исходной и целевой объект, который используется для репликации.</span><span class="sxs-lookup"><span data-stu-id="6622b-141">Set up hello source and target that's used for replication.</span></span> <span data-ttu-id="6622b-142">Настройка параметров источника включает запущен tooinstall единой установки компонентов Site Recovery hello в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="6622b-142">Setting up source settings includes running Unified Setup tooinstall hello on-premises Site Recovery components.</span></span>

<span data-ttu-id="6622b-143">Go слишком[Step 8: Настройка hello исходной и целевой](vmware-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="6622b-143">Go too[Step 8: Set up hello source and target](vmware-walkthrough-source-target.md)</span></span>

## <a name="step-9-set-up-a-replication-policy"></a><span data-ttu-id="6622b-144">Шаг 9. Настройка политики репликации</span><span class="sxs-lookup"><span data-stu-id="6622b-144">Step 9: Set up a replication policy</span></span>

<span data-ttu-id="6622b-145">Вы настроили параметры политики toospecify репликации для виртуальных машин VMware в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="6622b-145">You set up a policy toospecify replication settings for VMware VMs in hello vault.</span></span>

<span data-ttu-id="6622b-146">Go слишком[шаг 9: настроить политику репликации](vmware-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="6622b-146">Go too[Step 9: Set up a replication policy](vmware-walkthrough-replication.md)</span></span>

## <a name="step-10-install-hello-mobility-service"></a><span data-ttu-id="6622b-147">Шаг 10: Установка службы Mobility hello</span><span class="sxs-lookup"><span data-stu-id="6622b-147">Step 10: Install hello Mobility service</span></span>

<span data-ttu-id="6622b-148">должен быть установлен Hello службы Mobility service на каждой виртуальной Машины будет tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="6622b-148">hello Mobility service must be installed on each VM you want tooreplicate.</span></span> <span data-ttu-id="6622b-149">Существует несколько способов tooset hello службы с установкой Принудительная или по запросу.</span><span class="sxs-lookup"><span data-stu-id="6622b-149">There are a few ways tooset up hello service with push or pull installation.</span></span>

<span data-ttu-id="6622b-150">Go слишком[шаг 10: Установка службы Mobility hello](vmware-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="6622b-150">Go too[Step 10: Install hello Mobility service](vmware-walkthrough-install-mobility.md)</span></span>

## <a name="step-11-enable-replication"></a><span data-ttu-id="6622b-151">Шаг 11. Включение репликации</span><span class="sxs-lookup"><span data-stu-id="6622b-151">Step 11: Enable replication</span></span>

<span data-ttu-id="6622b-152">После запуска hello службы Mobility service на виртуальной Машине можно включить для него репликацию.</span><span class="sxs-lookup"><span data-stu-id="6622b-152">After hello Mobility service is running on a VM you can enable replication for it.</span></span> <span data-ttu-id="6622b-153">После включения, происходит начальной репликации hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="6622b-153">After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="6622b-154">Go слишком[шаг 11: включение репликации](vmware-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="6622b-154">Go too[Step 11: Enable replication](vmware-walkthrough-enable-replication.md)</span></span>

## <a name="step-12-run-a-test-failover"></a><span data-ttu-id="6622b-155">Шаг 12. Запуск тестовой отработки отказа</span><span class="sxs-lookup"><span data-stu-id="6622b-155">Step 12: Run a test failover</span></span>

<span data-ttu-id="6622b-156">После завершения первоначальной репликации, а разностная репликация выполняется, можно запустить тест отработки отказа toomake, убедиться, что все работает правильно.</span><span class="sxs-lookup"><span data-stu-id="6622b-156">After initial replication finishes, and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="6622b-157">Go слишком[шаг 12: запустите тестовую отработку отказа](vmware-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="6622b-157">Go too[Step 12: Run a test failover](vmware-walkthrough-test-failover.md)</span></span>
