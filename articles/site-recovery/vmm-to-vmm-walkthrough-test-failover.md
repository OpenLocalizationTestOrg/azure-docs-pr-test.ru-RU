---
title: "aaaRun тестовую отработку отказа для виртуальной Машины Hyper-V репликации tooa вторичного сайта с помощью Azure Site Recovery | Документы Microsoft"
description: "Описывает, как toorun тестовую отработку отказа для виртуальных Машин Hyper-V репликации tooa получателей System Center VMM сайта с Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a3fd11ce-65a1-4308-8435-45cf954353ef
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: a60411541c2db001c573735bcb0d651f6618f295
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-run-a-test-failover-for-hyper-v-replication-tooa-secondary-site"></a><span data-ttu-id="e5e7f-103">Шаг 10: Запуск тестовой отработки отказа для Hyper-V репликации tooa вторичного сайта</span><span class="sxs-lookup"><span data-stu-id="e5e7f-103">Step 10: Run a test failover for Hyper-V replication tooa secondary site</span></span>


<span data-ttu-id="e5e7f-104">После включения репликации для виртуальных машин Hyper-V (ВМ) с [Azure Site Recovery](site-recovery-overview.md), использование этой статьи toorun тестовой отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="e5e7f-104">After you enable replication for Hyper-V virtual machines (VMs) with [Azure Site Recovery](site-recovery-overview.md), use this article toorun a test failover.</span></span> <span data-ttu-id="e5e7f-105">При тестовой отработке отказа проверяется, работает ли репликация, не влияя на рабочую среду.</span><span class="sxs-lookup"><span data-stu-id="e5e7f-105">A test failover verifies that replication is working, without impacting your production environment.</span></span> 


<span data-ttu-id="e5e7f-106">После считывания в этой статье, отправлять любые комментарии, внизу hello, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="e5e7f-106">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="e5e7f-107">Перед началом</span><span class="sxs-lookup"><span data-stu-id="e5e7f-107">Before you start</span></span>

