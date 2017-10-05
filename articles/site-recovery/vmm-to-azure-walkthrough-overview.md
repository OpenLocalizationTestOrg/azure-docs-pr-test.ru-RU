---
title: "Репликация виртуальных машин Hyper-V в облаках VMM в Azure с помощью Azure Site Recovery | Документация Майкрософт"
description: "Общие сведения о репликации виртуальных машин Hyper-V в облаках VMM в Azure с помощью службы Azure Site Recovery."
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
ms.openlocfilehash: af68d21184c137b2b0f1bb4c1afb9bf507e8332d
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/29/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-to-azure-using-site-recovery-in-the-azure-portal"></a><span data-ttu-id="be0b6-103">Репликация виртуальных машин Hyper-V из облаков VMM в Azure с помощью Site Recovery на портале Azure</span><span class="sxs-lookup"><span data-stu-id="be0b6-103">Replicate Hyper-V virtual machines in VMM clouds to Azure using Site Recovery in the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="be0b6-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="be0b6-104">Azure portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="be0b6-105">Классическая модель Azure</span><span class="sxs-lookup"><span data-stu-id="be0b6-105">Azure classic</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="be0b6-106">PowerShell — Resource Manager</span><span class="sxs-lookup"><span data-stu-id="be0b6-106">PowerShell Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="be0b6-107">PowerShell — классическая модель</span><span class="sxs-lookup"><span data-stu-id="be0b6-107">PowerShell classic</span></span>](site-recovery-deploy-with-powershell.md)


