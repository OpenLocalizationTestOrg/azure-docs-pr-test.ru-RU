---
title: "Репликация виртуальных машин Hyper-V в Azure с помощью Azure Site Recovery | Документация Майкрософт"
description: "В этот статье описано, как управлять репликацией, отработкой отказа и восстановлением локальных виртуальных машин Hyper-V в Azure"
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
ms.openlocfilehash: da10b213bc2543942b5ac77cf5c5d8547c00220c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-to-azure"></a><span data-ttu-id="c9582-103">Репликация виртуальных машин Hyper-V (без VMM) в Azure</span><span class="sxs-lookup"><span data-stu-id="c9582-103">Replicate Hyper-V virtual machines (without VMM) to Azure</span></span> 

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c9582-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="c9582-104">Azure portal</span></span>](site-recovery-hyper-v-site-to-azure.md)
> * [<span data-ttu-id="c9582-105">Классическая модель Azure</span><span class="sxs-lookup"><span data-stu-id="c9582-105">Azure classic</span></span>](site-recovery-hyper-v-site-to-azure-classic.md)
> * [<span data-ttu-id="c9582-106">PowerShell — Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c9582-106">PowerShell - Resource Manager</span></span>](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

<span data-ttu-id="c9582-107">В этой статье кратко описаны шаги для репликации локальных виртуальных машин Hyper-V в Azure с помощью [Azure Site Recovery](site-recovery-overview.md) на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="c9582-107">This article provides an overview of the steps required to replicate on-premises Hyper-V virtual machines to Azure, using the [Azure Site Recovery](site-recovery-overview.md) in the Azure portal.</span></span> <span data-ttu-id="c9582-108">В этом развертывании Hyper-V виртуальные машины не передаются под управление System Center Virtual Machine Manager (VMM).</span><span class="sxs-lookup"><span data-stu-id="c9582-108">In this deployment Hyper-V VMs aren't managed by System Center Virtual Machine Manager (VMM).</span></span>


<span data-ttu-id="c9582-109">Комментарии или вопросы технического характера можно добавить в конце этой статьи или на [форуме по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="c9582-109">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="c9582-110">Шаг 1. Проверка архитектуры и предварительных требований</span><span class="sxs-lookup"><span data-stu-id="c9582-110">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="c9582-111">Перед началом развертывания ознакомьтесь с архитектурой сценария и убедитесь, что вам знакомы все компоненты, которые необходимо развернуть.</span><span class="sxs-lookup"><span data-stu-id="c9582-111">Before you start deployment, review the scenario architecture, and make sure you understand all the components you need to deploy</span></span>

<span data-ttu-id="c9582-112">Перейдите к статье [Шаг 1. Обзор архитектуры репликации физического сервера в Azure](hyper-v-site-walkthrough-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="c9582-112">Go to [Step 1: Review the architecture](hyper-v-site-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="c9582-113">Шаг 2. Проверка предварительных требований</span><span class="sxs-lookup"><span data-stu-id="c9582-113">Step 2: Review prerequisites</span></span>

<span data-ttu-id="c9582-114">Убедитесь, что предварительные требования выполняются для каждого компонента развертывания.</span><span class="sxs-lookup"><span data-stu-id="c9582-114">Make sure you have the prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="c9582-115">**Предварительные требования Azure**: учетная запись Microsoft Azure, сети Azure и учетные записи хранения.</span><span class="sxs-lookup"><span data-stu-id="c9582-115">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="c9582-116">**Предварительные требования локальной среды Hyper-V**: убедитесь, что узлы Hyper-V подготовлены к развертыванию Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="c9582-116">**On-premises Hyper-V prerequisites**: Make sure Hyper-V hosts are prepared for Site Recovery deployment.</span></span>
- <span data-ttu-id="c9582-117">**Реплицированные виртуальные машины**: виртуальные машины, которые требуется реплицировать, должны соответствовать требованиям Azure.</span><span class="sxs-lookup"><span data-stu-id="c9582-117">**Replicated VMs**: VMs you want to replicate need to comply with Azure requirements.</span></span>

<span data-ttu-id="c9582-118">Перейдите к разделу [Шаг 2. Проверка предварительных требований для репликации из VMware в Azure](hyper-v-site-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="c9582-118">Go to [Step 2: Verify prerequisites and limitations](hyper-v-site-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="c9582-119">Шаг 3. Планирование ресурсов</span><span class="sxs-lookup"><span data-stu-id="c9582-119">Step 3: Plan capacity</span></span>

<span data-ttu-id="c9582-120">При выполнении полного развертывания необходимо выяснить, какие ресурсы требуются для репликации.</span><span class="sxs-lookup"><span data-stu-id="c9582-120">If you're doing a full deployment you need to figure out what replication resources you need.</span></span> <span data-ttu-id="c9582-121">Доступно несколько инструментов, которые помогут выполнить эту задачу.</span><span class="sxs-lookup"><span data-stu-id="c9582-121">There are a couple of tools available to help you do this.</span></span> <span data-ttu-id="c9582-122">Перейдите к шагу 2.</span><span class="sxs-lookup"><span data-stu-id="c9582-122">Go to Step 2.</span></span> <span data-ttu-id="c9582-123">Если выполняется быстрая настройка для тестирования среды, то этот шаг можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="c9582-123">If you're doing a quick set up to test the environment you can skip this step.</span></span>

<span data-ttu-id="c9582-124">Перейдите к статье [Шаг 3. Планирование ресурсов и масштабирования для репликации физического сервера в Azure](hyper-v-site-walkthrough-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="c9582-124">Go to [Step 3: Plan capacity](hyper-v-site-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="c9582-125">Шаг 4. Планирование сетей</span><span class="sxs-lookup"><span data-stu-id="c9582-125">Step 4: Plan networking</span></span>

<span data-ttu-id="c9582-126">Необходимо выполнить определенное планирование сетей, чтобы обеспечить подключение виртуальных машин Azure к сетям после отработки отказа и правильность их IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="c9582-126">You need to do some network planning to ensure that Azure VMs are connected to networks after failover occurs, and  that that they have the right IP addresses.</span></span>

<span data-ttu-id="c9582-127">Перейдите к статье [Шаг 4. Планирование сетей для репликации физического сервера в Azure](hyper-v-site-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="c9582-127">Go to [Step 4: Plan networking](hyper-v-site-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="c9582-128">Шаг 5. Подготовка ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="c9582-128">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="c9582-129">Прежде чем начать, настройте сети и хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="c9582-129">Set up Azure networks and storage before you start.</span></span> <span data-ttu-id="c9582-130">Это можно сделать при развертывании, но мы рекомендуем это сделать до начала процесса.</span><span class="sxs-lookup"><span data-stu-id="c9582-130">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="c9582-131">Перейдите к статье [Шаг 5. Подготовка ресурсов Azure для репликации Hyper-V в Azure](hyper-v-site-walkthrough-prepare-azure.md).</span><span class="sxs-lookup"><span data-stu-id="c9582-131">Go to [Step 5: Prepare Azure](hyper-v-site-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-prepare-hyper-v"></a><span data-ttu-id="c9582-132">Шаг 6. Подготовка Hyper-V</span><span class="sxs-lookup"><span data-stu-id="c9582-132">Step 6: Prepare Hyper-V</span></span>

<span data-ttu-id="c9582-133">Убедитесь, что серверы Hyper-V соответствуют требованиям к развертыванию Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="c9582-133">Make sure that Hyper-V servers meet Site Recovery deployment requirements.</span></span>

<span data-ttu-id="c9582-134">Перейдите к статье [Шаг 6. Подготовка узлов Hyper-V для репликации в Azure](hyper-v-site-walkthrough-prepare-hyper-v.md).</span><span class="sxs-lookup"><span data-stu-id="c9582-134">Go to [Step 6: Prepare Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="c9582-135">Шаг 7. Настройка хранилища</span><span class="sxs-lookup"><span data-stu-id="c9582-135">Step 7: Set up a vault</span></span>

<span data-ttu-id="c9582-136">Для координации процесса репликации и управления им необходимо настроить хранилище Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="c9582-136">You need to set up a Recovery Services vault to orchestrate and manage replication.</span></span> <span data-ttu-id="c9582-137">При настройке хранилища укажите целевые объекты и место для репликации.</span><span class="sxs-lookup"><span data-stu-id="c9582-137">When you set up the vault, you specify what you want to replicate, and where you want to replicate it to.</span></span>

<span data-ttu-id="c9582-138">Перейдите к статье [Шаг 7. Настройка хранилища для репликации Hyper-V](hyper-v-site-walkthrough-create-vault.md).</span><span class="sxs-lookup"><span data-stu-id="c9582-138">Go to [Step 7: Create a vault](hyper-v-site-walkthrough-create-vault.md)</span></span>

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="c9582-139">Шаг 8. Настройка параметров исходной и целевой среды</span><span class="sxs-lookup"><span data-stu-id="c9582-139">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="c9582-140">Настройте исходную и целевую среды, которые используются для репликации.</span><span class="sxs-lookup"><span data-stu-id="c9582-140">Set up the source and target that's used for replication.</span></span> <span data-ttu-id="c9582-141">Настройка параметров исходной среды включает в себя добавление узлов Hyper-V на сайт Hyper-V, установку поставщика Site Recovery и агента служб восстановления на каждом узле Hyper-V и регистрацию сайта в хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="c9582-141">Setting up source settings includes adding Hyper-V hosts to a Hyper-V site, installing the Site Recovery Provider and Recovery Services agent on each Hyper-V host, and registering the site in the Recovery Services vault.</span></span>

<span data-ttu-id="c9582-142">Перейдите к разделу [Шаг 8. Настройка исходной и целевой среды для репликации физического сервера в Azure](hyper-v-site-walkthrough-source-target.md).</span><span class="sxs-lookup"><span data-stu-id="c9582-142">Go to [Step 8: Set up the source and target](hyper-v-site-walkthrough-source-target.md)</span></span>

## <a name="step-9-set-up-a-replication-policy"></a><span data-ttu-id="c9582-143">Шаг 9. Настройка политики репликации</span><span class="sxs-lookup"><span data-stu-id="c9582-143">Step 9: Set up a replication policy</span></span>

<span data-ttu-id="c9582-144">Настройте политику, чтобы указать параметры репликации для виртуальных машин Hyper-V в хранилище.</span><span class="sxs-lookup"><span data-stu-id="c9582-144">You set up a policy to specify replication settings for Hyper-V VMs in the vault.</span></span>

<span data-ttu-id="c9582-145">Перейдите к разделу [Шаг 9. Настройка политики репликации для репликации физического сервера в Azure](hyper-v-site-walkthrough-replication.md).</span><span class="sxs-lookup"><span data-stu-id="c9582-145">Go to [Step 9: Set up a replication policy](hyper-v-site-walkthrough-replication.md)</span></span>


## <a name="step-10-enable-replication"></a><span data-ttu-id="c9582-146">Шаг 10. Включение репликации</span><span class="sxs-lookup"><span data-stu-id="c9582-146">Step 10: Enable replication</span></span>

<span data-ttu-id="c9582-147">После настройки и включения политики репликации выполняется начальная репликация виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c9582-147">After you have a replication policy in place,  After enabling, initial replication of the VM occurs.</span></span>

<span data-ttu-id="c9582-148">Перейдите к статье [Шаг 10. Включение репликации для физических серверов в Azure](hyper-v-site-walkthrough-enable-replication.md).</span><span class="sxs-lookup"><span data-stu-id="c9582-148">Go to [Step 10: Enable replication](hyper-v-site-walkthrough-enable-replication.md)</span></span>

## <a name="step-11-run-a-test-failover"></a><span data-ttu-id="c9582-149">Шаг 11. Запуск тестовой отработки отказа</span><span class="sxs-lookup"><span data-stu-id="c9582-149">Step 11: Run a test failover</span></span>

<span data-ttu-id="c9582-150">После завершения начальной репликации и запуска репликации разностных изменений можно выполнить тестовую отработку отказа, чтобы убедиться, что все работает правильно.</span><span class="sxs-lookup"><span data-stu-id="c9582-150">After initial replication finishes, and delta replication is running, you can run a test failover to make sure everything works as expected.</span></span>

<span data-ttu-id="c9582-151">Перейдите к статье [Шаг 11: Запуск тестовой отработки отказа физических серверов в Azure](hyper-v-site-walkthrough-test-failover.md).</span><span class="sxs-lookup"><span data-stu-id="c9582-151">Go to [Step 11: Run a test failover](hyper-v-site-walkthrough-test-failover.md)</span></span>
