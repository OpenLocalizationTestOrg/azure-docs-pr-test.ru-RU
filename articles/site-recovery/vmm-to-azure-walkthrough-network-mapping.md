---
title: "aaaConfigure сетевое сопоставление для репликации виртуальных машин Hyper-V в VMM облаков tooAzure с Azure Site Recovery | Документы Microsoft"
description: "Описывает, каким образом tooconfigure сетевое сопоставление, при репликации виртуальных машин Hyper-V в VMM облаков tooAzure с Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 081a9fdb0ffa4114099e9bcb9c1b1e43ad26ecbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-configure-network-mapping-for-hyper-v-replication-with-vmm-tooazure"></a><span data-ttu-id="56286-103">Шаг 9: Настройка сопоставления сетей для Hyper-V tooAzure репликации (с помощью VMM)</span><span class="sxs-lookup"><span data-stu-id="56286-103">Step 9: Configure network mapping for Hyper-V replication (with VMM) tooAzure</span></span>

<span data-ttu-id="56286-104">После настройки hello [исходной и целевой настройки репликации](vmm-to-azure-walkthrough-source-target.md), используйте этот toomap статьи tooconfigure сетевого сопоставления между локальными сетями виртуальной Машины VMM и сетями Azure.</span><span class="sxs-lookup"><span data-stu-id="56286-104">After you set up hello [source and target replication settings](vmm-to-azure-walkthrough-source-target.md), use this article tooconfigure network mapping toomap between on-premises VMM VM networks, and Azure networks.</span></span>

<span data-ttu-id="56286-105">Учет комментарии и вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="56286-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="56286-106">Перед началом</span><span class="sxs-lookup"><span data-stu-id="56286-106">Before you start</span></span>

- <span data-ttu-id="56286-107">Узнайте о [сопоставлении сети](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span><span class="sxs-lookup"><span data-stu-id="56286-107">Learn about [network mapping](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span></span>
- <span data-ttu-id="56286-108">[Подготовьте VMM к сопоставлению сети](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping).</span><span class="sxs-lookup"><span data-stu-id="56286-108">[Prepare VMM for network mapping](vmm-to-azure-walkthrough-network.md#prepare-vmm-for-network-mapping).</span></span> 
- <span data-ttu-id="56286-109">Убедитесь, виртуальные машины на сервере VMM hello tooa подключенной сети виртуальной Машины, и что вы создали по крайней мере одна виртуальная сеть Azure.</span><span class="sxs-lookup"><span data-stu-id="56286-109">Verify that virtual machines on hello VMM server are connected tooa VM network, and that you've created at least one Azure virtual network.</span></span> <span data-ttu-id="56286-110">Несколько сетей виртуальной Машины может быть сопоставленных tooa одной сетью Azure.</span><span class="sxs-lookup"><span data-stu-id="56286-110">Multiple VM networks can be mapped tooa single Azure network.</span></span>

## <a name="configure-mapping"></a><span data-ttu-id="56286-111">Настройка сопоставления</span><span class="sxs-lookup"><span data-stu-id="56286-111">Configure mapping</span></span>

<span data-ttu-id="56286-112">Настройте сопоставление следующим образом:</span><span class="sxs-lookup"><span data-stu-id="56286-112">Configure mapping as follows:</span></span>

1. <span data-ttu-id="56286-113">В **инфраструктура Site Recovery** > **сетевого сопоставления** > **сетевое сопоставление**, нажмите кнопку hello **+ сетевое сопоставление**  значок.</span><span class="sxs-lookup"><span data-stu-id="56286-113">In **Site Recovery Infrastructure** > **Network mappings** > **Network Mapping**, click hello **+Network Mapping** icon.</span></span>

    ![Сетевое сопоставление](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping1.png)
2. <span data-ttu-id="56286-115">В **добавить сопоставление сети**выберите hello исходном сервере VMM, и **Azure** как целевой hello.</span><span class="sxs-lookup"><span data-stu-id="56286-115">In **Add network mapping**, select hello source VMM server, and **Azure** as hello target.</span></span>
3. <span data-ttu-id="56286-116">Проверка подписки hello и модель развертывания hello после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="56286-116">Verify hello subscription and hello deployment model after failover.</span></span>
4. <span data-ttu-id="56286-117">В **Исходная сеть**выберите hello исходную сеть виртуальных Машин в локальной среде требуется toomap из списка hello, связанные с сервером VMM hello.</span><span class="sxs-lookup"><span data-stu-id="56286-117">In **Source network**, select hello source on-premises VM network you want toomap from hello list associated with hello VMM server.</span></span>
5. <span data-ttu-id="56286-118">В **целевой сети**, выберите hello реплик виртуальных машин Azure будет находиться во время создания сети Azure.</span><span class="sxs-lookup"><span data-stu-id="56286-118">In **Target network**, select hello Azure network in which replica Azure VMs will be located when they're created.</span></span> <span data-ttu-id="56286-119">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="56286-119">Then click **OK**.</span></span>

    ![Сетевое сопоставление](./media/vmm-to-azure-walkthrough-network-mapping/network-mapping2.png)

<span data-ttu-id="56286-121">Когда начинается сопоставление сетей, происходит следующее:</span><span class="sxs-lookup"><span data-stu-id="56286-121">Here's what happens when network mapping begins:</span></span>

* <span data-ttu-id="56286-122">Существующих виртуальных машин в исходной сети VM hello, подключенных toohello целевой сети, когда начинает сопоставление.</span><span class="sxs-lookup"><span data-stu-id="56286-122">Existing VMs on hello source VM network are connected toohello target network when mapping begins.</span></span> <span data-ttu-id="56286-123">Новые виртуальные машины подключенных toohello исходную сеть виртуальных Машин подключены toohello сопоставлено сетью Azure при выполнении репликации.</span><span class="sxs-lookup"><span data-stu-id="56286-123">New VMs connected toohello source VM network are connected toohello mapped Azure network when replication occurs.</span></span>
* <span data-ttu-id="56286-124">Можно изменить существующее сопоставление сети, виртуальные машины реплики подключаться с использованием новых параметров hello.</span><span class="sxs-lookup"><span data-stu-id="56286-124">If you modify an existing network mapping, replica virtual machines connect using hello new settings.</span></span>
* <span data-ttu-id="56286-125">Если hello целевая сеть содержит несколько подсетей, и одна из этих подсетей имеет hello находится совпадает с именем подсети, на какие hello исходной виртуальной машины, то виртуальная машина реплики hello подключается toothat целевой подсети после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="56286-125">If hello target network has multiple subnets, and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine connects toothat target subnet after failover.</span></span>
* <span data-ttu-id="56286-126">Если никакой целевой подсети с совпадающим именем виртуальной машины hello подключается toohello первой подсети в сети hello.</span><span class="sxs-lookup"><span data-stu-id="56286-126">If there’s no target subnet with a matching name, hello virtual machine connects toohello first subnet in hello network.</span></span>



## <a name="next-steps"></a><span data-ttu-id="56286-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="56286-127">Next steps</span></span>

<span data-ttu-id="56286-128">Go слишком[шаг 10: Создание политики репликации](vmm-to-azure-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="56286-128">Go too[Step 10: Create a replication policy](vmm-to-azure-walkthrough-replication.md)</span></span>
