---
title: "Включение репликации для репликации виртуальных машин Hyper-V (без использования System Center VMM) в Azure с помощью Azure Site Recovery | Документация Майкрософт"
description: "В этой статье кратко описаны шаги для включения репликации в Azure для виртуальных машин Hyper-V с помощью службы Azure Site Recovery"
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
ms.openlocfilehash: aabe99dbd375b80e4a87ca7a067927008672b4ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="step-10-enable-replication-for-hyper-v-vms-replicating-to-azure"></a><span data-ttu-id="2fc5c-103">Шаг 10. Включение репликации для репликации виртуальных машин Hyper-V в Azure</span><span class="sxs-lookup"><span data-stu-id="2fc5c-103">Step 10: Enable replication for Hyper-V VMs replicating to Azure</span></span>


<span data-ttu-id="2fc5c-104">В этой статье описано, как включить репликацию для локальных виртуальных машин Hyper-V (которыми не управляет System Center VMM) в Azure с помощью службы [Azure Site Recovery](site-recovery-overview.md) на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="2fc5c-104">This article describes how to enable replication for on-premises Hyper-V virtual machines (not managed by System Center VMM) to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="2fc5c-105">Комментарии или вопросы можно добавить в конце этой статьи или на [форуме по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="2fc5c-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="before-you-start"></a><span data-ttu-id="2fc5c-106">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="2fc5c-106">Before you start</span></span>

<span data-ttu-id="2fc5c-107">Прежде чем начать, убедитесь, что учетная запись пользователя Azure содержит [разрешения](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines), необходимые для включения репликации новой виртуальной машины в Azure.</span><span class="sxs-lookup"><span data-stu-id="2fc5c-107">Before you start, ensure that your Azure user account has the required [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) to enable replication of a new virtual machine to Azure.</span></span>

## <a name="exclude-disks-from-replication"></a><span data-ttu-id="2fc5c-108">Исключение дисков из репликации</span><span class="sxs-lookup"><span data-stu-id="2fc5c-108">Exclude disks from replication</span></span>

<span data-ttu-id="2fc5c-109">По умолчанию реплицируются все диски на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="2fc5c-109">By default all disks on a machine are replicated.</span></span> <span data-ttu-id="2fc5c-110">Диски можно исключить из репликации.</span><span class="sxs-lookup"><span data-stu-id="2fc5c-110">You can exclude disks from replication.</span></span> <span data-ttu-id="2fc5c-111">Например, репликация может не требоваться для дисков с временными данными или данными, которые обновляются при каждом перезапуске компьютера или приложения (например, pagefile.sys или базы данных tempdb SQL Server).</span><span class="sxs-lookup"><span data-stu-id="2fc5c-111">For example you might not want to replicate disks with temporary data, or data that's refreshed each time a machine or application restarts (for example pagefile.sys or SQL Server tempdb).</span></span> [<span data-ttu-id="2fc5c-112">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="2fc5c-112">Learn more</span></span>](site-recovery-exclude-disk.md)


## <a name="replicate-vms"></a><span data-ttu-id="2fc5c-113">Репликация виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="2fc5c-113">Replicate VMs</span></span>

<span data-ttu-id="2fc5c-114">Включите репликацию для виртуальных машин, сделав следующее.</span><span class="sxs-lookup"><span data-stu-id="2fc5c-114">Enable replication for VMs as follows:</span></span>          

1. <span data-ttu-id="2fc5c-115">Выберите **Репликация приложения** > **Источник**.</span><span class="sxs-lookup"><span data-stu-id="2fc5c-115">Click **Replicate application** > **Source**.</span></span> <span data-ttu-id="2fc5c-116">Когда вы закончите настройку репликации, щелкните **+Реплицировать**, чтобы включить репликацию для дополнительных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="2fc5c-116">After you've set up replication for the first time, you can click **+Replicate** to enable replication for additional machines.</span></span>

    ![Включение репликации](./media/hyper-v-site-walkthrough-enable-replication/enable-replication.png)
2. <span data-ttu-id="2fc5c-118">В колонке **Источник** выберите сайт Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="2fc5c-118">In **Source**, select the Hyper-V site.</span></span> <span data-ttu-id="2fc5c-119">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="2fc5c-119">Then click **OK**.</span></span>
3. <span data-ttu-id="2fc5c-120">В поле **Целевой объект** выберите подписку хранилища и модель отработки отказа (классическую или на основе Resource Manager), которую следует использовать в Azure после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="2fc5c-120">In **Target**, select the vault subscription, and the failover model you want to use in Azure (classic or resource management) after failover.</span></span>
4. <span data-ttu-id="2fc5c-121">Выберите учетную запись хранения, которую нужно использовать.</span><span class="sxs-lookup"><span data-stu-id="2fc5c-121">Select the storage account you want to use.</span></span> <span data-ttu-id="2fc5c-122">Если у вас нет учетной записи, которую можно использовать, [создайте ее](#set-up-an-azure-storage-account).</span><span class="sxs-lookup"><span data-stu-id="2fc5c-122">If you don't have an account you want to use, you can [create one](#set-up-an-azure-storage-account).</span></span> <span data-ttu-id="2fc5c-123">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="2fc5c-123">Then click **OK**.</span></span>
5. <span data-ttu-id="2fc5c-124">Выберите сеть и подсеть Azure, к которой будут подключаться виртуальные машины Azure, созданные после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="2fc5c-124">Select the Azure network and subnet to which Azure VMs will connect when they're created failover.</span></span>

    - <span data-ttu-id="2fc5c-125">Выберите **Настроить сейчас для всех выбранных компьютеров**, чтобы применить параметр сети ко всем защищаемым виртуальным машинам.</span><span class="sxs-lookup"><span data-stu-id="2fc5c-125">To apply the network settings to all machines you enable for replication, select **Configure now for selected machines**.</span></span>
    - <span data-ttu-id="2fc5c-126">Выберите **Отложить настройку**, чтобы выбрать сеть Azure для каждого компьютера.</span><span class="sxs-lookup"><span data-stu-id="2fc5c-126">Select **Configure later** to select the Azure network per machine.</span></span>
    - <span data-ttu-id="2fc5c-127">Если у вас нет сети, которую можно использовать, [создайте ее](#set-up-an-azure-network).</span><span class="sxs-lookup"><span data-stu-id="2fc5c-127">If you don't have a network you want to use, you can [create one](#set-up-an-azure-network).</span></span> <span data-ttu-id="2fc5c-128">Выберите подсеть (если это применимо).</span><span class="sxs-lookup"><span data-stu-id="2fc5c-128">Select a subnet if applicable.</span></span> <span data-ttu-id="2fc5c-129">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="2fc5c-129">Then click **OK**.</span></span>

   ![Включение репликации](./media/hyper-v-site-walkthrough-enable-replication/enable-replication11.png)

6. <span data-ttu-id="2fc5c-131">В разделе **Виртуальные машины** > **Выбор виртуальных машин**, выберите каждую машину, которую нужно реплицировать.</span><span class="sxs-lookup"><span data-stu-id="2fc5c-131">In **Virtual Machines** > **Select virtual machines**, click and select each machine you want to replicate.</span></span> <span data-ttu-id="2fc5c-132">Можно выбрать только те компьютеры, для которых можно включить репликацию.</span><span class="sxs-lookup"><span data-stu-id="2fc5c-132">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="2fc5c-133">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="2fc5c-133">Then click **OK**.</span></span>

    ![Включение репликации](./media/hyper-v-site-walkthrough-enable-replication/enable-replication5-for-exclude-disk.png)

7. <span data-ttu-id="2fc5c-135">В поле **Свойства** > **Настройка свойств**, выберите операционную систему для выбранных виртуальных машин и диск операционной системы.</span><span class="sxs-lookup"><span data-stu-id="2fc5c-135">In **Properties** > **Configure properties**, select the operating system for the selected VMs, and the OS disk.</span></span>
8. <span data-ttu-id="2fc5c-136">Убедитесь, что имя виртуальной машины Azure (имя целевого объекта) соответствует [требованиям к виртуальным машинам Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="2fc5c-136">Verify that the Azure VM name (target name) complies with [Azure virtual machine requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
9. <span data-ttu-id="2fc5c-137">По умолчанию для репликации выбраны все диски виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="2fc5c-137">By default all the disks of the VM are selected for replication.</span></span> <span data-ttu-id="2fc5c-138">Исключите отдельные диски, сняв с них выделение.</span><span class="sxs-lookup"><span data-stu-id="2fc5c-138">Clear disks to exclude them.</span></span>
10. <span data-ttu-id="2fc5c-139">Нажмите кнопку **OK**, чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="2fc5c-139">Click **OK** to save changes.</span></span> <span data-ttu-id="2fc5c-140">Позже можно задать дополнительные свойства.</span><span class="sxs-lookup"><span data-stu-id="2fc5c-140">You can set additional properties later.</span></span>

    ![Включение репликации](./media/hyper-v-site-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

11. <span data-ttu-id="2fc5c-142">Щелкнув **Параметры репликации** > **Настройка параметров репликации**, выберите политику репликации, которую необходимо применить к защищенным виртуальным машинам.</span><span class="sxs-lookup"><span data-stu-id="2fc5c-142">In **Replication settings** > **Configure replication settings**, select the replication policy you want to apply for the protected VMs.</span></span> <span data-ttu-id="2fc5c-143">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="2fc5c-143">Then click **OK**.</span></span> <span data-ttu-id="2fc5c-144">Политику репликации можно изменить, последовательно выбрав **Политики репликации** > имя_политики > **Изменить параметры**.</span><span class="sxs-lookup"><span data-stu-id="2fc5c-144">You can modify the replication policy in **Replication policies** > policy-name > **Edit Settings**.</span></span> <span data-ttu-id="2fc5c-145">Изменения будут применяться к компьютерам, для которых уже выполняется репликация, и к новым компьютерам.</span><span class="sxs-lookup"><span data-stu-id="2fc5c-145">Changes you apply will be used for machines that are already replicating, and new machines.</span></span>


   ![Включение репликации](./media/hyper-v-site-walkthrough-enable-replication/enable-replication7.png)

<span data-ttu-id="2fc5c-147">Ход выполнения задания **включения защиты** можно отслеживать, выбрав **Задания** > **Задания Azure Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="2fc5c-147">You can track progress of the **Enable Protection** job in **Jobs** > **Site Recovery jobs**.</span></span> <span data-ttu-id="2fc5c-148">После выполнения задания **Завершить подготовку защиты** виртуальная машина будет готова к отработке отказа.</span><span class="sxs-lookup"><span data-stu-id="2fc5c-148">After the **Finalize Protection** job runs the machine is ready for failover.</span></span>


## <a name="next-steps"></a><span data-ttu-id="2fc5c-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2fc5c-149">Next steps</span></span>


<span data-ttu-id="2fc5c-150">Перейдите к статье [Шаг 11: Запуск тестовой отработки отказа физических серверов в Azure](hyper-v-site-walkthrough-test-failover.md).</span><span class="sxs-lookup"><span data-stu-id="2fc5c-150">Go to [Step 11: Run a test failover](hyper-v-site-walkthrough-test-failover.md)</span></span>
