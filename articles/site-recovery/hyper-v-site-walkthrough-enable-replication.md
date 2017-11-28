---
title: "aaaEnable репликации для виртуальных машин Hyper-V, репликация tooAzure (без System Center VMM) с Azure Site Recovery | Документы Microsoft"
description: "Собраны действия hello необходимо tooAzure tooenable репликации для виртуальных машин Hyper-V с помощью службы Azure Site Recovery hello"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: bd31ef01-69f1-4591-a519-e42510a6e2f4
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 1589cb7aa1fe954e075cb7bf1f4a4ec199ed3ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-enable-replication-for-hyper-v-vms-replicating-tooazure"></a><span data-ttu-id="33baf-103">Шаг 10: Включение репликации для виртуальных машин Hyper-V, репликация tooAzure</span><span class="sxs-lookup"><span data-stu-id="33baf-103">Step 10: Enable replication for Hyper-V VMs replicating tooAzure</span></span>


<span data-ttu-id="33baf-104">В этой статье описывается, как репликация tooenable для локальных виртуальных машин Hyper-V (не под управлением System Center VMM) tooAzure, с помощью hello [Azure Site Recovery](site-recovery-overview.md) в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="33baf-104">This article describes how tooenable replication for on-premises Hyper-V virtual machines (not managed by System Center VMM) tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="33baf-105">Учет комментарии и вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="33baf-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="before-you-start"></a><span data-ttu-id="33baf-106">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="33baf-106">Before you start</span></span>

