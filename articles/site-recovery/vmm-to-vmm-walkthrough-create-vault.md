---
title: "aaaCreate хранилища для Hyper-V репликации tooa вторичного сайта с помощью Azure Site Recovery | Документы Microsoft"
description: "Описывает, как toocreate хранилище при репликации виртуальных машин Hyper-V tooa получателей System Center VMM сайта с Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: ff65dbfb-cb26-410e-ab48-76971625db08
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 96ee09cbf2376a5089b9efa09dc7ab3fb7d472cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-create-a-vault-for-hyper-v-replication-tooa-secondary-site"></a><span data-ttu-id="a5370-103">Шаг 5: Создание хранилища для Hyper-V репликации tooa вторичного сайта</span><span class="sxs-lookup"><span data-stu-id="a5370-103">Step 5: Create a vault for Hyper-V replication tooa secondary site</span></span>

<span data-ttu-id="a5370-104">После подготовки локальной [серверы диспетчера виртуальных машин System Center (VMM) и узлы Hyper-V и кластеры](vmm-to-vmm-walkthrough-vmm-hyper-v.md) для Hyper-V репликации tooa вторичного сайта с помощью [Azure Site Recovery](site-recovery-overview.md), можно создать Хранилище служб восстановления и выберите hello сценарий репликации.</span><span class="sxs-lookup"><span data-stu-id="a5370-104">After preparing on-premises [System Center Virtual Machine Manager (VMM) servers and Hyper-V hosts/clusters](vmm-to-vmm-walkthrough-vmm-hyper-v.md) for Hyper-V replication tooa secondary site using [Azure Site Recovery](site-recovery-overview.md), you can create a Recovery Services vault, and select hello replication scenario.</span></span>

<span data-ttu-id="a5370-105">После считывания в этой статье, отправлять любые комментарии, внизу hello, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="a5370-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="a5370-106">Создание хранилища служб восстановления</span><span class="sxs-lookup"><span data-stu-id="a5370-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]


## <a name="choose-a-protection-goal"></a><span data-ttu-id="a5370-107">Выбор цели защиты</span><span class="sxs-lookup"><span data-stu-id="a5370-107">Choose a protection goal</span></span>

<span data-ttu-id="a5370-108">Выберите том, что необходимо tooreplicate, а также место tooreplicate для.</span><span class="sxs-lookup"><span data-stu-id="a5370-108">Select what you want tooreplicate and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="a5370-109">Щелкните **Site Recovery** > **Шаг 1. Подготовка инфраструктуры** > **Цель защиты**.</span><span class="sxs-lookup"><span data-stu-id="a5370-109">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>
2. <span data-ttu-id="a5370-110">Выберите **сайта toorecovery**и выберите **Да, с помощью Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="a5370-110">Select **toorecovery site**, and select **Yes, with Hyper-V**.</span></span>
3. <span data-ttu-id="a5370-111">Выберите **Да** tooindicate вы используете узлов Hyper-V hello toomanage VMM.</span><span class="sxs-lookup"><span data-stu-id="a5370-111">Select **Yes** tooindicate you're using VMM toomanage hello Hyper-V hosts.</span></span>
4. <span data-ttu-id="a5370-112">Выберите **Да**, если используется дополнительный сервер VMM.</span><span class="sxs-lookup"><span data-stu-id="a5370-112">Select **Yes** if you have a secondary VMM server.</span></span> <span data-ttu-id="a5370-113">Если вы развертываете репликацию между облаками, развернутыми на одном сервере VMM, щелкните **Нет**.</span><span class="sxs-lookup"><span data-stu-id="a5370-113">If you're deploying replication between clouds on a single VMM server, click **No**.</span></span> <span data-ttu-id="a5370-114">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a5370-114">Then click **OK**.</span></span>

    ![Выбор цели](./media/vmm-to-vmm-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a><span data-ttu-id="a5370-116">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a5370-116">Next steps</span></span>

<span data-ttu-id="a5370-117">Go слишком[шаг 6: Настройка hello репликации исходной и целевой](vmm-to-vmm-walkthrough-source-target.md).</span><span class="sxs-lookup"><span data-stu-id="a5370-117">Go too[Step 6: Set up hello replication source and target](vmm-to-vmm-walkthrough-source-target.md).</span></span>
