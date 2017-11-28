---
title: "Настройка политики репликации для репликации физического сервера в Azure с помощью Azure Site Recovery | Документация Майкрософт"
description: "В этой статье описаны шаги, необходимые для настройки политики репликации при репликации локальных физических серверов в службу хранилища Azure с помощью службы Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d7874bd8-6626-4668-9ec9-dbd2d26f8f81
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 9ce23382001b54e7b9b7a58b8dd9aa61b400826d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="step-8-set-up-a-replication-policy-for-physical-server-replication-to-azure"></a><span data-ttu-id="06ec5-103">Шаг 8. Настройка политики репликации для репликации физического сервера в Azure</span><span class="sxs-lookup"><span data-stu-id="06ec5-103">Step 8: Set up a replication policy for physical server replication to Azure</span></span>


<span data-ttu-id="06ec5-104">В этой статье описывается настройка политики репликации при репликации физических серверов Windows и Linux в Azure с помощью службы [Azure Site Recovery](site-recovery-overview.md) на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="06ec5-104">This article describes how to set up a replication policy when you're replicating Windows/Linux physical servers to Azure using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="06ec5-105">Комментарии или вопросы можно добавить в конце этой статьи или на [форуме по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="06ec5-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="configure-a-policy"></a><span data-ttu-id="06ec5-106">Настройка политики</span><span class="sxs-lookup"><span data-stu-id="06ec5-106">Configure a policy</span></span>

1. <span data-ttu-id="06ec5-107">Щелкните **Site Recovery infrastructure** (Инфраструктура Site Recovery) > **Политики репликации** > **+Replication Policy** (+Политика репликации).</span><span class="sxs-lookup"><span data-stu-id="06ec5-107">Click **Site Recovery infrastructure** > **Replication Policies** > **+Replication Policy**.</span></span>
2. <span data-ttu-id="06ec5-108">На странице **Создать политику репликации** укажите имя политики.</span><span class="sxs-lookup"><span data-stu-id="06ec5-108">In **Create replication policy**, specify a policy name.</span></span>
3. <span data-ttu-id="06ec5-109">В поле **Пороговое значение RPO**укажите предельное значение целевой точки восстановления (RPO).</span><span class="sxs-lookup"><span data-stu-id="06ec5-109">In **RPO threshold**, specify the RPO limit.</span></span> <span data-ttu-id="06ec5-110">Это значение указывает, как часто создаются точки восстановления данных.</span><span class="sxs-lookup"><span data-stu-id="06ec5-110">This value indicates how often data recovery points are created.</span></span> <span data-ttu-id="06ec5-111">Если непрерывная репликация превышает это значение, выдаются оповещения.</span><span class="sxs-lookup"><span data-stu-id="06ec5-111">An alert is generated if continuous replication exceeds this limit.</span></span>
4. <span data-ttu-id="06ec5-112">В поле **Хранение точки восстановления** укажите продолжительность периода хранения для каждой точки восстановления (в часах).</span><span class="sxs-lookup"><span data-stu-id="06ec5-112">In **Recovery point retention**, specify (in hours) how long the retention window is for each recovery point.</span></span> <span data-ttu-id="06ec5-113">Реплицированные виртуальные машины можно восстановить до любой точки в рамках этого периода.</span><span class="sxs-lookup"><span data-stu-id="06ec5-113">Replicated VMs can be recovered to any point in a window.</span></span> <span data-ttu-id="06ec5-114">Для компьютеров, реплицируемых в хранилище класса Premium, поддерживается период удержания до 24 часов, а для хранилище класса Standard — до 72 часов.</span><span class="sxs-lookup"><span data-stu-id="06ec5-114">Up to 24 hours retention is supported for machines replicated to premium storage, and 72 hours for standard storage.</span></span>
5. <span data-ttu-id="06ec5-115">В поле **Периодичность создания моментальных снимков с согласованием приложений**укажите, с какой периодичностью (в минутах) будут создаваться точки восстановления, содержащие моментальные снимки, согласованные на уровне приложений.</span><span class="sxs-lookup"><span data-stu-id="06ec5-115">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="06ec5-116">Нажмите кнопку **ОК** , чтобы создать политику.</span><span class="sxs-lookup"><span data-stu-id="06ec5-116">Click **OK** to create the policy.</span></span>

    ![Политика репликации](./media/physical-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="06ec5-118">Созданная политика автоматически сопоставляется с облаком сервером конфигурации.</span><span class="sxs-lookup"><span data-stu-id="06ec5-118">When you create a new policy it's automatically associated with the configuration server.</span></span> <span data-ttu-id="06ec5-119">Для восстановления размещения по умолчанию автоматически создается соответствующая политика.</span><span class="sxs-lookup"><span data-stu-id="06ec5-119">By default, a matching policy is automatically created for failback.</span></span> <span data-ttu-id="06ec5-120">Например, если политика репликации называется **rep-policy**, то политика восстановления размещения будет называться **rep-policy-failback**.</span><span class="sxs-lookup"><span data-stu-id="06ec5-120">For example, if the replication policy is **rep-policy** then the failback policy will be **rep-policy-failback**.</span></span> <span data-ttu-id="06ec5-121">Эта политика не используется, пока не будет запущено восстановление размещения из Azure.</span><span class="sxs-lookup"><span data-stu-id="06ec5-121">This policy isn't used until you initiate a failback from Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="06ec5-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="06ec5-122">Next steps</span></span>

<span data-ttu-id="06ec5-123">Перейдите к статье [Step 9: Install the Mobility service](physical-walkthrough-install-mobility.md) (Шаг 9. Установка службы Mobility Service).</span><span class="sxs-lookup"><span data-stu-id="06ec5-123">Go to [Step 9: Install the Mobility service](physical-walkthrough-install-mobility.md)</span></span>