- <span data-ttu-id="e5e7f-108">Когда Запуск тестовой отработки отказа, можно указать hello сети toowhich hello тестовой реплики будет подключаться виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="e5e7f-108">When you're triggering a test failover, you can specify hello network toowhich hello test replica VMs will connect.</span></span> <span data-ttu-id="e5e7f-109">[Дополнительные сведения](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery) о hello сетевых параметров.</span><span class="sxs-lookup"><span data-stu-id="e5e7f-109">[Learn more](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery) about hello network options.</span></span>
- <span data-ttu-id="e5e7f-110">Мы рекомендуем не выбирать сеть, выбранную во время сетевого сопоставления.</span><span class="sxs-lookup"><span data-stu-id="e5e7f-110">We recommend that you don't choose a network that you selected during network mapping.</span></span>
- <span data-ttu-id="e5e7f-111">Hello в этой статье описан первый способ toofail по одной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="e5e7f-111">hello instructions in this article describe how toofail over a single VM.</span></span> <span data-ttu-id="e5e7f-112">Узнайте, как [создание планов восстановления](site-recovery-create-recovery-plans.md) Если toofail через несколько виртуальных машин друг с другом.</span><span class="sxs-lookup"><span data-stu-id="e5e7f-112">Read about [creating recovery plans](site-recovery-create-recovery-plans.md) if you want toofail over multiple VMs together.</span></span>
- <span data-ttu-id="e5e7f-113">Ознакомьтесь с [ограничениями для тестовой отработки отказа](site-recovery-test-failover-vmm-to-vmm.md#things-to-note).</span><span class="sxs-lookup"><span data-stu-id="e5e7f-113">Read about [limitations for test failovers](site-recovery-test-failover-vmm-to-vmm.md#things-to-note).</span></span>
- <span data-ttu-id="e5e7f-114">Hello заданное tooa виртуальной Машины во время тестовой отработки отказа IP-адрес — hello же IP-адрес, который hello виртуальной Машины получают при выполнении плановой или незапланированной отработки отказа (предполагается, что IP-адрес hello доступна в hello тестовой отработки отказа сети).</span><span class="sxs-lookup"><span data-stu-id="e5e7f-114">hello IP address given tooa VM during test failover is hello same IP address that hello VM would receive for a planned or unplanned failover (presuming that hello IP address is available in hello test failover network).</span></span> <span data-ttu-id="e5e7f-115">Если IP-адрес hello не поддерживается в hello тестовой отработки отказа сети, hello виртуальной Машины получит другой IP-адрес, который доступен в hello тестовой отработки отказа сети.</span><span class="sxs-lookup"><span data-stu-id="e5e7f-115">If hello IP address isn't available in hello test failover network, hello VM receives another IP address that is available in hello test failover network.</span></span>
- <span data-ttu-id="e5e7f-116">Если вы хотите toodo тестовую отработку отказа в собственной рабочей сети, для полного прошедший проверку машины подключения к сети с начала до конца, обратите внимание, что:</span><span class="sxs-lookup"><span data-stu-id="e5e7f-116">If you do want toodo a test failover in your production network, for full validatation of end-to-end network connectivity machine, note that:</span></span>
    - <span data-ttu-id="e5e7f-117">Здравствуйте, основной виртуальной Машины необходимо завершить работу при выполнении тестовой отработки отказа hello.</span><span class="sxs-lookup"><span data-stu-id="e5e7f-117">hello primary VM should be shut down when you're doing hello test failover.</span></span> <span data-ttu-id="e5e7f-118">В противном случае две виртуальные машины с удостоверением будет выполняться в hello hello сетевых на hello то же время.</span><span class="sxs-lookup"><span data-stu-id="e5e7f-118">Otherwise, two VMs with hello same identity will be running in hello same network at hello same time.</span></span> 
    - <span data-ttu-id="e5e7f-119">При внесении изменений tootest виртуальных машин, эти изменения будут потеряны при очистке hello тестировании отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="e5e7f-119">If you make changes tootest VMs, those changes are lost when you clean up hello test failover.</span></span> <span data-ttu-id="e5e7f-120">Эти изменения не реплицированных задней toohello основной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="e5e7f-120">These changes aren't replicated back toohello primary VM.</span></span>
    - <span data-ttu-id="e5e7f-121">Тестирование в рабочей сети ведет toodowntime для рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="e5e7f-121">Testing a a production network leads toodowntime for your production workloads.</span></span> <span data-ttu-id="e5e7f-122">Попросите пользователей не toouse приложение hello hello аварийного восстановления во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="e5e7f-122">Ask users not toouse hello app when hello disaster recovery drill is in progress.</span></span>  


## <a name="run-a-test-failover-for-a-vm"></a><span data-ttu-id="e5e7f-123">Выполнение тестовой отработки отказа для виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="e5e7f-123">Run a test failover for a VM</span></span>

1. <span data-ttu-id="e5e7f-124">toofail по одной виртуальной Машины в **реплицируются элементы**, щелкните hello виртуальной Машины > **тестовой отработки отказа**.</span><span class="sxs-lookup"><span data-stu-id="e5e7f-124">toofail over a single VM, in **Replicated Items**, click hello VM > **Test Failover**.</span></span>
2. <span data-ttu-id="e5e7f-125">В **тестовой отработки отказа**, укажите, как ВМ будет проверка подключенных toonetworks после тестовой отработки отказа hello.</span><span class="sxs-lookup"><span data-stu-id="e5e7f-125">In **Test Failover**, specify how test VMs will be connected toonetworks after hello test failover.</span></span> 
3. <span data-ttu-id="e5e7f-126">Нажмите кнопку **ОК** hello toobegin перехода на другой ресурс.</span><span class="sxs-lookup"><span data-stu-id="e5e7f-126">Click **OK** toobegin hello failover.</span></span> <span data-ttu-id="e5e7f-127">Отслеживать ход выполнения hello **заданий** вкладки.</span><span class="sxs-lookup"><span data-stu-id="e5e7f-127">Track progress on hello **Jobs** tab.</span></span>
5. <span data-ttu-id="e5e7f-128">После завершения отработки отказа успешно проверьте hello теста для запуска виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e5e7f-128">After failover is complete, verify that hello test VMs start successfully.</span></span>
6. <span data-ttu-id="e5e7f-129">Когда закончите, нажмите кнопку **очистку тестовой отработки отказа** hello плана восстановления.</span><span class="sxs-lookup"><span data-stu-id="e5e7f-129">When you're done, click **Cleanup test failover** on hello recovery plan.</span></span>
7. <span data-ttu-id="e5e7f-130">В **заметки**, записать и сохранить все наблюдения, связанные с тестовой отработки отказа hello.</span><span class="sxs-lookup"><span data-stu-id="e5e7f-130">In **Notes**, record and save any observations associated with hello test failover.</span></span> <span data-ttu-id="e5e7f-131">Этот шаг удаляет hello виртуальные машины и сети, которые были созданы во время тестовой отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="e5e7f-131">This step deletes hello virtual machines and networks that were created during test failover.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e5e7f-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e5e7f-132">Next steps</span></span>

<span data-ttu-id="e5e7f-133">После тестирования развертывания hello, Дополнительные сведения о других типах [перехода на другой ресурс](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="e5e7f-133">After you've tested hello deployment, learn more about other types of [failover](site-recovery-failover.md).</span></span>
