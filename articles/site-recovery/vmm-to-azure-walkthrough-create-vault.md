---
title: "aaaSet копирование хранилища для Hyper-V tooAzure репликации (с System Center VMM), с помощью Azure Site Recovery | Документы Microsoft"
description: "Собраны действия hello требуется tooset копии хранилища для Hyper-V tooAzure репликации (с помощью VMM), с помощью Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: b3cd6f03-c33c-406d-91d4-5cba69f79abd
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: f2c90f3c8b0a48db1e57fefd9829d29cffff8d43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-a-vault-for-hyper-v-replication"></a><span data-ttu-id="dbbc3-103">Шаг 7. Настройка хранилища для репликации Hyper-V</span><span class="sxs-lookup"><span data-stu-id="dbbc3-103">Step 7: Set up a vault for Hyper-V replication</span></span>

<span data-ttu-id="dbbc3-104">В этой статье описывается настройка хранилища tooset и укажите, какие действия tooreplicate из папки в локальной среде, с помощью hello tooAzure [Azure Site Recovery](site-recovery-overview.md) в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="dbbc3-104">This article describes how tooset up a vault, and specify what you want tooreplicate from your on-premises location, tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="dbbc3-105">Учет комментарии и вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="dbbc3-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="dbbc3-106">Создание хранилища служб восстановления</span><span class="sxs-lookup"><span data-stu-id="dbbc3-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]



## <a name="select-a-protection-goal"></a><span data-ttu-id="dbbc3-107">Выбор целевого объекта защиты</span><span class="sxs-lookup"><span data-stu-id="dbbc3-107">Select a protection goal</span></span>

<span data-ttu-id="dbbc3-108">Выберите объект tooreplicate, и когда необходимо tooreplicate для.</span><span class="sxs-lookup"><span data-stu-id="dbbc3-108">Select what you want tooreplicate, and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="dbbc3-109">Щелкните **Хранилища служб восстановления** > хранилище.</span><span class="sxs-lookup"><span data-stu-id="dbbc3-109">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="dbbc3-110">В hello ресурсов меню, щелкните **Site Recovery** > **Подготовка инфраструктуры** > **цель защиты**.</span><span class="sxs-lookup"><span data-stu-id="dbbc3-110">In hello Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="dbbc3-111">В **цель защиты**выберите **tooAzure** > **Да, с помощью Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="dbbc3-111">In **Protection goal**, select **tooAzure** > **Yes, with Hyper-V**.</span></span> <span data-ttu-id="dbbc3-112">Выберите **Да** вы tooconfirm nusing VMM.</span><span class="sxs-lookup"><span data-stu-id="dbbc3-112">Select **Yes** tooconfirm you're nusing VMM.</span></span> 

     ![Выбор цели](./media/vmm-to-azure-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a><span data-ttu-id="dbbc3-114">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dbbc3-114">Next steps</span></span>

<span data-ttu-id="dbbc3-115">Go слишком[Step 8: Настройка исходного и конечного](vmm-to-azure-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="dbbc3-115">Go too[Step 8: Set up source and target](vmm-to-azure-walkthrough-source-target.md)</span></span>
