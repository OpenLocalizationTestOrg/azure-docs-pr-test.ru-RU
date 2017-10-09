---
title: "aaaSet политику репликации для виртуальной Машины Hyper-V (с помощью VMM) tooAzure репликации с помощью Azure Site Recovery | Документы Microsoft"
description: "Описывает способ tooset политику репликации для виртуальной Машины Hyper-V (с помощью VMM) tooAzure репликации с помощью Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: ee808b20-324b-4198-b831-edb65b95e8b7
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: e1579fde559ca34eca19a01e740fec28a0df2f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-set-up-a-replication-policy-for-hyper-v-vm-replication-with-vmm-tooazure"></a><span data-ttu-id="2af03-103">Шаг 10: Настройка политики репликации для виртуальных Машин Hyper-V tooAzure репликации (с помощью VMM)</span><span class="sxs-lookup"><span data-stu-id="2af03-103">Step 10: Set up a replication policy for Hyper-V VM replication (with VMM) tooAzure</span></span>


<span data-ttu-id="2af03-104">После настройки [сетевое сопоставление](vmm-to-azure-walkthrough-network-mapping.md), использование этой статьи tooconfigure политику репликации T\tooreplicate локальных виртуальных машин Hyper-V управляются в облаках tooAzure диспетчера виртуальных машин System Center (VMM), с помощью hello [ Azure Site Recovery](site-recovery-overview.md) в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="2af03-104">After setting up [network mapping](vmm-to-azure-walkthrough-network-mapping.md), use this article tooconfigure a replication policy T\tooreplicate on-premises Hyper-V virtual machines managed in System Center Virtual Machine Manager (VMM) clouds tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="2af03-105">После считывания в этой статье, отправлять любые комментарии, внизу hello, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="2af03-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="create-a-policy"></a><span data-ttu-id="2af03-106">Создание политики</span><span class="sxs-lookup"><span data-stu-id="2af03-106">Create a policy</span></span>

1. <span data-ttu-id="2af03-107">Щелкните toocreate новую политику репликации **подготовки инфраструктуры** > **параметры репликации** > **+ Создание и связывание**.</span><span class="sxs-lookup"><span data-stu-id="2af03-107">toocreate a new replication policy, click **Prepare infrastructure** > **Replication Settings** > **+Create and associate**.</span></span>

    ![Сеть](./media/vmm-to-azure-walkthrough-replication/gs-replication.png)
2. <span data-ttu-id="2af03-109">На странице **Создать и связать политику**укажите имя политики.</span><span class="sxs-lookup"><span data-stu-id="2af03-109">In **Create and associate policy**, specify a policy name.</span></span>
3. <span data-ttu-id="2af03-110">В **частота копирования**, укажите, как часто tooreplicate дельта-данные после начальной репликации hello (каждые 30 секунд, 5 или 15 минут).</span><span class="sxs-lookup"><span data-stu-id="2af03-110">In **Copy frequency**, specify how often you want tooreplicate delta data after hello initial replication (every 30 seconds, 5 or 15 minutes).</span></span>

    > [!NOTE]
    >  <span data-ttu-id="2af03-111">30 второй частоты не поддерживается при репликации toopremium хранилища.</span><span class="sxs-lookup"><span data-stu-id="2af03-111">A 30 second frequency isn't supported when replicating toopremium storage.</span></span> <span data-ttu-id="2af03-112">ограничение Hello определяется hello число моментальных снимков для каждого большого двоичного объекта (100), поддерживаемое хранилище premium.</span><span class="sxs-lookup"><span data-stu-id="2af03-112">hello limitation is determined by hello number of snapshots per blob (100) supported by premium storage.</span></span> [<span data-ttu-id="2af03-113">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="2af03-113">Learn more</span></span>](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)

