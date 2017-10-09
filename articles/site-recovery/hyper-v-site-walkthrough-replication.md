---
title: "aaaSet политику репликации для виртуальных Машин Hyper-V tooAzure репликации (без System Center VMM) с Azure Site Recovery | Документы Microsoft"
description: "Собраны действия hello потребуется tooset политику репликации при репликации виртуальных машин Hyper-V tooAzure хранилища"
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 1777e0eb-accb-42b5-a747-11272e131a52
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 4bd7161f4a0f015da0ecf595fbc6861ede5d68b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-set-up-a-replication-policy-for-hyper-v-vm-replication-tooazure"></a><span data-ttu-id="4a322-103">Шаг 9: Настройка политики репликации для виртуальных Машин Hyper-V tooAzure репликации</span><span class="sxs-lookup"><span data-stu-id="4a322-103">Step 9: Set up a replication policy for Hyper-V VM replication tooAzure</span></span>

<span data-ttu-id="4a322-104">В этой статье описывается как tooset политику репликации при репликации tooAzure виртуальных машин Hyper-V (без System Center VMM) с помощью hello [Azure Site Recovery](site-recovery-overview.md) в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="4a322-104">This article describes how tooset up a replication policy when you're replicating Hyper-V VMs tooAzure (without System Center VMM) using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="4a322-105">Учет комментарии и вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="4a322-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="about-snapshots"></a><span data-ttu-id="4a322-106">Сведения о моментальных снимках</span><span class="sxs-lookup"><span data-stu-id="4a322-106">About snapshots</span></span>

<span data-ttu-id="4a322-107">Hyper-V использует два типа моментальных снимков — стандартного моментального снимка, которая обеспечивает добавочный моментальный снимок всей виртуальной машины hello и согласованных с приложением моментальный снимок, создает моментальный снимок в момент данные приложения hello виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="4a322-107">Hyper-V uses two types of snapshots — a standard snapshot that provides an incremental snapshot of hello entire virtual machine, and an application-consistent snapshot that takes a point-in-time snapshot of hello application data inside hello virtual machine.</span></span>
    - <span data-ttu-id="4a322-108">Моментальные снимки приложений используйте tooensure службы теневого копирования томов (VSS), приложения находятся в согласованном состоянии при hello моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="4a322-108">Application-consistent snapshots use Volume Shadow Copy Service (VSS) tooensure that applications are in a consistent state when hello snapshot is taken.</span></span>
    - <span data-ttu-id="4a322-109">Если включить моментальные снимки приложений повлияет на производительность hello приложений, работающих на исходных виртуальных машинах.</span><span class="sxs-lookup"><span data-stu-id="4a322-109">If you enable application-consistent snapshots, it will affect hello performance of applications running on source virtual machines.</span></span> <span data-ttu-id="4a322-110">Убедитесь, что hello значение, заданное меньше, чем количество дополнительных точек восстановления, настроенные в hello.</span><span class="sxs-lookup"><span data-stu-id="4a322-110">Ensure that hello value you set is less than hello number of additional recovery points you configure.</span></span>

## <a name="set-up-a-replication-policy"></a><span data-ttu-id="4a322-111">Настройка политики репликации</span><span class="sxs-lookup"><span data-stu-id="4a322-111">Set up a replication policy</span></span>

1. <span data-ttu-id="4a322-112">Щелкните toocreate новую политику репликации **подготовки инфраструктуры** > **параметры репликации** > **+ Создание и связывание**.</span><span class="sxs-lookup"><span data-stu-id="4a322-112">toocreate a new replication policy, click **Prepare infrastructure** > **Replication Settings** > **+Create and associate**.</span></span>

    ![Сеть](./media/hyper-v-site-walkthrough-replication/gs-replication.png)
