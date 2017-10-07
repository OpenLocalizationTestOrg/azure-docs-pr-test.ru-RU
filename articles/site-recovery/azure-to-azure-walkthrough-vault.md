---
title: "aaaSet копирование хранилища для виртуальной Машины Azure repliction между регионами с Azure Site Recovery | Документы Microsoft"
description: "Собраны действия hello необходимо tooset копии хранилища Azure репликации между регионах Azure, с помощью Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 40472189-3d80-4963-b175-8bddcbc2f61f
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: 9959c59c7ea57114763f13bf060404ddd267ba80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-set-up-a-vault-for-azure-tooazure-replication"></a><span data-ttu-id="cf525-103">Шаг 4: Настройка хранилища Azure tooAzure репликации</span><span class="sxs-lookup"><span data-stu-id="cf525-103">Step 4: Set up a vault for Azure tooAzure replication</span></span>

<span data-ttu-id="cf525-104">После [Планирование сетей](azure-to-azure-walkthrough-network.md), использование этой статьи tooset копии хранилища для виртуальных машин (ВМ) Azure репликации tooanother регион Azure, с помощью hello [Azure Site Recovery](site-recovery-overview.md) в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="cf525-104">After [planning networks](azure-to-azure-walkthrough-network.md), use this article tooset up a vault, for Azure virtual machines (VMs) replicating tooanother Azure region, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

- <span data-ttu-id="cf525-105">Завершив hello статьи, необходимо настроить хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="cf525-105">When you finish hello article, you should have a Recovery Services vault set up.</span></span>
- <span data-ttu-id="cf525-106">Отправлять все комментарии hello нижней части этой статьи, или задать вопросы в hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="cf525-106">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



>[!NOTE]
>
> <span data-ttu-id="cf525-107">Репликация виртуальных машин Azure сейчас доступна в режиме предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="cf525-107">Azure VM replication is currently in preview.</span></span>




## <a name="create-a-vault"></a><span data-ttu-id="cf525-108">Создание хранилища</span><span class="sxs-lookup"><span data-stu-id="cf525-108">Create a vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> <span data-ttu-id="cf525-109">Рекомендуется создать хранилище служб восстановления hello в hello место хранения вашей tooreplicate виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="cf525-109">We recommend that you create hello Recovery Services vault in hello location where you want your VMs tooreplicate.</span></span> <span data-ttu-id="cf525-110">Например, если в целевом расположении hello центральный нам, создайте хранилище hello в **центральной части США**.</span><span class="sxs-lookup"><span data-stu-id="cf525-110">For example, if your target location is hello central US, create hello vault in **Central US**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="cf525-111">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cf525-111">Next steps</span></span>

<span data-ttu-id="cf525-112">Go слишком[шаг 5: включение репликации](azure-to-azure-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="cf525-112">Go too[Step 5: Enable replication](azure-to-azure-walkthrough-enable-replication.md)</span></span>
