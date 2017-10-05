---
title: "Настройка хранилища для репликации виртуальной машины Azure между регионами с помощью Azure Site Recovery | Документация Майкрософт"
description: "В этой статье кратко описаны шаги по настройке хранилища для репликации Azure между регионами Azure с помощью Azure Site Recovery."
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
ms.openlocfilehash: e03d17992ee0b12049636e40188950bcc4a6f31e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="step-4-set-up-a-vault-for-azure-to-azure-replication"></a><span data-ttu-id="b98a1-103">Шаг 4. Настройка хранилища для репликации из Azure в Azure</span><span class="sxs-lookup"><span data-stu-id="b98a1-103">Step 4: Set up a vault for Azure to Azure replication</span></span>

<span data-ttu-id="b98a1-104">После [планирования сетей](azure-to-azure-walkthrough-network.md) вы можете воспользоваться этой статьей, чтобы настроить хранилище для виртуальных машин Azure, реплицируемых в другой регион Azure, с помощью службы [Azure Site Recovery](site-recovery-overview.md) на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="b98a1-104">After [planning networks](azure-to-azure-walkthrough-network.md), use this article to set up a vault, for Azure virtual machines (VMs) replicating to another Azure region, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

- <span data-ttu-id="b98a1-105">После выполнения инструкций в этой статье у вас будет настроенное хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="b98a1-105">When you finish the article, you should have a Recovery Services vault set up.</span></span>
- <span data-ttu-id="b98a1-106">Все комментарии можно добавить в конце этой статьи. Вопросы можно задать на [форуме по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="b98a1-106">Post any comments at the bottom of this article, or ask questions in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>



>[!NOTE]
>
> <span data-ttu-id="b98a1-107">Репликация виртуальных машин Azure сейчас доступна в режиме предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="b98a1-107">Azure VM replication is currently in preview.</span></span>




## <a name="create-a-vault"></a><span data-ttu-id="b98a1-108">Создание хранилища</span><span class="sxs-lookup"><span data-stu-id="b98a1-108">Create a vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> <span data-ttu-id="b98a1-109">Советуем создавать хранилище служб восстановления в расположении, куда вы хотите реплицировать ваши виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="b98a1-109">We recommend that you create the Recovery Services vault in the location where you want your VMs to replicate.</span></span> <span data-ttu-id="b98a1-110">Например, если целевое расположение центральная часть США, создайте хранилище в **центральной части США**.</span><span class="sxs-lookup"><span data-stu-id="b98a1-110">For example, if your target location is the central US, create the vault in **Central US**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b98a1-111">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b98a1-111">Next steps</span></span>

<span data-ttu-id="b98a1-112">Перейдите к статье [Шаг 5. Включение репликации для виртуальных машин Azure](azure-to-azure-walkthrough-enable-replication.md).</span><span class="sxs-lookup"><span data-stu-id="b98a1-112">Go to [Step 5: Enable replication](azure-to-azure-walkthrough-enable-replication.md)</span></span>
