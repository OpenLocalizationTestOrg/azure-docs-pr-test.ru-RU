---
title: "aaaSet политику репликации для виртуальной Машины VMware tooAzure репликации с помощью Azure Site Recovery | Документы Microsoft"
description: "Собраны действия hello потребуется tooset политику репликации при репликации виртуальных машин VMware tooAzure хранилища"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d7874bd8-6626-4668-9ec9-dbd2d26f8f81
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 12870f3f98a4dd412221b817581403cd4bf7a76d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-set-up-a-replication-policy-for-vmware-vm-replication-tooazure"></a><span data-ttu-id="1287d-103">Шаг 9: Настройка политики репликации для виртуальной Машины VMware tooAzure репликации</span><span class="sxs-lookup"><span data-stu-id="1287d-103">Step 9: Set up a replication policy for VMware VM replication tooAzure</span></span>


<span data-ttu-id="1287d-104">В этой статье описывается как tooset политику репликации при репликации с помощью hello tooAzure виртуальных машин VMware [Azure Site Recovery](site-recovery-overview.md) в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="1287d-104">This article describes how tooset up a replication policy when you're replicating VMware VMs tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="1287d-105">Учет комментарии и вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="1287d-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="configure-a-policy"></a><span data-ttu-id="1287d-106">Настройка политики</span><span class="sxs-lookup"><span data-stu-id="1287d-106">Configure a policy</span></span>

<span data-ttu-id="1287d-107">Перед началом посмотрите краткий видеообзор:</span><span class="sxs-lookup"><span data-stu-id="1287d-107">Get a quick video overview before you start:</span></span>
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. <span data-ttu-id="1287d-108">Щелкните toocreate новую политику репликации **инфраструктура Site Recovery** > **политики репликации** > **+ политику репликации**.</span><span class="sxs-lookup"><span data-stu-id="1287d-108">toocreate a new replication policy, click **Site Recovery infrastructure** > **Replication Policies** > **+Replication Policy**.</span></span>
2. <span data-ttu-id="1287d-109">На странице **Создать политику репликации** укажите имя политики.</span><span class="sxs-lookup"><span data-stu-id="1287d-109">In **Create replication policy**, specify a policy name.</span></span>
3. <span data-ttu-id="1287d-110">В **пороговое значение RPO**, ограничить количество RPO hello.</span><span class="sxs-lookup"><span data-stu-id="1287d-110">In **RPO threshold**, specify hello RPO limit.</span></span> <span data-ttu-id="1287d-111">Это значение указывает, как часто создаются точки восстановления данных.</span><span class="sxs-lookup"><span data-stu-id="1287d-111">This value specifies how often data recovery points are created.</span></span> <span data-ttu-id="1287d-112">Если непрерывная репликация превышает это значение, выдаются оповещения.</span><span class="sxs-lookup"><span data-stu-id="1287d-112">An alert is generated if continuous replication exceeds this limit.</span></span>
4. <span data-ttu-id="1287d-113">В **хранения точки восстановления**, укажите длительность (в часах) является окном приветствия хранения для каждой точки восстановления.</span><span class="sxs-lookup"><span data-stu-id="1287d-113">In **Recovery point retention**, specify (in hours) how long hello retention window is for each recovery point.</span></span> <span data-ttu-id="1287d-114">Реплицированные виртуальные машины могут быть восстановлены tooany точки в окне.</span><span class="sxs-lookup"><span data-stu-id="1287d-114">Replicated VMs can be recovered tooany point in a window.</span></span> <span data-ttu-id="1287d-115">Копирование too24 часов хранения поддерживается для машин реплицируются toopremium хранилища и 72 часа для стандартного хранилища.</span><span class="sxs-lookup"><span data-stu-id="1287d-115">Up too24 hours retention is supported for machines replicated toopremium storage, and 72 hours for standard storage.</span></span>
5. <span data-ttu-id="1287d-116">В поле **Периодичность создания моментальных снимков с согласованием приложений**укажите, с какой периодичностью (в минутах) будут создаваться точки восстановления, содержащие моментальные снимки, согласованные на уровне приложений.</span><span class="sxs-lookup"><span data-stu-id="1287d-116">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="1287d-117">Нажмите кнопку **ОК** toocreate hello политики.</span><span class="sxs-lookup"><span data-stu-id="1287d-117">Click **OK** toocreate hello policy.</span></span>

    ![Политика репликации](./media/vmware-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="1287d-119">При создании новой политики она автоматически связывается с сервера конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="1287d-119">When you create a new policy it's automatically associated with hello configuration server.</span></span> <span data-ttu-id="1287d-120">Для восстановления размещения по умолчанию автоматически создается соответствующая политика.</span><span class="sxs-lookup"><span data-stu-id="1287d-120">By default, a matching policy is automatically created for failback.</span></span> <span data-ttu-id="1287d-121">Например, если hello политика репликации — **политики rep** политика восстановления размещения hello будет **rep политика восстановления размещения**.</span><span class="sxs-lookup"><span data-stu-id="1287d-121">For example, if hello replication policy is **rep-policy** then hello failback policy will be **rep-policy-failback**.</span></span> <span data-ttu-id="1287d-122">Эта политика не используется, пока не будет запущено восстановление размещения из Azure.</span><span class="sxs-lookup"><span data-stu-id="1287d-122">This policy isn't used until you initiate a failback from Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1287d-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1287d-123">Next steps</span></span>

<span data-ttu-id="1287d-124">Go слишком[шаг 10: Установка службы Mobility hello](vmware-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="1287d-124">Go too[Step 10: Install hello Mobility service](vmware-walkthrough-install-mobility.md)</span></span>
