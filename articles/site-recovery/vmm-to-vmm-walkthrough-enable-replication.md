---
title: "вторичный сайт Hyper-V aaaEnable репликации tooa с Azure Site Recovery | Документы Microsoft"
description: "Описывает, как tooenable репликации для виртуальных машин Hyper-V, репликация tooa получателей System Center VMM сайта с помощью Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d8782d14-9fef-4396-8912-ff945efc851b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: b4484e0118cb23f343187fe867d9795d30926baf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-enable-replication-tooa-secondary-site-for-hyper-v-vms"></a><span data-ttu-id="f3566-103">Шаг 9: Включение репликации tooa вторичного сайта для виртуальных машин Hyper-V</span><span class="sxs-lookup"><span data-stu-id="f3566-103">Step 9: Enable replication tooa secondary site for Hyper-V VMs</span></span>


<span data-ttu-id="f3566-104">После настройки политики репликации, этот статье tooenable репликации tooa получателей диспетчера виртуальных машин System Center (VMM) сайт используется для локального Hyper-V виртуальных машин (ВМ) с помощью [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f3566-104">After setting up a replication policy, use this article tooenable replication tooa secondary System Center Virtual Machine Manager (VMM) site for on-premises Hyper-V virtual machines (VM), using [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="f3566-105">После считывания в этой статье, отправлять любые комментарии, внизу hello, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="f3566-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="select-vms-tooreplicate"></a><span data-ttu-id="f3566-106">Выберите tooreplicate виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="f3566-106">Select VMs tooreplicate</span></span>

1. <span data-ttu-id="f3566-107">Последовательно выберите **Шаг 2. Репликация приложения** > **Источник**.</span><span class="sxs-lookup"><span data-stu-id="f3566-107">Click **Step 2: Replicate application** > **Source**.</span></span> 

    ![Включение репликации](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication1.png)

2. <span data-ttu-id="f3566-109">В **источника**, выберите сервер VMM hello и облака, в которых hello находятся узлы Hyper-V требуется tooreplicate hello.</span><span class="sxs-lookup"><span data-stu-id="f3566-109">In **Source**, select hello VMM server, and hello cloud in which hello Hyper-V hosts you want tooreplicate are located.</span></span> <span data-ttu-id="f3566-110">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f3566-110">Then click **OK**.</span></span>

    ![Включение репликации](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication2.png)
3. <span data-ttu-id="f3566-112">В **целевой**, проверьте hello дополнительный сервер VMM и облака.</span><span class="sxs-lookup"><span data-stu-id="f3566-112">In **Target**, verify hello secondary VMM server and cloud.</span></span>
4. <span data-ttu-id="f3566-113">В **виртуальные машины**, выберите виртуальные машины hello требуется tooprotect из списка hello.</span><span class="sxs-lookup"><span data-stu-id="f3566-113">In **Virtual machines**, select hello VMs you want tooprotect from hello list.</span></span>

    ![Включение защиты виртуальной машины](./media/vmm-to-vmm-walkthrough-enable-replication/enable-replication5.png)

<span data-ttu-id="f3566-115">Вы можете отслеживать ход выполнения hello **включить защиту** действия в **заданий** > **задания Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="f3566-115">You can track progress of hello **Enable Protection** action in **Jobs** > **Site Recovery jobs**.</span></span> <span data-ttu-id="f3566-116">После hello **окончательной установки защиты** завершения задания, hello начальная репликация завершается и hello виртуальная машина будет готова для отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="f3566-116">After hello **Finalize Protection** job completes, hello initial replication is complete, and hello virtual machine is ready for failover.</span></span>

<span data-ttu-id="f3566-117">Обратите внимание на следующее.</span><span class="sxs-lookup"><span data-stu-id="f3566-117">Note that:</span></span>

- <span data-ttu-id="f3566-118">Можно также включить защиту для виртуальных машин в консоли VMM hello.</span><span class="sxs-lookup"><span data-stu-id="f3566-118">You can also enable protection for virtual machines in hello VMM console.</span></span> <span data-ttu-id="f3566-119">Нажмите кнопку **включить защиту** на панели инструментов hello в свойствах виртуальной машины hello > **Azure Site Recovery** вкладки.</span><span class="sxs-lookup"><span data-stu-id="f3566-119">Click **Enable Protection** on hello toolbar in hello virtual machine properties > **Azure Site Recovery** tab.</span></span>
- <span data-ttu-id="f3566-120">После включения репликации, можно просмотреть свойства для hello виртуальной Машины в **реплицируются элементы**.</span><span class="sxs-lookup"><span data-stu-id="f3566-120">After you've enabled replication, you can view properties for hello VM in **Replicated Items**.</span></span> <span data-ttu-id="f3566-121">На hello **Essentials** панели мониторинга, можно просмотреть информацию о политике репликации hello hello виртуальной Машины и ее состояние.</span><span class="sxs-lookup"><span data-stu-id="f3566-121">On hello **Essentials** dashboard, you can see information about hello replication policy for hello VM and its status.</span></span> <span data-ttu-id="f3566-122">Щелкните **Свойства** для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="f3566-122">Click **Properties** for more details.</span></span>

## <a name="onboard-existing-vms"></a><span data-ttu-id="f3566-123">Включение имеющихся виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="f3566-123">Onboard existing VMs</span></span>

<span data-ttu-id="f3566-124">Если в VMM есть виртуальные машины, которые реплицируются с помощью реплики Hyper-V, их можно включить в репликацию Azure Site Recovery следующим образом.</span><span class="sxs-lookup"><span data-stu-id="f3566-124">If you have existing virtual machines in VMM that are replicating with Hyper-V Replica, you can onboard them for Azure Site Recovery replication as follows:</span></span>

1. <span data-ttu-id="f3566-125">Убедитесь, что сервер hello Hyper-V, размещающий hello существующей виртуальной Машины находится в основное облако hello и вторичное облако hello расположен сервер Hyper-V, hello, размещение hello реплики виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="f3566-125">Ensure that hello Hyper-V server hosting hello existing VM is located in hello primary cloud, and that hello Hyper-V server hosting hello replica virtual machine is located in hello secondary cloud.</span></span>
2. <span data-ttu-id="f3566-126">Убедитесь, что политика репликации настроена для hello основное облако VMM.</span><span class="sxs-lookup"><span data-stu-id="f3566-126">Make sure a replication policy is configured for hello primary VMM cloud.</span></span>
3. <span data-ttu-id="f3566-127">Включение репликации для основной виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="f3566-127">Enable replication for hello primary virtual machine.</span></span> <span data-ttu-id="f3566-128">Восстановления сайтов Azure и VMM убедитесь, что hello того же сервера реплики и виртуальной машины обнаруживается и будет использовать Azure Site Recovery и установить репликацию с использованием hello указаны параметры.</span><span class="sxs-lookup"><span data-stu-id="f3566-128">Azure Site Recovery and VMM ensure that hello same replica host and virtual machine is detected, and Azure Site Recovery will reuse and reestablish replication using hello specified settings.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f3566-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f3566-129">Next steps</span></span>

<span data-ttu-id="f3566-130">Go слишком[шаг 10: запустите тестовую отработку отказа](vmm-to-vmm-walkthrough-test-failover.md).</span><span class="sxs-lookup"><span data-stu-id="f3566-130">Go too[Step 10: Run a test failover](vmm-to-vmm-walkthrough-test-failover.md).</span></span>
