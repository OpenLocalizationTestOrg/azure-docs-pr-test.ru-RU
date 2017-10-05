---
title: "Выполнение тестовой отработки отказа для репликации виртуальной машины Hyper-V на дополнительный сайт с использованием Azure Site Recovery | Документация Майкрософт"
description: "Здесь описывается, как выполнить тестовую отработку отказа для репликации виртуальной машины Hyper-V на дополнительный сайт System Center VMM с помощью Azure Site Recovery."
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
ms.openlocfilehash: 23d235d326273e7ec59feee6588a39f685401e52
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="step-10-run-a-test-failover-for-hyper-v-replication-to-a-secondary-site"></a><span data-ttu-id="98005-103">Шаг 10. Выполнение тестовой отработки отказа для репликации Hyper-V на дополнительный сайт</span><span class="sxs-lookup"><span data-stu-id="98005-103">Step 10: Run a test failover for Hyper-V replication to a secondary site</span></span>


<span data-ttu-id="98005-104">Включив репликацию для виртуальных машин Hyper-V с помощью [Azure Site Recovery](site-recovery-overview.md), воспользуйтесь сведениями в этой статье для выполнения тестовой отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="98005-104">After you enable replication for Hyper-V virtual machines (VMs) with [Azure Site Recovery](site-recovery-overview.md), use this article to run a test failover.</span></span> <span data-ttu-id="98005-105">При тестовой отработке отказа проверяется, работает ли репликация, не влияя на рабочую среду.</span><span class="sxs-lookup"><span data-stu-id="98005-105">A test failover verifies that replication is working, without impacting your production environment.</span></span> 


