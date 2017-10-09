---
title: "aaaMap сетей для виртуальных Машин Hyper-V репликации tooa вторичного сайта с помощью Azure Site Recovery | Документы Microsoft"
description: "Описывает, каким образом toomap сети при репликации виртуальных машин Hyper-V tooa вторичный сайт VMM с помощью Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 461b7c1c-ef61-4005-aeec-2324e727a3d0
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: d4f621df4ce08ae055bc6809daea0b71b76754ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-map-networks-for-hyper-v-vm-replication-tooa-secondary-site"></a><span data-ttu-id="4199c-103">Шаг 7: Сопоставление сетей для виртуальных Машин Hyper-V репликации tooa вторичного сайта</span><span class="sxs-lookup"><span data-stu-id="4199c-103">Step 7: Map networks for Hyper-V VM replication tooa secondary site</span></span>


<span data-ttu-id="4199c-104">После настройки [источника и целевых параметров](vmm-to-vmm-walkthrough-source-target.md) для репликации Hyper-V виртуальных машин (ВМ) tooa вторичный сайт, диспетчер виртуальных машин System Center (VMM), использовать в этой статье tooconfigure сетевое сопоставление для Hyper-V виртуального tooa репликации машины (VM) вторичного сайта, с помощью [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4199c-104">After setting up [source and target settings](vmm-to-vmm-walkthrough-source-target.md) for replicating Hyper-V virtual machines (VMs) tooa secondary System Center Virtual Machine Manager (VMM) site, use this article tooconfigure network mapping for Hyper-V virtual machine (VM) replication tooa secondary site, using  [Azure Site Recovery](site-recovery-overview.md).</span></span>

<span data-ttu-id="4199c-105">После считывания в этой статье, отправлять любые комментарии, внизу hello, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="4199c-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="4199c-106">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="4199c-106">Before you start</span></span>

- <span data-ttu-id="4199c-107">Прежде чем начинать работу, изучите сведения о [сетевом сопоставлении](vmm-to-vmm-walkthrough-network.md#network-mapping-overview).</span><span class="sxs-lookup"><span data-stu-id="4199c-107">Learn about [network mapping](vmm-to-vmm-walkthrough-network.md#network-mapping-overview) before you start.</span></span>
- <span data-ttu-id="4199c-108">Убедитесь, что виртуальные машины на серверах VMM tooa подключенной сети виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="4199c-108">Verify that virtual machines on VMM servers are connected tooa VM network.</span></span>

## <a name="configure-network-mapping"></a><span data-ttu-id="4199c-109">Настройка сетевого сопоставления</span><span class="sxs-lookup"><span data-stu-id="4199c-109">Configure network mapping</span></span>

1. <span data-ttu-id="4199c-110">В области **Сетевое сопоставление** > **Сетевые сопоставления** щелкните **+Network Mapping** (+Сетевое сопоставление).</span><span class="sxs-lookup"><span data-stu-id="4199c-110">In **Network Mapping** > **Network mappings**, click **+Network Mapping**.</span></span>
2. <span data-ttu-id="4199c-111">В **добавить сопоставление сети** выберите hello исходном и целевом серверах VMM.</span><span class="sxs-lookup"><span data-stu-id="4199c-111">In **Add network mapping** tab, select hello source and target VMM servers.</span></span> <span data-ttu-id="4199c-112">извлекаются Hello сетей виртуальных Машин, связанные с серверами VMM hello.</span><span class="sxs-lookup"><span data-stu-id="4199c-112">hello VM networks associated with hello VMM servers are retrieved.</span></span>
3. <span data-ttu-id="4199c-113">В **Исходная сеть**выберите hello сети, которую требуется toouse из списка hello сетей виртуальных Машин, связанные с hello первичного сервера VMM.</span><span class="sxs-lookup"><span data-stu-id="4199c-113">In **Source network**, select hello network you want toouse from hello list of VM networks associated with hello primary VMM server.</span></span>
4. <span data-ttu-id="4199c-114">В **целевой сети**выберите hello сети, которую требуется toouse на вторичном сервере VMM hello.</span><span class="sxs-lookup"><span data-stu-id="4199c-114">In **Target network**, select hello network you want toouse on hello secondary VMM server.</span></span> <span data-ttu-id="4199c-115">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="4199c-115">Then click **OK**.</span></span>

    ![Сетевое сопоставление](./media/vmm-to-vmm-walkthrough-network-mapping/network-mapping2.png)

<span data-ttu-id="4199c-117">Когда начинается сопоставление сетей, происходит следующее:</span><span class="sxs-lookup"><span data-stu-id="4199c-117">Here's what happens when network mapping begins:</span></span>

* <span data-ttu-id="4199c-118">Все существующие реплики виртуальных машин, соответствующих toohello исходную сеть виртуальных Машин будет подключенных toohello целевой сети ВМ.</span><span class="sxs-lookup"><span data-stu-id="4199c-118">Any existing replica virtual machines that correspond toohello source VM network will be connected toohello target VM network.</span></span>
* <span data-ttu-id="4199c-119">Новые виртуальные машины, подключенной toohello исходную сеть виртуальных Машин будет подключенных toohello целевой сопоставленные сетевые после репликации.</span><span class="sxs-lookup"><span data-stu-id="4199c-119">New virtual machines that are connected toohello source VM network will be connected toohello target mapped network after replication.</span></span>
* <span data-ttu-id="4199c-120">При изменении существующего сопоставления с новой сети, виртуальные машины реплики будут подключены с использованием новых параметров hello.</span><span class="sxs-lookup"><span data-stu-id="4199c-120">If you modify an existing mapping with a new network, replica virtual machines will be connected using hello new settings.</span></span>
* <span data-ttu-id="4199c-121">Если hello целевая сеть содержит несколько подсетей, и одна из этих подсетей имеет hello находится совпадает с именем подсети, на какие hello исходной виртуальной машины, а затем hello реплики виртуальной машины после отработки отказа будет подключенных toothat целевой подсети.</span><span class="sxs-lookup"><span data-stu-id="4199c-121">If hello target network has multiple subnets and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after failover.</span></span> <span data-ttu-id="4199c-122">Если никакой целевой подсети с совпадающим именем, hello виртуальная машина будет подключенных toohello первой подсети в сети hello.</span><span class="sxs-lookup"><span data-stu-id="4199c-122">If there’s no target subnet with a matching name, hello virtual machine will be connected toohello first subnet in hello network.</span></span>



## <a name="next-steps"></a><span data-ttu-id="4199c-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4199c-123">Next steps</span></span>

<span data-ttu-id="4199c-124">Go слишком[Step 8: настроить политику репликации](vmm-to-vmm-walkthrough-replication.md).</span><span class="sxs-lookup"><span data-stu-id="4199c-124">Go too[Step 8: Configure a replication policy](vmm-to-vmm-walkthrough-replication.md).</span></span>
