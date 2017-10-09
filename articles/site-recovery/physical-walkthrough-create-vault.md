---
title: "aaaSet копирование хранилища для tooAzure репликации физического сервера с помощью Azure Site Recovery | Документы Microsoft"
description: "Собраны действия hello необходимо tooset копирование tooAzure физических серверов tooreplicate хранилище, с помощью Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99f2605-f417-4995-be77-5323136b814f
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 988928e3ece31116823f132cc39223fe44443468
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-a-vault-for-physical-server-replication-tooazure"></a><span data-ttu-id="28973-103">Шаг 6: Настройка хранилища для репликации tooAzure физического сервера</span><span class="sxs-lookup"><span data-stu-id="28973-103">Step 6: Set up a vault for physical server replication tooAzure</span></span>


<span data-ttu-id="28973-104">В этой статье описывается как tooset копии хранилища.</span><span class="sxs-lookup"><span data-stu-id="28973-104">This article describes how tooset up a vault.</span></span> <span data-ttu-id="28973-105">Создание хранилища hello и укажите, какие действия tooreplicate из вашего tooAzure расположения в локальной среде, с помощью hello [Azure Site Recovery](site-recovery-overview.md) в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="28973-105">You create hello vault, and specify what you want tooreplicate from your on-premises location tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="28973-106">Учет комментарии и вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="28973-106">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="28973-107">Создание хранилища служб восстановления</span><span class="sxs-lookup"><span data-stu-id="28973-107">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a><span data-ttu-id="28973-108">Выбор целевого объекта защиты</span><span class="sxs-lookup"><span data-stu-id="28973-108">Select a protection goal</span></span>

<span data-ttu-id="28973-109">Выберите объект tooreplicate, и когда необходимо tooreplicate для.</span><span class="sxs-lookup"><span data-stu-id="28973-109">Select what you want tooreplicate, and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="28973-110">Щелкните **Хранилища служб восстановления** > хранилище.</span><span class="sxs-lookup"><span data-stu-id="28973-110">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="28973-111">В hello ресурсов меню, щелкните **Site Recovery** > **Подготовка инфраструктуры** > **цель защиты**.</span><span class="sxs-lookup"><span data-stu-id="28973-111">In hello Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="28973-112">В **цель защиты**выберите **tooAzure** > **не виртуализированных, другие**.</span><span class="sxs-lookup"><span data-stu-id="28973-112">In **Protection goal**, select **tooAzure** > **Not virtualized/Other**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="28973-113">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="28973-113">Next steps</span></span>

<span data-ttu-id="28973-114">Go слишком[шаг 7: Настройка исходного и конечного](physical-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="28973-114">Go too[Step 7: Set up source and target](physical-walkthrough-source-target.md)</span></span>
