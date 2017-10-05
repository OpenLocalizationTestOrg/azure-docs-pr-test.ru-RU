---
title: "Репликация локальных физических серверов в Azure с помощью службы Azure Site Recovery | Документация Майкрософт"
description: "В этой статье описаны действия, необходимые для репликации рабочих нагрузок, выполняющихся на локальных физических серверах Windows или Linux, в Azure с помощью службы Azure Site Recovery."
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
ms.openlocfilehash: 0a09b35e98dc0b2f5283c2a707a3a2b8ac9a39f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-physical-servers-to-azure-with-site-recovery"></a><span data-ttu-id="85a5e-103">Репликация физических серверов в Azure с помощью Site Recovery</span><span class="sxs-lookup"><span data-stu-id="85a5e-103">Replicate physical servers to Azure with Site Recovery</span></span>

<span data-ttu-id="85a5e-104">В этой статье описаны действия для репликации локальных физических серверов Windows или Linux в Azure с помощью службы [Azure Site Recovery](site-recovery-overview.md) на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="85a5e-104">This article provides an overview of the steps required to replicate on-premises Windows/Linux physical servers to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


## <a name="step-1-review-architecture-and-prerequisites"></a><span data-ttu-id="85a5e-105">Шаг 1. Проверка архитектуры и предварительных требований</span><span class="sxs-lookup"><span data-stu-id="85a5e-105">Step 1: Review architecture and prerequisites</span></span>

<span data-ttu-id="85a5e-106">Перед началом развертывания ознакомьтесь с архитектурой сценария и убедитесь, что вам знакомы все компоненты, которые необходимы для настройки развертывания.</span><span class="sxs-lookup"><span data-stu-id="85a5e-106">Before you start deployment, review the scenario architecture, and make sure you understand all the components you need to set up the deployment.</span></span>

