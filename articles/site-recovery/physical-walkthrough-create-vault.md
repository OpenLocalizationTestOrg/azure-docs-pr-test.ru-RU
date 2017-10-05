---
title: "Настройка хранилища для репликации физического сервера в Azure с помощью Azure Site Recovery | Документация Майкрософт"
description: "В этой статье кратко описаны шаги настройки хранилища для репликации из физических серверов в Azure с помощью Azure Site Recovery."
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
ms.openlocfilehash: deb5ad0495edc969b374795eeb2698326dd4ff4d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="step-6-set-up-a-vault-for-physical-server-replication-to-azure"></a><span data-ttu-id="2350c-103">Шаг 6. Настройка хранилища для репликации физического сервера в Azure</span><span class="sxs-lookup"><span data-stu-id="2350c-103">Step 6: Set up a vault for physical server replication to Azure</span></span>


<span data-ttu-id="2350c-104">В этой статье описывается настройка хранилища.</span><span class="sxs-lookup"><span data-stu-id="2350c-104">This article describes how to set up a vault.</span></span> <span data-ttu-id="2350c-105">Вы создадите хранилище и укажете, что именно необходимо реплицировать из локальной среды в Azure, используя службу [Azure Site Recovery](site-recovery-overview.md) на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="2350c-105">You create the vault, and specify what you want to replicate from your on-premises location to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="2350c-106">Комментарии или вопросы можно добавить в конце этой статьи или на [форуме по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="2350c-106">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="2350c-107">Создание хранилища служб восстановления</span><span class="sxs-lookup"><span data-stu-id="2350c-107">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a><span data-ttu-id="2350c-108">Выбор целевого объекта защиты</span><span class="sxs-lookup"><span data-stu-id="2350c-108">Select a protection goal</span></span>

<span data-ttu-id="2350c-109">Выберите целевые объекты и место для репликации.</span><span class="sxs-lookup"><span data-stu-id="2350c-109">Select what you want to replicate, and where you want to replicate to.</span></span>

1. <span data-ttu-id="2350c-110">Щелкните **Хранилища служб восстановления** > хранилище.</span><span class="sxs-lookup"><span data-stu-id="2350c-110">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="2350c-111">В меню ресурсов щелкните **Site Recovery** > **Подготовка инфраструктуры** > **Цель защиты**.</span><span class="sxs-lookup"><span data-stu-id="2350c-111">In the Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="2350c-112">На странице **Цель защиты** выберите **To Azure** (В Azure) > **Без виртуализации или иное**.</span><span class="sxs-lookup"><span data-stu-id="2350c-112">In **Protection goal**, select **To Azure** > **Not virtualized/Other**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="2350c-113">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2350c-113">Next steps</span></span>

<span data-ttu-id="2350c-114">Перейдите к статье [Шаг 7. Настройка исходной и целевой среды для репликации физического сервера в Azure](physical-walkthrough-source-target.md).</span><span class="sxs-lookup"><span data-stu-id="2350c-114">Go to [Step 7: Set up source and target](physical-walkthrough-source-target.md)</span></span>
