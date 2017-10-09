---
title: "aaaSet копирование хранилища для Hyper-V tooAzure репликации (без System Center VMM), с помощью Azure Site Recovery | Документы Microsoft"
description: "Собраны действия hello требуется tooset копирование хранилище для tooAzure репликации Hyper-V с помощью Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a936b3e2-0dbe-47ac-a98e-5285d96dc786
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: e3ef8758faab36d19d0968d98a23105bed7830f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-a-vault-for-hyper-v-replication"></a><span data-ttu-id="37628-103">Шаг 7. Настройка хранилища для репликации Hyper-V</span><span class="sxs-lookup"><span data-stu-id="37628-103">Step 7: Set up a vault for Hyper-V replication</span></span>

<span data-ttu-id="37628-104">В этой статье описывается настройка хранилища tooset и укажите, какие действия tooreplicate из папки в локальной среде, с помощью hello tooAzure [Azure Site Recovery](site-recovery-overview.md) в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="37628-104">This article describes how tooset up a vault, and specify what you want tooreplicate from your on-premises location, tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="37628-105">Учет комментарии и вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="37628-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="37628-106">Создание хранилища служб восстановления</span><span class="sxs-lookup"><span data-stu-id="37628-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]



## <a name="select-a-protection-goal"></a><span data-ttu-id="37628-107">Выбор целевого объекта защиты</span><span class="sxs-lookup"><span data-stu-id="37628-107">Select a protection goal</span></span>

<span data-ttu-id="37628-108">Выберите объект tooreplicate, и когда необходимо tooreplicate для.</span><span class="sxs-lookup"><span data-stu-id="37628-108">Select what you want tooreplicate, and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="37628-109">Щелкните **Хранилища служб восстановления** > хранилище.</span><span class="sxs-lookup"><span data-stu-id="37628-109">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="37628-110">В hello ресурсов меню, щелкните **Site Recovery** > **Подготовка инфраструктуры** > **цель защиты**.</span><span class="sxs-lookup"><span data-stu-id="37628-110">In hello Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="37628-111">В **цель защиты**выберите **tooAzure** > **Да, с помощью Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="37628-111">In **Protection goal**, select **tooAzure** > **Yes, with Hyper-V**.</span></span> <span data-ttu-id="37628-112">Выберите **нет** tooconfirm, вы не используете VMM.</span><span class="sxs-lookup"><span data-stu-id="37628-112">Select **No** tooconfirm you're not using VMM.</span></span> 

    ![Выбор цели](./media/hyper-v-site-walkthrough-create-vault/choose-goals2.png)



## <a name="next-steps"></a><span data-ttu-id="37628-114">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="37628-114">Next steps</span></span>

<span data-ttu-id="37628-115">Go слишком[Step 8: Настройка исходного и конечного](hyper-v-site-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="37628-115">Go too[Step 8: Set up source and target](hyper-v-site-walkthrough-source-target.md)</span></span>
