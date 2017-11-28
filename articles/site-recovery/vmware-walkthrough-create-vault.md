---
title: "aaaSet копирование хранилища для VMware tooAzure репликации, с помощью Azure Site Recovery | Документы Microsoft"
description: "Собраны действия hello требуется tooset копирование хранилище для tooAzure репликации VMware с помощью Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8bce940e-f19f-4418-8360-aee7b073519a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 8a7755a6c9a3f55f241c615e425285bc4b782493
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-a-vault-for-vmware-replication-tooazure"></a><span data-ttu-id="ee1fa-103">Шаг 7: Настройка хранилища для VMware tooAzure репликации</span><span class="sxs-lookup"><span data-stu-id="ee1fa-103">Step 7: Set up a vault for VMware replication tooAzure</span></span>


<span data-ttu-id="ee1fa-104">В этой статье описывается настройка хранилища tooset и укажите, какие действия tooreplicate из папки в локальной среде, с помощью hello tooAzure [Azure Site Recovery](site-recovery-overview.md) в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ee1fa-104">This article describes how tooset up a vault, and specify what you want tooreplicate from your on-premises location, tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="ee1fa-105">Учет комментарии и вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="ee1fa-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="ee1fa-106">Создание хранилища служб восстановления</span><span class="sxs-lookup"><span data-stu-id="ee1fa-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a><span data-ttu-id="ee1fa-107">Выбор целевого объекта защиты</span><span class="sxs-lookup"><span data-stu-id="ee1fa-107">Select a protection goal</span></span>

<span data-ttu-id="ee1fa-108">Выберите объект tooreplicate, и когда необходимо tooreplicate для.</span><span class="sxs-lookup"><span data-stu-id="ee1fa-108">Select what you want tooreplicate, and where you want tooreplicate to.</span></span>

1. <span data-ttu-id="ee1fa-109">Щелкните **Хранилища служб восстановления** > хранилище.</span><span class="sxs-lookup"><span data-stu-id="ee1fa-109">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="ee1fa-110">В hello ресурсов меню, щелкните **Site Recovery** > **Подготовка инфраструктуры** > **цель защиты**.</span><span class="sxs-lookup"><span data-stu-id="ee1fa-110">In hello Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="ee1fa-111">В **цель защиты**выберите **tooAzure** > **Да, с VMware vSphere низкоуровневой оболочки**.</span><span class="sxs-lookup"><span data-stu-id="ee1fa-111">In **Protection goal**, select **tooAzure** > **Yes, with VMware vSphere Hypervisor**.</span></span>



## <a name="next-steps"></a><span data-ttu-id="ee1fa-112">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ee1fa-112">Next steps</span></span>

<span data-ttu-id="ee1fa-113">Go слишком[Step 8: Настройка исходного и конечного](vmware-walkthrough-source-target.md)</span><span class="sxs-lookup"><span data-stu-id="ee1fa-113">Go too[Step 8: Set up source and target](vmware-walkthrough-source-target.md)</span></span>
