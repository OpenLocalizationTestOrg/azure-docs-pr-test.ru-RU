---
title: "Настройка политики репликации для репликации виртуальных машин VMware (с VMM) в Azure с помощью Azure Site Recovery | Документация Майкрософт"
description: "Здесь описывается, как настроить политику репликации для репликации виртуальных машин Hyper-V (с VMM) в Azure с помощью Azure Site Recovery."
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
ms.openlocfilehash: 592e1c3f647e5b1f1d9aa776657e8f89b60349e1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="step-10-set-up-a-replication-policy-for-hyper-v-vm-replication-with-vmm-to-azure"></a><span data-ttu-id="7530b-103">Шаг 10. Настройка политики репликации для репликации виртуальных машин Hyper-V (с VMM) в Azure</span><span class="sxs-lookup"><span data-stu-id="7530b-103">Step 10: Set up a replication policy for Hyper-V VM replication (with VMM) to Azure</span></span>


<span data-ttu-id="7530b-104">После настройки [сетевого сопоставления](vmm-to-azure-walkthrough-network-mapping.md) воспользуйтесь сведениями в этой статье, чтобы настроить политику репликации для репликации локальных виртуальных машин Hyper-V, управляемых в облаках System Center Virtual Machine Manager (VMM), в Azure с помощью службы [Azure Site Recovery](site-recovery-overview.md) на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="7530b-104">After setting up [network mapping](vmm-to-azure-walkthrough-network-mapping.md), use this article to configure a replication policy T\to replicate on-premises Hyper-V virtual machines managed in System Center Virtual Machine Manager (VMM) clouds to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="7530b-105">Любые комментарии, которые возникнут после прочтения этой статьи, можно добавить в конце этой страницы или на [форуме по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="7530b-105">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



## <a name="create-a-policy"></a><span data-ttu-id="7530b-106">Создание политики</span><span class="sxs-lookup"><span data-stu-id="7530b-106">Create a policy</span></span>

1. <span data-ttu-id="7530b-107">Чтобы создать политику репликации, выберите **Подготовка инфраструктуры** > **Параметры репликации** > **Создание и связывание**.</span><span class="sxs-lookup"><span data-stu-id="7530b-107">To create a new replication policy, click **Prepare infrastructure** > **Replication Settings** > **+Create and associate**.</span></span>

    ![Сеть](./media/vmm-to-azure-walkthrough-replication/gs-replication.png)
2. <span data-ttu-id="7530b-109">На странице **Создать и связать политику**укажите имя политики.</span><span class="sxs-lookup"><span data-stu-id="7530b-109">In **Create and associate policy**, specify a policy name.</span></span>
3. <span data-ttu-id="7530b-110">В раскрывающемся списке **Частота копирования**выберите периодичность репликации изменений данных после начальной репликации (каждые 30 секунд, 5 или 15 минут).</span><span class="sxs-lookup"><span data-stu-id="7530b-110">In **Copy frequency**, specify how often you want to replicate delta data after the initial replication (every 30 seconds, 5 or 15 minutes).</span></span>

    > [!NOTE]
    >  <span data-ttu-id="7530b-111">Частота 30 секунд не поддерживается при репликации в хранилище класса Premium.</span><span class="sxs-lookup"><span data-stu-id="7530b-111">A 30 second frequency isn't supported when replicating to premium storage.</span></span> <span data-ttu-id="7530b-112">Это связано с ограничением в 100 моментальных снимков на большой двоичный объект, которые можно сохранить в хранилище уровня "Премиум".</span><span class="sxs-lookup"><span data-stu-id="7530b-112">The limitation is determined by the number of snapshots per blob (100) supported by premium storage.</span></span> [<span data-ttu-id="7530b-113">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="7530b-113">Learn more</span></span>](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)

4. <span data-ttu-id="7530b-114">В поле **Хранение точки восстановления**укажите продолжительность периода хранения для каждой точки восстановления (в часах).</span><span class="sxs-lookup"><span data-stu-id="7530b-114">In **Recovery point retention**, specify in hours how long the retention window will be for each recovery point.</span></span> <span data-ttu-id="7530b-115">Защищенные компьютеры будут восстанавливаться до любой точки в пределах этого периода.</span><span class="sxs-lookup"><span data-stu-id="7530b-115">Protected machines can be recovered to any point within a window.</span></span>
5. <span data-ttu-id="7530b-116">В поле **Периодичность создания моментальных снимков с согласованием приложений** укажите, как часто (от 1 до 12 часов) будут создаваться точки восстановления, содержащие согласованные с приложениями моментальные снимки.</span><span class="sxs-lookup"><span data-stu-id="7530b-116">In **App-consistent snapshot frequency**, specify how frequently (1-12 hours) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="7530b-117">Hyper-V использует два типа резервного копирования: стандартное резервное копирование, обеспечивающее создание добавочных резервных копий всей виртуальной машины, и соответствующие приложению моментальные снимки, обеспечивающие создание моментального снимка данных приложений в виртуальной машине на момент времени.</span><span class="sxs-lookup"><span data-stu-id="7530b-117">Hyper-V uses two types of snapshots — a standard snapshot that provides an incremental snapshot of the entire virtual machine, and an application-consistent snapshot that takes a point-in-time snapshot of the application data inside the virtual machine.</span></span> <span data-ttu-id="7530b-118">Функция моментальных снимков, соответствующих приложению, использует службу теневого копирования томов (VSS), чтобы гарантировать согласованное состояние приложений на момент создания снимка.</span><span class="sxs-lookup"><span data-stu-id="7530b-118">Application-consistent snapshots use Volume Shadow Copy Service (VSS) to ensure that applications are in a consistent state when the snapshot is taken.</span></span> <span data-ttu-id="7530b-119">Примечание. Включение моментальных снимков, соответствующих приложению, влияет на производительность приложений, выполняющихся на исходных виртуальных машинах.</span><span class="sxs-lookup"><span data-stu-id="7530b-119">Note that if you enable application-consistent snapshots, it will affect the performance of applications running on source virtual machines.</span></span> <span data-ttu-id="7530b-120">Заданное значение должно быть меньше числа настроенных дополнительных точек восстановления.</span><span class="sxs-lookup"><span data-stu-id="7530b-120">Ensure that the value you set is less than the number of additional recovery points you configure.</span></span>
6. <span data-ttu-id="7530b-121">Укажите необходимые данные в поле **Время запуска начальной репликации**.</span><span class="sxs-lookup"><span data-stu-id="7530b-121">In **Initial replication start time**, indicate when to start the initial replication.</span></span> <span data-ttu-id="7530b-122">При репликации используется полоса пропускания Интернета. Поэтому проведение репликации нужно запланировать на свободное от работы время.</span><span class="sxs-lookup"><span data-stu-id="7530b-122">The replication occurs over your internet bandwidth so you might want to schedule it outside your busy hours.</span></span>
7. <span data-ttu-id="7530b-123">В области **Шифровать данные, хранящиеся в Azure**нажмите соответствующую кнопку.</span><span class="sxs-lookup"><span data-stu-id="7530b-123">In **Encrypt data stored on Azure**, specify whether to encrypt at rest data in Azure storage.</span></span> <span data-ttu-id="7530b-124">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="7530b-124">Then click **OK**.</span></span>

    ![Политика репликации](./media/vmm-to-azure-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="7530b-126">При создании политики она автоматически сопоставляется с облаком VMM.</span><span class="sxs-lookup"><span data-stu-id="7530b-126">When you create a new policy it's automatically associated with the VMM cloud.</span></span> <span data-ttu-id="7530b-127">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="7530b-127">Click **OK**.</span></span> <span data-ttu-id="7530b-128">С этой политикой репликации можно сопоставить дополнительные облака VMM (и виртуальные машины, содержащиеся в них). Для этого выберите **Репликация** > имя политики > **Associate VMM Cloud** (Сопоставить облако VMM).</span><span class="sxs-lookup"><span data-stu-id="7530b-128">You can associate additional VMM clouds (and the VMs in them) with this replication policy in **Replication** > policy name > **Associate VMM Cloud**.</span></span>

    ![Политика репликации](./media/vmm-to-azure-walkthrough-replication/policy-associate.png)



## <a name="next-steps"></a><span data-ttu-id="7530b-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7530b-130">Next steps</span></span>

<span data-ttu-id="7530b-131">Перейдите к разделу [Шаг 11. Включение репликации](vmm-to-azure-walkthrough-enable-replication.md).</span><span class="sxs-lookup"><span data-stu-id="7530b-131">Go to [Step 11: Enable replication](vmm-to-azure-walkthrough-enable-replication.md)</span></span>
