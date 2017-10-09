---
title: "aaaReplicate виртуальных машинах Azure между регионами Azure | Документы Microsoft"
description: "Обобщает hello действия требуется tooreplicate виртуальных машинах Azure между регионами Azure со службой Azure Site Recovery hello в hello портал Azure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 6dd36239-4363-4538-bf80-a18e71b8ec67
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: f4ac386f040945131f8a10f02143437f4441e298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a><span data-ttu-id="a1876-103">Репликация виртуальных машин Azure между регионами с помощью Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="a1876-103">Replicate Azure VMs between regions with Azure Site Recovery</span></span>

><span data-ttu-id="a1876-104">В этой статье Обзор tooreplicate необходимые шаги hello Azure виртуальных машин (ВМ) в tooAzure одного региона Azure виртуальные машины в другом регионе.</span><span class="sxs-lookup"><span data-stu-id="a1876-104">This article provides an overview of hello steps required tooreplicate Azure virtual machines (VMs) in one Azure region tooAzure VMs in a different region.</span></span> 

>[!NOTE]
>
> <span data-ttu-id="a1876-105">Репликация виртуальных машин Azure сейчас доступна в режиме предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="a1876-105">Azure VM replication is currently in preview.</span></span>

<span data-ttu-id="a1876-106">Учет комментарии и вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="a1876-106">Post comments and questions at hello bottom of this article or on hello [Azure Recovery Services forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="step-1-review-architecture"></a><span data-ttu-id="a1876-107">Шаг 1. Общие сведения об архитектуре</span><span class="sxs-lookup"><span data-stu-id="a1876-107">Step 1: Review architecture</span></span>

<span data-ttu-id="a1876-108">Перед началом развертывания ознакомьтесь архитектура сценария hello и hello компоненты, необходимые toodeploy.</span><span class="sxs-lookup"><span data-stu-id="a1876-108">Before you start deployment, review hello scenario architecture, and hello components you need toodeploy.</span></span>

<span data-ttu-id="a1876-109">Go слишком[шаг 1: обзор архитектуры hello](azure-to-azure-walkthrough-architecture.md)</span><span class="sxs-lookup"><span data-stu-id="a1876-109">Go too[Step 1: Review hello architecture](azure-to-azure-walkthrough-architecture.md)</span></span>


## <a name="step-2-review-prerequisites"></a><span data-ttu-id="a1876-110">Шаг 2. Проверка предварительных требований</span><span class="sxs-lookup"><span data-stu-id="a1876-110">Step 2: Review prerequisites</span></span>

<span data-ttu-id="a1876-111">Проверьте, что у hello Azure необходимые компоненты в местах, включая подписки, виртуальных сетей, учетные записи хранения и требования виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a1876-111">Check that you have hello Azure prerequisites in places, including a subscription, virtual networks, storage accounts, and VM requirements.</span></span>

<span data-ttu-id="a1876-112">Go слишком[шаг 2: Проверьте предварительные условия и ограничения](azure-to-azure-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="a1876-112">Go too[Step 2: Verify prerequisites and limitations](azure-to-azure-walkthrough-prerequisites.md)</span></span>


## <a name="step-3-plan-networking"></a><span data-ttu-id="a1876-113">Шаг 3. Планирование сетей</span><span class="sxs-lookup"><span data-stu-id="a1876-113">Step 3: Plan networking</span></span>

<span data-ttu-id="a1876-114">Проверьте, что исходящие подключения настроены на виртуальных машинах Azure, требуется tooreplicate и подключения из локального настраиваются.</span><span class="sxs-lookup"><span data-stu-id="a1876-114">Check that outbound connectivity is set up on Azure VMs you want tooreplicate, and that connections from on-premises are set up.</span></span>

<span data-ttu-id="a1876-115">Go слишком[шаг 4: Планирование сети](azure-to-azure-walkthrough-network.md)</span><span class="sxs-lookup"><span data-stu-id="a1876-115">Go too[Step 4: Plan networking](azure-to-azure-walkthrough-network.md)</span></span>



## <a name="step-4-create-a-vault"></a><span data-ttu-id="a1876-116">Шаг 4. Создание хранилища</span><span class="sxs-lookup"><span data-stu-id="a1876-116">Step 4: Create a vault</span></span> 

<span data-ttu-id="a1876-117">Требуется tooset копирование tooorchestrate хранилище служб восстановления и управление репликацией и укажите регион источника hello.</span><span class="sxs-lookup"><span data-stu-id="a1876-117">You need tooset up a Recovery Services vault tooorchestrate and manage replication, and specify hello source region.</span></span>

<span data-ttu-id="a1876-118">Go слишком[шаг 4: Создание хранилища](azure-to-azure-walkthrough-vault.md)</span><span class="sxs-lookup"><span data-stu-id="a1876-118">Go too[Step 4: Create a vault](azure-to-azure-walkthrough-vault.md)</span></span>


## <a name="step-5-enable-replication"></a><span data-ttu-id="a1876-119">Шаг 5. Включение репликации</span><span class="sxs-lookup"><span data-stu-id="a1876-119">Step 5: Enable replication</span></span>


<span data-ttu-id="a1876-120">репликация tooenable, настройте параметры целевого расположения, настройте политику репликации и выберите hello виртуальных машинах Azure, которые должны tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="a1876-120">tooenable replication, you configure target location settings, set up a replication policy, and select hello Azure VMs that you want tooreplicate.</span></span> <span data-ttu-id="a1876-121">После включения, происходит начальной репликации hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a1876-121">After enabling, initial replication of hello VM occurs.</span></span>

<span data-ttu-id="a1876-122">Go слишком[шаг 5: включение репликации](azure-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="a1876-122">Go too[Step 5: Enable replication](azure-to-azure-walkthrough-enable-replication.md)</span></span>


## <a name="step-6-run-a-test-failover"></a><span data-ttu-id="a1876-123">Шаг 6. Выполнение тестовой отработки отказа</span><span class="sxs-lookup"><span data-stu-id="a1876-123">Step 6: Run a test failover</span></span>

<span data-ttu-id="a1876-124">После завершения первоначальной репликации, а разностная репликация выполняется, можно запустить тест отработки отказа toomake, убедиться, что все работает правильно.</span><span class="sxs-lookup"><span data-stu-id="a1876-124">After initial replication finishes, and delta replication is running, you can run a test failover toomake sure everything works as expected.</span></span>

<span data-ttu-id="a1876-125">Go слишком[шаг 6: запустите тестовую отработку отказа](azure-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="a1876-125">Go too[Step 6: Run a test failover](azure-to-azure-walkthrough-test-failover.md)</span></span>