<span data-ttu-id="98005-106">Любые комментарии, которые возникнут после прочтения этой статьи, можно добавить в конце этой страницы или на [форуме по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="98005-106">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="98005-107">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="98005-107">Before you start</span></span>

- <span data-ttu-id="98005-108">Запустив тестовую отработку отказа, можно указать сеть, к которой будут подключаться тестовые виртуальные машины реплики.</span><span class="sxs-lookup"><span data-stu-id="98005-108">When you're triggering a test failover, you can specify the network to which the test replica VMs will connect.</span></span> <span data-ttu-id="98005-109">Дополнительные сведения о параметрах сети в Site Recovery см. в [этом разделе](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery).</span><span class="sxs-lookup"><span data-stu-id="98005-109">[Learn more](site-recovery-test-failover-vmm-to-vmm.md#network-options-in-site-recovery) about the network options.</span></span>
- <span data-ttu-id="98005-110">Мы рекомендуем не выбирать сеть, выбранную во время сетевого сопоставления.</span><span class="sxs-lookup"><span data-stu-id="98005-110">We recommend that you don't choose a network that you selected during network mapping.</span></span>
- <span data-ttu-id="98005-111">В инструкциях в этой статье описывается выполнение отработки отказа для одной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="98005-111">The instructions in this article describe how to fail over a single VM.</span></span> <span data-ttu-id="98005-112">Если нужно выполнить отработку отказа нескольких виртуальных машин, ознакомьтесь со сведениями о [создании планов восстановления](site-recovery-create-recovery-plans.md).</span><span class="sxs-lookup"><span data-stu-id="98005-112">Read about [creating recovery plans](site-recovery-create-recovery-plans.md) if you want to fail over multiple VMs together.</span></span>
- <span data-ttu-id="98005-113">Ознакомьтесь с [ограничениями для тестовой отработки отказа](site-recovery-test-failover-vmm-to-vmm.md#things-to-note).</span><span class="sxs-lookup"><span data-stu-id="98005-113">Read about [limitations for test failovers](site-recovery-test-failover-vmm-to-vmm.md#things-to-note).</span></span>
- <span data-ttu-id="98005-114">IP-адрес, выделенный виртуальной машине при тестовой отработки отказа, это тот же IP-адрес, который она бы получила при выполнении плановой или внеплановой отработки отказа (если этот IP-адрес доступен в сети тестовой отработки отказа).</span><span class="sxs-lookup"><span data-stu-id="98005-114">The IP address given to a VM during test failover is the same IP address that the VM would receive for a planned or unplanned failover (presuming that the IP address is available in the test failover network).</span></span> <span data-ttu-id="98005-115">Если такой IP-адрес недоступен в сети тестовой отработки отказа, виртуальная машина получит другой IP-адрес, доступный в сети тестовой отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="98005-115">If the IP address isn't available in the test failover network, the VM receives another IP address that is available in the test failover network.</span></span>
- <span data-ttu-id="98005-116">Если вы хотите выполнить тестовую отработку отказа в рабочей сети, то обратите внимание на следующие моменты для полной проверки сквозного сетевого подключения на виртуальной машине:</span><span class="sxs-lookup"><span data-stu-id="98005-116">If you do want to do a test failover in your production network, for full validatation of end-to-end network connectivity machine, note that:</span></span>
    - <span data-ttu-id="98005-117">При выполнении тестовой отработки отказа основную виртуальную машину следует выключать.</span><span class="sxs-lookup"><span data-stu-id="98005-117">The primary VM should be shut down when you're doing the test failover.</span></span> <span data-ttu-id="98005-118">В противном случае в одной сети будут одновременно работать две виртуальные машины с одинаковыми идентификаторами.</span><span class="sxs-lookup"><span data-stu-id="98005-118">Otherwise, two VMs with the same identity will be running in the same network at the same time.</span></span> 
    - <span data-ttu-id="98005-119">Если тестовые виртуальные машины изменяются, при очистке тестовой отработки отказа изменения будут утеряны.</span><span class="sxs-lookup"><span data-stu-id="98005-119">If you make changes to test VMs, those changes are lost when you clean up the test failover.</span></span> <span data-ttu-id="98005-120">Они не реплицируются на основную виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="98005-120">These changes aren't replicated back to the primary VM.</span></span>
    - <span data-ttu-id="98005-121">Тестирование рабочей сети приводит к простою рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="98005-121">Testing a a production network leads to downtime for your production workloads.</span></span> <span data-ttu-id="98005-122">Попросите пользователей не использовать приложение во время аварийного восстановления.</span><span class="sxs-lookup"><span data-stu-id="98005-122">Ask users not to use the app when the disaster recovery drill is in progress.</span></span>  


## <a name="run-a-test-failover-for-a-vm"></a><span data-ttu-id="98005-123">Выполнение тестовой отработки отказа для виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="98005-123">Run a test failover for a VM</span></span>

1. <span data-ttu-id="98005-124">Чтобы выполнить отработку отказа для одной виртуальной машины, в разделе **Реплицированные элементы** щелкните виртуальную машину и **Тестовая отработка отказа**.</span><span class="sxs-lookup"><span data-stu-id="98005-124">To fail over a single VM, in **Replicated Items**, click the VM > **Test Failover**.</span></span>
2. <span data-ttu-id="98005-125">В области **Тестовая отработка отказа** укажите, как тестовые виртуальные машины будут подключаться к сетям после тестовой отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="98005-125">In **Test Failover**, specify how test VMs will be connected to networks after the test failover.</span></span> 
3. <span data-ttu-id="98005-126">Нажмите кнопку **ОК** , чтобы запустить отработку отказа.</span><span class="sxs-lookup"><span data-stu-id="98005-126">Click **OK** to begin the failover.</span></span> <span data-ttu-id="98005-127">Отслеживайте ход выполнения на вкладке **Задания** .</span><span class="sxs-lookup"><span data-stu-id="98005-127">Track progress on the **Jobs** tab.</span></span>
5. <span data-ttu-id="98005-128">После отработки отказа проверьте, успешно ли запущены тестовые виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="98005-128">After failover is complete, verify that the test VMs start successfully.</span></span>
6. <span data-ttu-id="98005-129">Когда все будет готово, щелкните **Cleanup test failover** (Очистить тестовую отработку отказа) в плане восстановления.</span><span class="sxs-lookup"><span data-stu-id="98005-129">When you're done, click **Cleanup test failover** on the recovery plan.</span></span>
7. <span data-ttu-id="98005-130">В разделе **Примечания** можно записать и сохранить любые замечания, связанные с тестовой отработкой отказа.</span><span class="sxs-lookup"><span data-stu-id="98005-130">In **Notes**, record and save any observations associated with the test failover.</span></span> <span data-ttu-id="98005-131">На этом шаге удаляются виртуальные машины и сети, созданные при тестовой отработке отказа.</span><span class="sxs-lookup"><span data-stu-id="98005-131">This step deletes the virtual machines and networks that were created during test failover.</span></span>


## <a name="next-steps"></a><span data-ttu-id="98005-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="98005-132">Next steps</span></span>

<span data-ttu-id="98005-133">После проверки развертывания изучите другие типы [отработки отказа](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="98005-133">After you've tested the deployment, learn more about other types of [failover](site-recovery-failover.md).</span></span>