<span data-ttu-id="33baf-107">Прежде чем начать, убедитесь, что учетная запись Azure пользователя имеет необходимые hello [разрешений](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable репликацию новых tooAzure виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="33baf-107">Before you start, ensure that your Azure user account has hello required [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of a new virtual machine tooAzure.</span></span>

## <a name="exclude-disks-from-replication"></a><span data-ttu-id="33baf-108">Исключение дисков из репликации</span><span class="sxs-lookup"><span data-stu-id="33baf-108">Exclude disks from replication</span></span>

<span data-ttu-id="33baf-109">По умолчанию реплицируются все диски на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="33baf-109">By default all disks on a machine are replicated.</span></span> <span data-ttu-id="33baf-110">Диски можно исключить из репликации.</span><span class="sxs-lookup"><span data-stu-id="33baf-110">You can exclude disks from replication.</span></span> <span data-ttu-id="33baf-111">Например tooreplicate диски с временные данные или данные, которая обновляется каждый раз, компьютер не имеет смысла или повторном запуске приложения (например pagefile.sys или базы данных tempdb SQL Server).</span><span class="sxs-lookup"><span data-stu-id="33baf-111">For example you might not want tooreplicate disks with temporary data, or data that's refreshed each time a machine or application restarts (for example pagefile.sys or SQL Server tempdb).</span></span> [<span data-ttu-id="33baf-112">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="33baf-112">Learn more</span></span>](site-recovery-exclude-disk.md)


## <a name="replicate-vms"></a><span data-ttu-id="33baf-113">Репликация виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="33baf-113">Replicate VMs</span></span>

<span data-ttu-id="33baf-114">Включите репликацию для виртуальных машин, сделав следующее.</span><span class="sxs-lookup"><span data-stu-id="33baf-114">Enable replication for VMs as follows:</span></span>          

1. <span data-ttu-id="33baf-115">Выберите **Репликация приложения** > **Источник**.</span><span class="sxs-lookup"><span data-stu-id="33baf-115">Click **Replicate application** > **Source**.</span></span> <span data-ttu-id="33baf-116">После настройки репликации для hello первый раз, можно щелкнуть **+ реплицировать** tooenable репликации для дополнительных компьютеров.</span><span class="sxs-lookup"><span data-stu-id="33baf-116">After you've set up replication for hello first time, you can click **+Replicate** tooenable replication for additional machines.</span></span>

    ![Включение репликации](./media/hyper-v-site-walkthrough-enable-replication/enable-replication.png)
2. <span data-ttu-id="33baf-118">В **источника**, выберите узел Hyper-V hello.</span><span class="sxs-lookup"><span data-stu-id="33baf-118">In **Source**, select hello Hyper-V site.</span></span> <span data-ttu-id="33baf-119">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="33baf-119">Then click **OK**.</span></span>
3. <span data-ttu-id="33baf-120">В **целевой**, выберите подписку хранилище hello и hello модель отработки отказа требуется toouse в Azure (классического или ресурса управления), после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="33baf-120">In **Target**, select hello vault subscription, and hello failover model you want toouse in Azure (classic or resource management) after failover.</span></span>
4. <span data-ttu-id="33baf-121">Выберите учетную запись хранения hello, требуется toouse.</span><span class="sxs-lookup"><span data-stu-id="33baf-121">Select hello storage account you want toouse.</span></span> <span data-ttu-id="33baf-122">Если нет необходимости toouse учетную запись, вы можете [создать](#set-up-an-azure-storage-account).</span><span class="sxs-lookup"><span data-stu-id="33baf-122">If you don't have an account you want toouse, you can [create one](#set-up-an-azure-storage-account).</span></span> <span data-ttu-id="33baf-123">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="33baf-123">Then click **OK**.</span></span>
5. <span data-ttu-id="33baf-124">Выберите hello Azure toowhich сети и подсети виртуальных машин Azure подключится, когда они создаются отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="33baf-124">Select hello Azure network and subnet toowhich Azure VMs will connect when they're created failover.</span></span>

    - <span data-ttu-id="33baf-125">Выберите tooapply hello параметры tooall виртуальных машин в сети включена для репликации, **настроить сейчас для всех выбранных компьютеров**.</span><span class="sxs-lookup"><span data-stu-id="33baf-125">tooapply hello network settings tooall machines you enable for replication, select **Configure now for selected machines**.</span></span>
    - <span data-ttu-id="33baf-126">Выберите **настроить позже** tooselect hello сети Azure на один компьютер.</span><span class="sxs-lookup"><span data-stu-id="33baf-126">Select **Configure later** tooselect hello Azure network per machine.</span></span>
    - <span data-ttu-id="33baf-127">Если у вас нет сети, требуется toouse, вы можете [создать](#set-up-an-azure-network).</span><span class="sxs-lookup"><span data-stu-id="33baf-127">If you don't have a network you want toouse, you can [create one](#set-up-an-azure-network).</span></span> <span data-ttu-id="33baf-128">Выберите подсеть (если это применимо).</span><span class="sxs-lookup"><span data-stu-id="33baf-128">Select a subnet if applicable.</span></span> <span data-ttu-id="33baf-129">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="33baf-129">Then click **OK**.</span></span>

   ![Включение репликации](./media/hyper-v-site-walkthrough-enable-replication/enable-replication11.png)

6. <span data-ttu-id="33baf-131">В **виртуальные машины** > **выберите виртуальные машины**щелкните и выберите каждый компьютер, tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="33baf-131">In **Virtual Machines** > **Select virtual machines**, click and select each machine you want tooreplicate.</span></span> <span data-ttu-id="33baf-132">Можно выбрать только те компьютеры, для которых можно включить репликацию.</span><span class="sxs-lookup"><span data-stu-id="33baf-132">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="33baf-133">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="33baf-133">Then click **OK**.</span></span>

    ![Включение репликации](./media/hyper-v-site-walkthrough-enable-replication/enable-replication5-for-exclude-disk.png)

7. <span data-ttu-id="33baf-135">В **свойства** > **Настройка свойств**выберите hello операционной системы для виртуальных машин выбранных hello и hello диска ОС.</span><span class="sxs-lookup"><span data-stu-id="33baf-135">In **Properties** > **Configure properties**, select hello operating system for hello selected VMs, and hello OS disk.</span></span>
8. <span data-ttu-id="33baf-136">Убедитесь, что hello виртуальной Машины Azure имя (целевой) соответствует [требования к виртуальной машине Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="33baf-136">Verify that hello Azure VM name (target name) complies with [Azure virtual machine requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
9. <span data-ttu-id="33baf-137">По умолчанию выбраны все диски hello hello виртуальной Машины, для репликации.</span><span class="sxs-lookup"><span data-stu-id="33baf-137">By default all hello disks of hello VM are selected for replication.</span></span> <span data-ttu-id="33baf-138">Снимите флажок дисков tooexclude их.</span><span class="sxs-lookup"><span data-stu-id="33baf-138">Clear disks tooexclude them.</span></span>
10. <span data-ttu-id="33baf-139">Нажмите кнопку **ОК** toosave изменений.</span><span class="sxs-lookup"><span data-stu-id="33baf-139">Click **OK** toosave changes.</span></span> <span data-ttu-id="33baf-140">Позже можно задать дополнительные свойства.</span><span class="sxs-lookup"><span data-stu-id="33baf-140">You can set additional properties later.</span></span>

    ![Включение репликации](./media/hyper-v-site-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

11. <span data-ttu-id="33baf-142">В **параметры репликации** > **Настройка параметров репликации**, выберите политику репликации hello требуется tooapply к hello защищенных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="33baf-142">In **Replication settings** > **Configure replication settings**, select hello replication policy you want tooapply for hello protected VMs.</span></span> <span data-ttu-id="33baf-143">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="33baf-143">Then click **OK**.</span></span> <span data-ttu-id="33baf-144">Можно изменить политику репликации hello в **политики репликации** > политики name > **изменение параметров**.</span><span class="sxs-lookup"><span data-stu-id="33baf-144">You can modify hello replication policy in **Replication policies** > policy-name > **Edit Settings**.</span></span> <span data-ttu-id="33baf-145">Изменения будут применяться к компьютерам, для которых уже выполняется репликация, и к новым компьютерам.</span><span class="sxs-lookup"><span data-stu-id="33baf-145">Changes you apply will be used for machines that are already replicating, and new machines.</span></span>


   ![Включение репликации](./media/hyper-v-site-walkthrough-enable-replication/enable-replication7.png)

<span data-ttu-id="33baf-147">Вы можете отслеживать ход выполнения hello **включить защиту** задания в **заданий** > **задания Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="33baf-147">You can track progress of hello **Enable Protection** job in **Jobs** > **Site Recovery jobs**.</span></span> <span data-ttu-id="33baf-148">После hello **окончательной установки защиты** задание запускается hello машина готова для отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="33baf-148">After hello **Finalize Protection** job runs hello machine is ready for failover.</span></span>


## <a name="next-steps"></a><span data-ttu-id="33baf-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="33baf-149">Next steps</span></span>


<span data-ttu-id="33baf-150">Go слишком[шаг 11: запустите тестовую отработку отказа](hyper-v-site-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="33baf-150">Go too[Step 11: Run a test failover](hyper-v-site-walkthrough-test-failover.md)</span></span>