4. <span data-ttu-id="2af03-114">В **хранения точки восстановления**, укажите в часах, как долго будет hello окна хранения для каждой из точек восстановления.</span><span class="sxs-lookup"><span data-stu-id="2af03-114">In **Recovery point retention**, specify in hours how long hello retention window will be for each recovery point.</span></span> <span data-ttu-id="2af03-115">Защищенные виртуальные машины могут быть восстановлены tooany точки внутри окна.</span><span class="sxs-lookup"><span data-stu-id="2af03-115">Protected machines can be recovered tooany point within a window.</span></span>
5. <span data-ttu-id="2af03-116">В поле **Периодичность создания моментальных снимков с согласованием приложений** укажите, как часто (от 1 до 12 часов) будут создаваться точки восстановления, содержащие согласованные с приложениями моментальные снимки.</span><span class="sxs-lookup"><span data-stu-id="2af03-116">In **App-consistent snapshot frequency**, specify how frequently (1-12 hours) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="2af03-117">Hyper-V использует два типа моментальных снимков — стандартного моментального снимка, которая обеспечивает добавочный моментальный снимок всей виртуальной машины hello и согласованных с приложением моментальный снимок, создает моментальный снимок в момент данные приложения hello виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="2af03-117">Hyper-V uses two types of snapshots — a standard snapshot that provides an incremental snapshot of hello entire virtual machine, and an application-consistent snapshot that takes a point-in-time snapshot of hello application data inside hello virtual machine.</span></span> <span data-ttu-id="2af03-118">Моментальные снимки приложений используйте tooensure службы теневого копирования томов (VSS), приложения находятся в согласованном состоянии при hello моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="2af03-118">Application-consistent snapshots use Volume Shadow Copy Service (VSS) tooensure that applications are in a consistent state when hello snapshot is taken.</span></span> <span data-ttu-id="2af03-119">Обратите внимание, что при включении снимков приложений влияет на hello производительность приложений, работающих на исходных виртуальных машинах.</span><span class="sxs-lookup"><span data-stu-id="2af03-119">Note that if you enable application-consistent snapshots, it will affect hello performance of applications running on source virtual machines.</span></span> <span data-ttu-id="2af03-120">Убедитесь, что hello значение, заданное меньше, чем количество дополнительных точек восстановления, настроенные в hello.</span><span class="sxs-lookup"><span data-stu-id="2af03-120">Ensure that hello value you set is less than hello number of additional recovery points you configure.</span></span>
6. <span data-ttu-id="2af03-121">В **время начала начальной репликации**, указывают, когда toostart hello начальной репликации.</span><span class="sxs-lookup"><span data-stu-id="2af03-121">In **Initial replication start time**, indicate when toostart hello initial replication.</span></span> <span data-ttu-id="2af03-122">Hello репликация выполняется по пропускной способности Интернета, поэтому вы можете tooschedule его вне вашей занятости времени.</span><span class="sxs-lookup"><span data-stu-id="2af03-122">hello replication occurs over your internet bandwidth so you might want tooschedule it outside your busy hours.</span></span>
7. <span data-ttu-id="2af03-123">В **шифровать данные, хранящиеся в Azure**, укажите ли tooencrypt rest данные в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="2af03-123">In **Encrypt data stored on Azure**, specify whether tooencrypt at rest data in Azure storage.</span></span> <span data-ttu-id="2af03-124">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="2af03-124">Then click **OK**.</span></span>

    ![Политика репликации](./media/vmm-to-azure-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="2af03-126">При создании новой политики она автоматически связывается с hello облака VMM.</span><span class="sxs-lookup"><span data-stu-id="2af03-126">When you create a new policy it's automatically associated with hello VMM cloud.</span></span> <span data-ttu-id="2af03-127">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="2af03-127">Click **OK**.</span></span> <span data-ttu-id="2af03-128">Дополнительные облака VMM (и hello виртуальных машин в них) можно связать с этой политикой репликации в **репликации** > имя политики > **связывание облака VMM**.</span><span class="sxs-lookup"><span data-stu-id="2af03-128">You can associate additional VMM clouds (and hello VMs in them) with this replication policy in **Replication** > policy name > **Associate VMM Cloud**.</span></span>

    ![Политика репликации](./media/vmm-to-azure-walkthrough-replication/policy-associate.png)



## <a name="next-steps"></a><span data-ttu-id="2af03-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2af03-130">Next steps</span></span>

<span data-ttu-id="2af03-131">Go слишком[шаг 11: включение репликации](vmm-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="2af03-131">Go too[Step 11: Enable replication](vmm-to-azure-walkthrough-enable-replication.md)</span></span>
