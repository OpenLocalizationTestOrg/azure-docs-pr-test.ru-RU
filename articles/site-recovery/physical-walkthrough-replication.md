---
title: "aaaSet политику репликации для физического сервера tooAzure репликации с помощью Azure Site Recovery | Документы Microsoft"
description: "Собраны действия hello потребуется tooset политику репликации при репликации локального хранилища tooAzure физических серверов, с помощью службы Azure Site Recovery hello"
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
ms.openlocfilehash: d6bdeeffc24ffc8eaba24311f7c76452edb65648
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-a-replication-policy-for-physical-server-replication-tooazure"></a><span data-ttu-id="f5ab1-103">Шаг 8: Настройка политики репликации для репликации tooAzure физического сервера</span><span class="sxs-lookup"><span data-stu-id="f5ab1-103">Step 8: Set up a replication policy for physical server replication tooAzure</span></span>


<span data-ttu-id="f5ab1-104">В этой статье описывается как tooset политику репликации при репликации tooAzure физических серверов Windows и Linux с помощью hello [Azure Site Recovery](site-recovery-overview.md) в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f5ab1-104">This article describes how tooset up a replication policy when you're replicating Windows/Linux physical servers tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="f5ab1-105">Учет комментарии и вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="f5ab1-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="configure-a-policy"></a><span data-ttu-id="f5ab1-106">Настройка политики</span><span class="sxs-lookup"><span data-stu-id="f5ab1-106">Configure a policy</span></span>

1. <span data-ttu-id="f5ab1-107">Щелкните **Site Recovery infrastructure** (Инфраструктура Site Recovery) > **Политики репликации** > **+Replication Policy** (+Политика репликации).</span><span class="sxs-lookup"><span data-stu-id="f5ab1-107">Click **Site Recovery infrastructure** > **Replication Policies** > **+Replication Policy**.</span></span>
2. <span data-ttu-id="f5ab1-108">На странице **Создать политику репликации** укажите имя политики.</span><span class="sxs-lookup"><span data-stu-id="f5ab1-108">In **Create replication policy**, specify a policy name.</span></span>
3. <span data-ttu-id="f5ab1-109">В **пороговое значение RPO**, ограничить количество RPO hello.</span><span class="sxs-lookup"><span data-stu-id="f5ab1-109">In **RPO threshold**, specify hello RPO limit.</span></span> <span data-ttu-id="f5ab1-110">Это значение указывает, как часто создаются точки восстановления данных.</span><span class="sxs-lookup"><span data-stu-id="f5ab1-110">This value indicates how often data recovery points are created.</span></span> <span data-ttu-id="f5ab1-111">Если непрерывная репликация превышает это значение, выдаются оповещения.</span><span class="sxs-lookup"><span data-stu-id="f5ab1-111">An alert is generated if continuous replication exceeds this limit.</span></span>
4. <span data-ttu-id="f5ab1-112">В **хранения точки восстановления**, укажите длительность (в часах) является окном приветствия хранения для каждой точки восстановления.</span><span class="sxs-lookup"><span data-stu-id="f5ab1-112">In **Recovery point retention**, specify (in hours) how long hello retention window is for each recovery point.</span></span> <span data-ttu-id="f5ab1-113">Реплицированные виртуальные машины могут быть восстановлены tooany точки в окне.</span><span class="sxs-lookup"><span data-stu-id="f5ab1-113">Replicated VMs can be recovered tooany point in a window.</span></span> <span data-ttu-id="f5ab1-114">Копирование too24 часов хранения поддерживается для машин реплицируются toopremium хранилища и 72 часа для стандартного хранилища.</span><span class="sxs-lookup"><span data-stu-id="f5ab1-114">Up too24 hours retention is supported for machines replicated toopremium storage, and 72 hours for standard storage.</span></span>
5. <span data-ttu-id="f5ab1-115">В поле **Периодичность создания моментальных снимков с согласованием приложений**укажите, с какой периодичностью (в минутах) будут создаваться точки восстановления, содержащие моментальные снимки, согласованные на уровне приложений.</span><span class="sxs-lookup"><span data-stu-id="f5ab1-115">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="f5ab1-116">Нажмите кнопку **ОК** toocreate hello политики.</span><span class="sxs-lookup"><span data-stu-id="f5ab1-116">Click **OK** toocreate hello policy.</span></span>

    ![Политика репликации](./media/physical-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="f5ab1-118">При создании новой политики она автоматически связывается с сервера конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="f5ab1-118">When you create a new policy it's automatically associated with hello configuration server.</span></span> <span data-ttu-id="f5ab1-119">Для восстановления размещения по умолчанию автоматически создается соответствующая политика.</span><span class="sxs-lookup"><span data-stu-id="f5ab1-119">By default, a matching policy is automatically created for failback.</span></span> <span data-ttu-id="f5ab1-120">Например, если hello политика репликации — **политики rep** политика восстановления размещения hello будет **rep политика восстановления размещения**.</span><span class="sxs-lookup"><span data-stu-id="f5ab1-120">For example, if hello replication policy is **rep-policy** then hello failback policy will be **rep-policy-failback**.</span></span> <span data-ttu-id="f5ab1-121">Эта политика не используется, пока не будет запущено восстановление размещения из Azure.</span><span class="sxs-lookup"><span data-stu-id="f5ab1-121">This policy isn't used until you initiate a failback from Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5ab1-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f5ab1-122">Next steps</span></span>

<span data-ttu-id="f5ab1-123">Go слишком[шаг 9: Установка службы Mobility hello](physical-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="f5ab1-123">Go too[Step 9: Install hello Mobility service](physical-walkthrough-install-mobility.md)</span></span>