<span data-ttu-id="be0b6-108">В этой статье приведены общие сведения о действиях, необходимых для репликации локальных виртуальных машин Hyper-V, управляемых в облаках System Center Virtual Machine Manager (VMM), в Azure, с помощью службы [Azure Site Recovery](site-recovery-overview.md) на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="be0b6-108">This article provides an overview of the steps required to replicate on-premises Hyper-V virtual machines (VMs) managed in System Center Virtual Machine Manager (VMM) clouds to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="be0b6-109">Любые комментарии, которые возникнут после прочтения этой статьи, можно добавить в конце этой страницы или на [форуме по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="be0b6-109">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="step-1-review-the-scenario-architecture"></a><span data-ttu-id="be0b6-110">Шаг 1. Ознакомление с архитектурой сценария</span><span class="sxs-lookup"><span data-stu-id="be0b6-110">Step 1: Review the scenario architecture</span></span>

<span data-ttu-id="be0b6-111">Перед началом развертывания ознакомьтесь с архитектурой сценария и убедитесь, что вам знакомы все компоненты, которые необходимо развернуть.</span><span class="sxs-lookup"><span data-stu-id="be0b6-111">Before you start deployment, review the scenario architecture, and make sure that you understand all the components you need to deploy.</span></span>

<span data-ttu-id="be0b6-112">Перейдите к статье [Шаг 1. Обзор архитектуры репликации физического сервера в Azure](vmm-to-azure-walkthrough-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="be0b6-112">Go to [Step 1: Review the architecture](vmm-to-azure-walkthrough-architecture.md)</span></span>

## <a name="step-2-review-prerequisites-and-limitations"></a><span data-ttu-id="be0b6-113">Шаг 2. Просмотр предварительных условий и ограничений</span><span class="sxs-lookup"><span data-stu-id="be0b6-113">Step 2: Review prerequisites and limitations</span></span>

<span data-ttu-id="be0b6-114">Убедитесь, что вы понимаете предварительные условия и ограничения для развертывания.</span><span class="sxs-lookup"><span data-stu-id="be0b6-114">Make sure that you understand the deployment prerequisites and limitations.</span></span>

<span data-ttu-id="be0b6-115">**Предварительные требования Azure**: учетная запись Microsoft Azure, сети Azure и учетные записи хранения.</span><span class="sxs-lookup"><span data-stu-id="be0b6-115">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
<span data-ttu-id="be0b6-116">**Локальные серверы VMM и узлы Hyper-V.** Убедитесь, что серверы VMM и узлы Hyper-V совместимы и подготовлены к развертыванию Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="be0b6-116">**On-premises VMM servers and Hyper-V hosts**: Make sure that VMM servers and Hyper-V hosts are compliant and prepared for Site Recovery deployment.</span></span>
<span data-ttu-id="be0b6-117">**Реплицированные виртуальные машины.** Убедитесь, что виртуальные машины, которые требуется реплицировать, соответствуют требованиям Azure.</span><span class="sxs-lookup"><span data-stu-id="be0b6-117">**Replicated VMs**: Check that VMs you want to replicate comply with Azure requirements.</span></span>

<span data-ttu-id="be0b6-118">Перейдите к разделу [Шаг 2. Проверка предварительных требований для репликации из VMware в Azure](vmm-to-azure-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="be0b6-118">Go to [Step 2: Verify prerequisites and limitations](vmm-to-azure-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="be0b6-119">Шаг 3. Планирование ресурсов</span><span class="sxs-lookup"><span data-stu-id="be0b6-119">Step 3: Plan capacity</span></span>

<span data-ttu-id="be0b6-120">При выполнении полного развертывания необходимо выяснить, какие ресурсы требуются для репликации.</span><span class="sxs-lookup"><span data-stu-id="be0b6-120">If you're doing a full deployment, you need to figure out what replication resources you need.</span></span> <span data-ttu-id="be0b6-121">Доступно несколько инструментов, которые помогут выполнить эту задачу.</span><span class="sxs-lookup"><span data-stu-id="be0b6-121">There are a couple of tools available to help you do this.</span></span> <span data-ttu-id="be0b6-122">Если выполняется быстрая настройка для тестирования среды, то этот шаг можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="be0b6-122">If you're doing a quick set up to test the environment, you can skip this step.</span></span>

<span data-ttu-id="be0b6-123">Перейдите к статье [Шаг 3. Планирование ресурсов и масштабирования для репликации физического сервера в Azure](vmm-to-azure-walkthrough-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="be0b6-123">Go to [Step 3: Plan capacity](vmm-to-azure-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="be0b6-124">Шаг 4. Планирование сетей</span><span class="sxs-lookup"><span data-stu-id="be0b6-124">Step 4: Plan networking</span></span>

<span data-ttu-id="be0b6-125">Необходимо выполнить определенное планирование сетей, чтобы обеспечить возможность настройки сопоставления сетей при развертывании сценария, подключение виртуальных машин Azure к сетям после отработки отказа и правильность их IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="be0b6-125">You need to do some network planning to ensure that you can configure network mapping when you deploy the scenario, that Azure VMs will be connected to Azure virtual networks after failover occurs, and that that they're assigned appropriate IP addresses.</span></span>

<span data-ttu-id="be0b6-126">Перейдите к статье [Шаг 4. Планирование сетей для репликации физического сервера в Azure](vmm-to-azure-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="be0b6-126">Go to [Step 4: Plan networking](vmm-to-azure-walkthrough-network.md)</span></span>


## <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="be0b6-127">Шаг 5. Подготовка ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="be0b6-127">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="be0b6-128">Настройте учетную запись, сети и хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="be0b6-128">Set up an Azure account, networks, and storage.</span></span> <span data-ttu-id="be0b6-129">Это можно сделать при развертывании, но мы рекомендуем это сделать до начала процесса.</span><span class="sxs-lookup"><span data-stu-id="be0b6-129">You can do this during deployment, but we recommend you do this before you start.</span></span>

<span data-ttu-id="be0b6-130">Перейдите к статье [Шаг 5. Подготовка ресурсов Azure для репликации Hyper-V в Azure](vmm-to-azure-walkthrough-prepare-azure.md).</span><span class="sxs-lookup"><span data-stu-id="be0b6-130">Go to [Step 5: Prepare Azure](vmm-to-azure-walkthrough-prepare-azure.md)</span></span>

## <a name="step-6-prepare-vmm-and-hyper-v"></a><span data-ttu-id="be0b6-131">Шаг 6. Подготовка VMM и Hyper-V</span><span class="sxs-lookup"><span data-stu-id="be0b6-131">Step 6: Prepare VMM and Hyper-V</span></span>

<span data-ttu-id="be0b6-132">Подготовьте локальные серверы VMM и узлы Hyper-V к развертыванию службы Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="be0b6-132">Prepare the on-premises VMM servers and Hyper-V hosts for Site Recovery deployment.</span></span>

<span data-ttu-id="be0b6-133">Перейдите к статье [Шаг 6. Подготовка серверов VMM и узлов Hyper-V к репликации Hyper-V в Azure](vmm-to-azure-walkthrough-vmm-hyper-v.md).</span><span class="sxs-lookup"><span data-stu-id="be0b6-133">Go to [Step 6: Prepare on-premises servers](vmm-to-azure-walkthrough-vmm-hyper-v.md)</span></span>

## <a name="step-7-set-up-a-vault"></a><span data-ttu-id="be0b6-134">Шаг 7. Настройка хранилища</span><span class="sxs-lookup"><span data-stu-id="be0b6-134">Step 7: Set up a vault</span></span>

<span data-ttu-id="be0b6-135">Настройте хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="be0b6-135">Set up a Recovery Services vault.</span></span> <span data-ttu-id="be0b6-136">которое содержит параметры конфигурации и управляет репликацией.</span><span class="sxs-lookup"><span data-stu-id="be0b6-136">The vault contains configuration settings, and orchestrates replication.</span></span>

[<span data-ttu-id="be0b6-137">Шаг 7. Настройка хранилища для репликации Hyper-V</span><span class="sxs-lookup"><span data-stu-id="be0b6-137">Step 7: Set up a vault</span></span>](vmm-to-azure-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a><span data-ttu-id="be0b6-138">Шаг 8. Настройка параметров исходной и целевой среды</span><span class="sxs-lookup"><span data-stu-id="be0b6-138">Step 8: Configure source and target settings</span></span>

<span data-ttu-id="be0b6-139">Настройте исходное и целевое расположение для репликации.</span><span class="sxs-lookup"><span data-stu-id="be0b6-139">Set up the source and target replication locations.</span></span> <span data-ttu-id="be0b6-140">Добавьте сервер VMM в хранилище и скачайте файлы установки для компонентов Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="be0b6-140">Add the VMM server to the vault, and download the installation files for Site Recovery components.</span></span> <span data-ttu-id="be0b6-141">Запустите поставщик Azure Site Recovery на сервере VMM.</span><span class="sxs-lookup"><span data-stu-id="be0b6-141">Run Azure Site Recovery Provider setup on the VMM server.</span></span> <span data-ttu-id="be0b6-142">Программа установки устанавливает поставщик на сервере VMM и регистрирует сервер в хранилище.</span><span class="sxs-lookup"><span data-stu-id="be0b6-142">Setup installs the Provider on the VMM server, and registers the server in the vault.</span></span> <span data-ttu-id="be0b6-143">Установите агент служб восстановления Microsoft на каждом узле Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="be0b6-143">You install the Microsoft Recovery Services agent on each Hyper-V host.</span></span>

<span data-ttu-id="be0b6-144">Перейдите к статье [Шаг 8. Настройка исходных и целевых параметров для репликации Hyper-V (с VMM) в Azure](vmm-to-azure-walkthrough-source-target.md).</span><span class="sxs-lookup"><span data-stu-id="be0b6-144">Go to [Step 8: Configure source and target settings](vmm-to-azure-walkthrough-source-target.md)</span></span>

## <a name="step-9-configure-network-mapping"></a><span data-ttu-id="be0b6-145">Шаг 9. Настройка сетевого сопоставления</span><span class="sxs-lookup"><span data-stu-id="be0b6-145">Step 9: Configure network mapping</span></span>

<span data-ttu-id="be0b6-146">Сопоставьте локальные сети виртуальных машин VMM с виртуальными сетями Azure.</span><span class="sxs-lookup"><span data-stu-id="be0b6-146">Map on-premises VMM VM networks to Azure virtual networks.</span></span> <span data-ttu-id="be0b6-147">После отработки отказа виртуальные машины Azure создаются в сети Azure, которая сопоставляется с локальной сетью виртуальной машины, в которой находится источник Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="be0b6-147">After failover, Azure VMs are created in the Azure network that maps to the on-premises VM network in which the source Hyper-V is located.</span></span>

<span data-ttu-id="be0b6-148">Перейдите к статье [Шаг 9. Настройка сетевого сопоставления для репликации Hyper-V (с VMM) в Azure](vmm-to-azure-walkthrough-network-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="be0b6-148">Go to [Step 9: Configure network mapping](vmm-to-azure-walkthrough-network-mapping.md)</span></span>


## <a name="step-10-set-up-a-replication-policy"></a><span data-ttu-id="be0b6-149">Шаг 10. Настройка политики репликации</span><span class="sxs-lookup"><span data-stu-id="be0b6-149">Step 10: Set up a replication policy</span></span>

<span data-ttu-id="be0b6-150">Укажите, как локальные виртуальные машины будут реплицироваться в Azure.</span><span class="sxs-lookup"><span data-stu-id="be0b6-150">Specify how on-premises VMs will be replicated to Azure.</span></span>

<span data-ttu-id="be0b6-151">Перейдите к статье [Шаг 10. Настройка политики репликации для репликации виртуальной машины Hyper-V (с VMM) в Azure](vmm-to-azure-walkthrough-replication.md).</span><span class="sxs-lookup"><span data-stu-id="be0b6-151">Go to [Step 10: Set up a replication policy](vmm-to-azure-walkthrough-replication.md)</span></span>


## <a name="step-11-enable-replication-for-vms"></a><span data-ttu-id="be0b6-152">Шаг 11. Включение репликации для виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="be0b6-152">Step 11: Enable replication for VMs</span></span>

<span data-ttu-id="be0b6-153">Выберите виртуальные машины для репликации.</span><span class="sxs-lookup"><span data-stu-id="be0b6-153">Select the VMs you want to replicate.</span></span> <span data-ttu-id="be0b6-154">При включении виртуальной машины для репликации инициируется начальная репликация в Azure, после которой выполняется разностная репликация.</span><span class="sxs-lookup"><span data-stu-id="be0b6-154">ENabling a VM for replication triggers the initial replication to Azure, followed by ongoing delta replication.</span></span>

<span data-ttu-id="be0b6-155">Перейдите к разделу [Шаг 11. Включение репликации](vmm-to-azure-walkthrough-enable-replication.md).</span><span class="sxs-lookup"><span data-stu-id="be0b6-155">Go to [Step 11: Enable replication](vmm-to-azure-walkthrough-enable-replication.md)</span></span>


## <a name="step-12-run-a-test-failover"></a><span data-ttu-id="be0b6-156">Шаг 12. Запуск тестовой отработки отказа</span><span class="sxs-lookup"><span data-stu-id="be0b6-156">Step 12: Run a test failover</span></span>

<span data-ttu-id="be0b6-157">Запустите тестовую отработку отказа, чтобы убедиться в надлежащей работе всех компонентов.</span><span class="sxs-lookup"><span data-stu-id="be0b6-157">Run a test failover to make sure everything's working as expected.</span></span>

<span data-ttu-id="be0b6-158">Перейдите к разделу [Шаг 12. Запуск тестовой отработки отказа](vmm-to-azure-walkthrough-test-failover.md).</span><span class="sxs-lookup"><span data-stu-id="be0b6-158">Go to [Step 12: Run a test failover](vmm-to-azure-walkthrough-test-failover.md)</span></span>