2. <span data-ttu-id="4a322-114">На странице **Создать и связать политику**укажите имя политики.</span><span class="sxs-lookup"><span data-stu-id="4a322-114">In **Create and associate policy**, specify a policy name.</span></span>
3. <span data-ttu-id="4a322-115">В **частота копирования**, укажите, как часто tooreplicate дельта-данные после начальной репликации hello (каждые 30 секунд, 5 или 15 минут).</span><span class="sxs-lookup"><span data-stu-id="4a322-115">In **Copy frequency**, specify how often you want tooreplicate delta data after hello initial replication (every 30 seconds, 5 or 15 minutes).</span></span>

    > [!NOTE]
    > <span data-ttu-id="4a322-116">30 второй частоты не поддерживается при репликации toopremium хранилища.</span><span class="sxs-lookup"><span data-stu-id="4a322-116">A 30 second frequency isn't supported when replicating toopremium storage.</span></span> <span data-ttu-id="4a322-117">ограничение Hello определяется hello число моментальных снимков для каждого большого двоичного объекта (100), поддерживаемое хранилище premium.</span><span class="sxs-lookup"><span data-stu-id="4a322-117">hello limitation is determined by hello number of snapshots per blob (100) supported by premium storage.</span></span> <span data-ttu-id="4a322-118">[Подробнее](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob).</span><span class="sxs-lookup"><span data-stu-id="4a322-118">[Learn more](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob).</span></span>

4. <span data-ttu-id="4a322-119">В **хранения точки восстановления**, укажите, сколько часов является окном приветствия хранения для каждой точки восстановления.</span><span class="sxs-lookup"><span data-stu-id="4a322-119">In **Recovery point retention**, specify in hours how long hello retention window is for each recovery point.</span></span> <span data-ttu-id="4a322-120">Виртуальные машины могут быть восстановлены tooany точки внутри окна.</span><span class="sxs-lookup"><span data-stu-id="4a322-120">VMs can be recovered tooany point within a window.</span></span>
5. <span data-ttu-id="4a322-121">В поле **Периодичность создания моментальных снимков с согласованием приложений** укажите, как часто (от 1-12 до часов) нужно создавать точки восстановления, содержащие согласованные на уровне приложений моментальные снимки.</span><span class="sxs-lookup"><span data-stu-id="4a322-121">In **App-consistent snapshot frequency**, specify how frequently (1-12 hours) recovery points containing application-consistent snapshots are created.</span></span>
6. <span data-ttu-id="4a322-122">В **время начала начальной репликации**, укажите, когда toostart hello начальной репликации.</span><span class="sxs-lookup"><span data-stu-id="4a322-122">In **Initial replication start time**, specify when toostart hello initial replication.</span></span> <span data-ttu-id="4a322-123">Hello репликация выполняется по пропускной способности Интернета, поэтому вы можете tooschedule его вне вашей занятости времени.</span><span class="sxs-lookup"><span data-stu-id="4a322-123">hello replication occurs over your internet bandwidth so you might want tooschedule it outside your busy hours.</span></span> <span data-ttu-id="4a322-124">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="4a322-124">Then click **OK**.</span></span>

    ![Политика репликации](./media/hyper-v-site-walkthrough-replication/gs-replication2.png)

<span data-ttu-id="4a322-126">При создании новой политики, она автоматически связывается с узла Hyper-V hello.</span><span class="sxs-lookup"><span data-stu-id="4a322-126">When you create a new policy, it's automatically associated with hello Hyper-V site.</span></span> <span data-ttu-id="4a322-127">Узел Hyper-V (и hello виртуальные машины в ней) можно связать с несколькими политиками репликации в **репликации** > политики name > **связать узла Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="4a322-127">You can associate a Hyper-V site (and hello VMs in it) with multiple replication policies in **Replication** > policy-name > **Associate Hyper-V Site**.</span></span>



## <a name="next-steps"></a><span data-ttu-id="4a322-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4a322-128">Next steps</span></span>

<span data-ttu-id="4a322-129">Go слишком[шаг 10: включение репликации](hyper-v-site-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="4a322-129">Go too[Step 10: Enable replication](hyper-v-site-walkthrough-enable-replication.md)</span></span>
