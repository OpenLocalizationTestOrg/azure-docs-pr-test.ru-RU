---
title: "aaaReplicate виртуальных машин Hyper-V в VMM облаков tooAzure с Azure Site Recovery | Документы Microsoft"
description: "Общие сведения для репликации виртуальных машин Hyper-V в tooAzure облака VMM, с помощью службы Azure Site Recovery hello"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: d6f729a49cc86ea07bebc4d7266fd7b58b3998f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-site-recovery-in-hello-azure-portal"></a><span data-ttu-id="d808b-103">Реплицировать виртуальные машины Hyper-V в tooAzure облака VMM, использование в hello портала Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="d808b-103">Replicate Hyper-V virtual machines in VMM clouds tooAzure using Site Recovery in hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d808b-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="d808b-104">Azure portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="d808b-105">Классическая модель Azure</span><span class="sxs-lookup"><span data-stu-id="d808b-105">Azure classic</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="d808b-106">PowerShell — Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d808b-106">PowerShell Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="d808b-107">PowerShell — классическая модель</span><span class="sxs-lookup"><span data-stu-id="d808b-107">PowerShell classic</span></span>](site-recovery-deploy-with-powershell.md)


<span data-ttu-id="d808b-108">В этой статье приведены общие сведения о необходимых tooreplicate действия hello в локальной среде Hyper-V виртуальных машин (ВМ), управляемых в tooAzure облаках диспетчера виртуальных машин System Center (VMM), с помощью hello [Azure Site Recovery](site-recovery-overview.md) в Здравствуйте, портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d808b-108">This article provides an overview of hello steps required tooreplicate on-premises Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="d808b-109">После считывания в этой статье, отправлять любые комментарии, внизу hello, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="d808b-109">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-hello-scenario-architecture"></a><span data-ttu-id="d808b-110">Шаг 1: Просмотрите архитектура сценария hello</span><span class="sxs-lookup"><span data-stu-id="d808b-110">Step 1: Review hello scenario architecture</span></span>

<span data-ttu-id="d808b-111">Прежде чем начать развертывание, просмотрите hello архитектура сценария и убедитесь, что вы понимаете все компоненты hello необходим toodeploy.</span><span class="sxs-lookup"><span data-stu-id="d808b-111">Before you start deployment, review hello scenario architecture, and make sure that you understand all hello components you need toodeploy.</span></span>