<span data-ttu-id="85a5e-107">Перейдите к статье [Шаг 1. Обзор архитектуры репликации физического сервера в Azure](physical-walkthrough-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="85a5e-107">Go to [Step 1: Review the architecture](physical-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="85a5e-108">Шаг 2. Проверка предварительных требований</span><span class="sxs-lookup"><span data-stu-id="85a5e-108">Step 2: Review prerequisites</span></span>

<span data-ttu-id="85a5e-109">Убедитесь, что предварительные требования выполняются для каждого компонента развертывания.</span><span class="sxs-lookup"><span data-stu-id="85a5e-109">Make sure you have the prerequisites in place for each deployment component:</span></span>

- <span data-ttu-id="85a5e-110">**Предварительные требования Azure**: учетная запись Microsoft Azure, сети Azure и учетные записи хранения.</span><span class="sxs-lookup"><span data-stu-id="85a5e-110">**Azure prerequisites**: You need a Microsoft Azure account, Azure networks, and storage accounts.</span></span>
- <span data-ttu-id="85a5e-111">**Локальные компоненты Site Recovery**: компьютер, на котором запущены локальные компоненты Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="85a5e-111">**On-premises Site Recovery components**: You need a machine running on-premises Site Recovery components.</span></span>
- <span data-ttu-id="85a5e-112">**Реплицируемые компьютеры**: реплицируемые серверы, соответствующие требованиям локальных компонентов и Azure.</span><span class="sxs-lookup"><span data-stu-id="85a5e-112">**Replicated machines**: Servers you want to replicate need to comply with on-premises and Azure requirements.</span></span>

<span data-ttu-id="85a5e-113">Перейдите к статье [Шаг 2. Просмотр предварительных требований для репликации физического сервера в Azure](physical-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="85a5e-113">Go to [Step 2: Review prerequisites and limitations](physical-walkthrough-prerequisites.md)</span></span>

## <a name="step-3-plan-capacity"></a><span data-ttu-id="85a5e-114">Шаг 3. Планирование ресурсов</span><span class="sxs-lookup"><span data-stu-id="85a5e-114">Step 3: Plan capacity</span></span>

<span data-ttu-id="85a5e-115">При выполнении полного развертывания необходимо выяснить, какие ресурсы требуются для репликации.</span><span class="sxs-lookup"><span data-stu-id="85a5e-115">If you're doing a full deployment you need to figure out what replication resources you need.</span></span> <span data-ttu-id="85a5e-116">Если выполняется быстрая настройка для тестирования среды, то этот шаг можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="85a5e-116">If you're doing a quick set up to test the environment, you can skip this step.</span></span>

<span data-ttu-id="85a5e-117">Перейдите к статье [Шаг 3. Планирование ресурсов и масштабирования для репликации физического сервера в Azure](physical-walkthrough-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="85a5e-117">Go to [Step 3: Plan capacity](physical-walkthrough-capacity.md)</span></span>

## <a name="step-4-plan-networking"></a><span data-ttu-id="85a5e-118">Шаг 4. Планирование сетей</span><span class="sxs-lookup"><span data-stu-id="85a5e-118">Step 4: Plan networking</span></span>

<span data-ttu-id="85a5e-119">Необходимо выполнить определенное планирование сетей, чтобы обеспечить подключение виртуальных машин Azure к сетям после отработки отказа и правильность их IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="85a5e-119">You need to do some network planning to ensure that Azure VMs are connected to networks after failover occurs, and  that that they have the right IP addresses.</span></span>

<span data-ttu-id="85a5e-120">Перейдите к статье [Шаг 4. Планирование сетей для репликации физического сервера в Azure](physical-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="85a5e-120">Go to [Step 4: Plan networking](physical-walkthrough-network.md)</span></span>

##  <a name="step-5-prepare-azure-resources"></a><span data-ttu-id="85a5e-121">Шаг 5. Подготовка ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="85a5e-121">Step 5: Prepare Azure resources</span></span>

<span data-ttu-id="85a5e-122">Прежде чем начать, настройте сети и хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="85a5e-122">Set up Azure networks and storage before you start.</span></span> 

<span data-ttu-id="85a5e-123">Перейдите к статье [Шаг 5. Подготовка ресурсов Azure для репликации Hyper-V в Azure](physical-walkthrough-prepare-azure.md).</span><span class="sxs-lookup"><span data-stu-id="85a5e-123">Go to [Step 5: Prepare Azure](physical-walkthrough-prepare-azure.md)</span></span>


## <a name="step-6-set-up-a-vault"></a><span data-ttu-id="85a5e-124">Шаг 6. Настройка хранилища</span><span class="sxs-lookup"><span data-stu-id="85a5e-124">Step 6: Set up a vault</span></span>

<span data-ttu-id="85a5e-125">Для координации процесса репликации и управления им необходимо настроить хранилище Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="85a5e-125">You set up a Recovery Services vault to orchestrate and manage replication.</span></span> <span data-ttu-id="85a5e-126">При настройке хранилища укажите целевые объекты и место для репликации.</span><span class="sxs-lookup"><span data-stu-id="85a5e-126">When you set up the vault, you specify what you want to replicate, and where you want to replicate it to.</span></span>

<span data-ttu-id="85a5e-127">Перейдите к статье [Step 6: Set up a vault for physical server replication to Azure](physical-walkthrough-create-vault.md) (Шаг 6. Настройка хранилища для репликации физического сервера в Azure).</span><span class="sxs-lookup"><span data-stu-id="85a5e-127">Go to [Step 6: Set up a vault](physical-walkthrough-create-vault.md)</span></span>

## <a name="step-7-configure-source-and-target-settings"></a><span data-ttu-id="85a5e-128">Шаг 7. Настройка параметров исходной и целевой среды</span><span class="sxs-lookup"><span data-stu-id="85a5e-128">Step 7: Configure source and target settings</span></span>

<span data-ttu-id="85a5e-129">Настройте параметры исходного и целевого (Azure) сайта.</span><span class="sxs-lookup"><span data-stu-id="85a5e-129">Configure settings for the source and target (Azure) site.</span></span> <span data-ttu-id="85a5e-130">Настройка параметров исходного сайта включает в себя выполнение единой установки для локальных компонентов Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="85a5e-130">Source settings includes running Unified Setup to install the on-premises Site Recovery components.</span></span>

<span data-ttu-id="85a5e-131">Перейдите к статье [Шаг 7. Настройка исходной и целевой среды для репликации физического сервера в Azure](physical-walkthrough-source-target.md).</span><span class="sxs-lookup"><span data-stu-id="85a5e-131">Go to [Step 7: Set up the source and target](physical-walkthrough-source-target.md)</span></span>

## <a name="step-8-set-up-a-replication-policy"></a><span data-ttu-id="85a5e-132">Шаг 8. Настройка политики репликации</span><span class="sxs-lookup"><span data-stu-id="85a5e-132">Step 8: Set up a replication policy</span></span>

<span data-ttu-id="85a5e-133">Настройте политику, чтобы указать параметры репликации физических серверов.</span><span class="sxs-lookup"><span data-stu-id="85a5e-133">You set up a policy to specify how physical servers should replicate.</span></span>

<span data-ttu-id="85a5e-134">Перейдите к разделу [Шаг 8. Настройка политики репликации для репликации физического сервера в Azure](physical-walkthrough-replication.md).</span><span class="sxs-lookup"><span data-stu-id="85a5e-134">Go to [Step 8: Set up a replication policy](physical-walkthrough-replication.md)</span></span>

## <a name="step-9-install-the-mobility-service"></a><span data-ttu-id="85a5e-135">Шаг 9. Установка службы Mobility Service</span><span class="sxs-lookup"><span data-stu-id="85a5e-135">Step 9: Install the Mobility service</span></span>

<span data-ttu-id="85a5e-136">Служба Mobility Service должна быть установлена на каждом сервере, который нужно реплицировать.</span><span class="sxs-lookup"><span data-stu-id="85a5e-136">The Mobility service must be installed on each server you want to replicate.</span></span> <span data-ttu-id="85a5e-137">Существует несколько способов настройки этой службы с помощью принудительной установки или установки по запросу.</span><span class="sxs-lookup"><span data-stu-id="85a5e-137">There are a few ways to set up the service, with push or pull installation.</span></span>

<span data-ttu-id="85a5e-138">Перейдите к разделу [Step 9: Install the Mobility service](physical-walkthrough-install-mobility.md) (Шаг 9. Установка службы Mobility Service).</span><span class="sxs-lookup"><span data-stu-id="85a5e-138">Go to [Step 9: Install the Mobility service](physical-walkthrough-install-mobility.md)</span></span>

## <a name="step-10-enable-replication"></a><span data-ttu-id="85a5e-139">Шаг 10. Включение репликации</span><span class="sxs-lookup"><span data-stu-id="85a5e-139">Step 10: Enable replication</span></span>

<span data-ttu-id="85a5e-140">После запуска службы Mobility Service на сервере можно включить для нее репликацию.</span><span class="sxs-lookup"><span data-stu-id="85a5e-140">After the Mobility service is running on a server, you can enable replication for it.</span></span> <span data-ttu-id="85a5e-141">После включения выполняется начальная репликация виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="85a5e-141">After enabling, initial replication of the VM occurs.</span></span>

<span data-ttu-id="85a5e-142">Перейдите к статье [Шаг 10. Включение репликации для физических серверов в Azure](physical-walkthrough-enable-replication.md).</span><span class="sxs-lookup"><span data-stu-id="85a5e-142">Go to [Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>

## <a name="step-11-run-a-test-failover"></a><span data-ttu-id="85a5e-143">Шаг 11. Запуск тестовой отработки отказа</span><span class="sxs-lookup"><span data-stu-id="85a5e-143">Step 11: Run a test failover</span></span>

<span data-ttu-id="85a5e-144">После завершения начальной репликации и запуска репликации разностных изменений можно выполнить тестовую отработку отказа, чтобы убедиться, что все работает правильно.</span><span class="sxs-lookup"><span data-stu-id="85a5e-144">After initial replication finishes and delta replication is running, you can run a test failover to make sure everything works as expected.</span></span>

<span data-ttu-id="85a5e-145">Перейдите к статье [Шаг 11: Запуск тестовой отработки отказа физических серверов в Azure](physical-walkthrough-test-failover.md).</span><span class="sxs-lookup"><span data-stu-id="85a5e-145">Go to [Step 11: Run a test failover](physical-walkthrough-test-failover.md)</span></span>

