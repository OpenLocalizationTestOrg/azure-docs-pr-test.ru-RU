---
title: "Настройка хранилища для репликации Hyper-V (с System Center VMM) в Azure с помощью Azure Site Recovery | Документация Майкрософт"
description: "В этой статье кратко описаны шаги по настройке хранилища для репликации из Hyper-V (с VMM) в Azure с помощью Azure Site Recovery."
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
ms.openlocfilehash: af453ec27ba15ad8c59cf9f544584ad18dc0f74a
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/29/2017
---
# <a name="step-7-set-up-a-vault-for-hyper-v-replication"></a><span data-ttu-id="a4a4c-103">Шаг 7. Настройка хранилища для репликации Hyper-V</span><span class="sxs-lookup"><span data-stu-id="a4a4c-103">Step 7: Set up a vault for Hyper-V replication</span></span>

<span data-ttu-id="a4a4c-104">В этой статье описано, как настроить хранилище и указать, что именно необходимо реплицировать из локальной среды в Azure, используя службу [Azure Site Recovery](site-recovery-overview.md) на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="a4a4c-104">This article describes how to set up a vault, and specify what you want to replicate from your on-premises location, to Azure using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="a4a4c-105">Комментарии или вопросы можно добавить в конце этой статьи или на [форуме по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="a4a4c-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="a4a4c-106">Создание хранилища служб восстановления</span><span class="sxs-lookup"><span data-stu-id="a4a4c-106">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]



## <a name="select-a-protection-goal"></a><span data-ttu-id="a4a4c-107">Выбор целевого объекта защиты</span><span class="sxs-lookup"><span data-stu-id="a4a4c-107">Select a protection goal</span></span>

<span data-ttu-id="a4a4c-108">Выберите целевые объекты и место для репликации.</span><span class="sxs-lookup"><span data-stu-id="a4a4c-108">Select what you want to replicate, and where you want to replicate to.</span></span>

1. <span data-ttu-id="a4a4c-109">Щелкните **Хранилища служб восстановления** > хранилище.</span><span class="sxs-lookup"><span data-stu-id="a4a4c-109">Click **Recovery Services vaults** > vault.</span></span>
2. <span data-ttu-id="a4a4c-110">В меню ресурсов щелкните **Site Recovery** > **Подготовка инфраструктуры** > **Цель защиты**.</span><span class="sxs-lookup"><span data-stu-id="a4a4c-110">In the Resource Menu, click **Site Recovery** > **Prepare Infrastructure** > **Protection goal**.</span></span>
3. <span data-ttu-id="a4a4c-111">На странице **Protection goal** (Цель защиты) выберите **To Azure** (В Azure) > **Yes, with Hyper-V** (Да, с помощью Hyper-V).</span><span class="sxs-lookup"><span data-stu-id="a4a4c-111">In **Protection goal**, select **To Azure** > **Yes, with Hyper-V**.</span></span> <span data-ttu-id="a4a4c-112">Выберите **Да**, чтобы подтвердить использование VMM.</span><span class="sxs-lookup"><span data-stu-id="a4a4c-112">Select **Yes** to confirm you're nusing VMM.</span></span> 

     ![Выбор цели](./media/vmm-to-azure-walkthrough-create-vault/choose-goals.png)



## <a name="next-steps"></a><span data-ttu-id="a4a4c-114">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a4a4c-114">Next steps</span></span>

<span data-ttu-id="a4a4c-115">Перейдите к разделу [Шаг 8. Настройка исходной и целевой среды для репликации физического сервера в Azure](vmm-to-azure-walkthrough-source-target.md).</span><span class="sxs-lookup"><span data-stu-id="a4a4c-115">Go to [Step 8: Set up source and target](vmm-to-azure-walkthrough-source-target.md)</span></span>