<span data-ttu-id="d808b-112">Go слишком[шаг 1: обзор архитектуры hello](vmm-to-azure-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="d808b-112">Go too[Step 1: Review hello architecture](vmm-to-azure-walkthrough-architecture.md)</span></span>

## <a name="step-2-review-prerequisites-and-limitations"></a><span data-ttu-id="d808b-113">Шаг 2. Просмотр предварительных условий и ограничений</span><span class="sxs-lookup"><span data-stu-id="d808b-113">Step 2: Review prerequisites and limitations</span></span>

<span data-ttu-id="d808b-114">Убедитесь, что вы понимаете предварительные условия для развертывания hello и ограничения.</span><span class="sxs-lookup"><span data-stu-id="d808b-114">Make sure that you understand hello deployment prerequisites and limitations.</span></span>

<span data-ttu-id="d808b-115">**Предварительные требования Azure**: учетная запись Microsoft Azure, сети Azure и учетные записи хранения.</span><span class="sxs-lookup"><span data-stu-id="d808b-115">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
<span data-ttu-id="d808b-116">**Локальные серверы VMM и узлы Hyper-V.** Убедитесь, что серверы VMM и узлы Hyper-V совместимы и подготовлены к развертыванию Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="d808b-116">**On-premises VMM servers and Hyper-V hosts**: Make sure that VMM servers and Hyper-V hosts are compliant and prepared for Site Recovery deployment.</span></span>
<span data-ttu-id="d808b-117">**Репликация виртуальных машин**: Убедитесь, что требуется tooreplicate виртуальные машины соответствуют требованиям Azure.</span><span class="sxs-lookup"><span data-stu-id="d808b-117">**Replicated VMs**: Check that VMs you want tooreplicate comply with Azure requirements.</span></span>

<span data-ttu-id="d808b-118">Go слишком[шаг 2: Проверьте предварительные условия и ограничения](vmm-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="d808b-118">Go too[Step 2: Verify prerequisites and limitations](vmm-to-azure-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="d808b-119">Шаг 3. Планирование ресурсов</span><span class="sxs-lookup"><span data-stu-id="d808b-119">Step 3: Plan capacity</span></span>

<span data-ttu-id="d808b-120">При выполнении полного развертывания, необходимо toofigure какие ресурсы репликации необходимо.</span><span class="sxs-lookup"><span data-stu-id="d808b-120">If you're doing a full deployment, you need toofigure out what replication resources you need.</span></span> <span data-ttu-id="d808b-121">Существует несколько из доступных toohelp средства это сделать.</span><span class="sxs-lookup"><span data-stu-id="d808b-121">There are a couple of tools available toohelp you do this.</span></span> <span data-ttu-id="d808b-122">Если вы выполняете быстро настроить среду tootest hello, этот шаг можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="d808b-122">If you're doing a quick set up tootest hello environment, you can skip this step.</span></span>

<span data-ttu-id="d808b-123">Go слишком[Step 3: Планирование емкости](vmm-to-azure-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="d808b-123">Go too[Step 3: Plan capacity](vmm-to-azure-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="d808b-124">Шаг 4. Планирование сетей</span><span class="sxs-lookup"><span data-stu-id="d808b-124">Step 4: Plan networking</span></span>

<span data-ttu-id="d808b-125">Необходимо toodo какой-либо сети, планирование tooensure, можно настроить сетевое сопоставление, при развертывании hello сценарий, что виртуальные машины Azure будут tooAzure подключенных виртуальных сетей, после отработки отказа, и, что они назначены соответствующие IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="d808b-125">You need toodo some network planning tooensure that you can configure network mapping when you deploy hello scenario, that Azure VMs will be connected tooAzure virtual networks after failover occurs, and that that they're assigned appropriate IP addresses.</span></span>

<span data-ttu-id="d808b-126">Go слишком[шаг 4: Планирование сети](vmm-to-azure-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="d808b-126">Go too[Step 4: Plan networking](vmm-to-azure-walkthrough-network.md)</span></span>


## <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="d808b-127">Шаг 5. Подготовка ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="d808b-127">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="d808b-128">Настройте учетную запись, сети и хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="d808b-128">Set up an Azure account, networks, and storage.</span></span> <span data-ttu-id="d808b-129">Это можно сделать при развертывании, но мы рекомендуем это сделать до начала процесса.</span><span class="sxs-lookup"><span data-stu-id="d808b-129">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="d808b-130">Go слишком[шаг 5: Подготовка Azure](vmm-to-azure-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="d808b-130">Go too[Step 5: Prepare Azure](vmm-to-azure-walkthrough-prepare-azure.md)</span></span>

## <a name="step-6-prepare-vmm-and-hyper-v"></a><span data-ttu-id="d808b-131">Шаг 6. Подготовка VMM и Hyper-V</span><span class="sxs-lookup"><span data-stu-id="d808b-131">Step 6: Prepare VMM and Hyper-V</span></span>

<span data-ttu-id="d808b-132">Подготовка серверов VMM в локальной среде hello и узлов Hyper-V для развертывания службы восстановления сайтов.</span><span class="sxs-lookup"><span data-stu-id="d808b-132">Prepare hello on-premises VMM servers and Hyper-V hosts for Site Recovery deployment.</span></span>

<span data-ttu-id="d808b-133">Go слишком[шаг 6: Подготовка локальных серверов](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="d808b-133">Go too[Step 6: Prepare on-premises servers](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="d808b-134">Шаг 7. Настройка хранилища</span><span class="sxs-lookup"><span data-stu-id="d808b-134">Step 7: Set up a vault</span></span>

<span data-ttu-id="d808b-135">Настройте хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="d808b-135">Set up a Recovery Services vault.</span></span> <span data-ttu-id="d808b-136">хранилище Hello содержит параметры конфигурации и управляет репликации.</span><span class="sxs-lookup"><span data-stu-id="d808b-136">hello vault contains configuration settings, and orchestrates replication.</span></span>

[<span data-ttu-id="d808b-137">Шаг 7. Настройка хранилища для репликации Hyper-V</span><span class="sxs-lookup"><span data-stu-id="d808b-137">Step 7: Set up a vault</span></span>](vmm-to-azure-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="d808b-138">Шаг 8. Настройка параметров исходной и целевой среды</span><span class="sxs-lookup"><span data-stu-id="d808b-138">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="d808b-139">Настройка hello исходное и конечное расположение репликации.</span><span class="sxs-lookup"><span data-stu-id="d808b-139">Set up hello source and target replication locations.</span></span> <span data-ttu-id="d808b-140">Добавьте хранилище toohello сервера VMM hello и загружать файлы установки hello для компонентов Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="d808b-140">Add hello VMM server toohello vault, and download hello installation files for Site Recovery components.</span></span> <span data-ttu-id="d808b-141">Запустите программу установки поставщика Azure Site Recovery на сервере VMM hello.</span><span class="sxs-lookup"><span data-stu-id="d808b-141">Run Azure Site Recovery Provider setup on hello VMM server.</span></span> <span data-ttu-id="d808b-142">Программа установки устанавливает hello поставщика на сервере VMM hello и регистрирует hello сервер в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="d808b-142">Setup installs hello Provider on hello VMM server, and registers hello server in hello vault.</span></span> <span data-ttu-id="d808b-143">Установка агента служб восстановления Microsoft hello на каждом узле Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="d808b-143">You install hello Microsoft Recovery Services agent on each Hyper-V host.</span></span>

<span data-ttu-id="d808b-144">Go слишком[Step 8: исходный и целевой настройки](vmm-to-azure-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="d808b-144">Go too[Step 8: Configure source and target settings](vmm-to-azure-walkthrough-source-target.md)</span></span>

## <a name="step-9-configure-network-mapping"></a><span data-ttu-id="d808b-145">Шаг 9. Настройка сетевого сопоставления</span><span class="sxs-lookup"><span data-stu-id="d808b-145">Step 9: Configure network mapping</span></span>

<span data-ttu-id="d808b-146">Карта локальной виртуальной Машины VMM сетей tooAzure виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="d808b-146">Map on-premises VMM VM networks tooAzure virtual networks.</span></span> <span data-ttu-id="d808b-147">После отработки отказа виртуальные машины Azure создаются в hello сеть Azure, которая сопоставляет ВМ toohello локальную сеть, в которой hello находится источник Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="d808b-147">After failover, Azure VMs are created in hello Azure network that maps toohello on-premises VM network in which hello source Hyper-V is located.</span></span>

<span data-ttu-id="d808b-148">Go слишком[шаг 9: настройте сетевое сопоставление](vmm-to-azure-walkthrough-network-mapping.md)</span><span class="sxs-lookup"><span data-stu-id="d808b-148">Go too[Step 9: Configure network mapping](vmm-to-azure-walkthrough-network-mapping.md)</span></span>


## <a name="step-10-set-up-a-replication-policy"></a><span data-ttu-id="d808b-149">Шаг 10. Настройка политики репликации</span><span class="sxs-lookup"><span data-stu-id="d808b-149">Step 10: Set up a replication policy</span></span>

<span data-ttu-id="d808b-150">Укажите, как локальные виртуальные машины будут реплицированных tooAzure.</span><span class="sxs-lookup"><span data-stu-id="d808b-150">Specify how on-premises VMs will be replicated tooAzure.</span></span>

<span data-ttu-id="d808b-151">Go слишком[шаг 10: настроить политику репликации](vmm-to-azure-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="d808b-151">Go too[Step 10: Set up a replication policy](vmm-to-azure-walkthrough-replication.md)</span></span>


## <a name="step-11-enable-replication-for-vms"></a><span data-ttu-id="d808b-152">Шаг 11. Включение репликации для виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="d808b-152">Step 11: Enable replication for VMs</span></span>

<span data-ttu-id="d808b-153">Выберите виртуальные машины hello требуется tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="d808b-153">Select hello VMs you want tooreplicate.</span></span> <span data-ttu-id="d808b-154">Включение виртуальной Машины для tooAzure начальной репликации hello триггеры репликации, за которым следует текущих разностной репликации.</span><span class="sxs-lookup"><span data-stu-id="d808b-154">ENabling a VM for replication triggers hello initial replication tooAzure, followed by ongoing delta replication.</span></span>

<span data-ttu-id="d808b-155">Go слишком[шаг 11: включение репликации](vmm-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="d808b-155">Go too[Step 11: Enable replication](vmm-to-azure-walkthrough-enable-replication.md)</span></span>


## <a name="step-12-run-a-test-failover"></a><span data-ttu-id="d808b-156">Шаг 12. Запуск тестовой отработки отказа</span><span class="sxs-lookup"><span data-stu-id="d808b-156">Step 12: Run a test failover</span></span>

<span data-ttu-id="d808b-157">Выполните тест отработки отказа toomake, убедиться, что все работает должным образом.</span><span class="sxs-lookup"><span data-stu-id="d808b-157">Run a test failover toomake sure everything's working as expected.</span></span>

<span data-ttu-id="d808b-158">Go слишком[шаг 12: запустите тестовую отработку отказа](vmm-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="d808b-158">Go too[Step 12: Run a test failover](vmm-to-azure-walkthrough-test-failover.md)</span></span>


