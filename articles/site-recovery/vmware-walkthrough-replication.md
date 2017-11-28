---
title: "Настройка политики репликации для репликации виртуальных машин VMware в Azure с помощью Azure Site Recovery | Документация Майкрософт"
description: "В этой статье кратко описаны шаги для настройки политики репликации при выполнении репликации виртуальных машин VMware в службу хранилища Azure."
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
ms.openlocfilehash: 3c4b7ad16e6a03fb605447def18f7475d502fdd1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="step-9-set-up-a-replication-policy-for-vmware-vm-replication-to-azure"></a><span data-ttu-id="2da56-103">Шаг 9. Настройка политики репликации для репликации виртуальных машин VMware в Azure</span><span class="sxs-lookup"><span data-stu-id="2da56-103">Step 9: Set up a replication policy for VMware VM replication to Azure</span></span>


<span data-ttu-id="2da56-104">В этой статье описывается настройка политики репликации при выполнении репликации виртуальных машин VMware в Azure с помощью службы [Azure Site Recovery](site-recovery-overview.md) на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="2da56-104">This article describes how to set up a replication policy when you're replicating VMware VMs to Azure using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="2da56-105">Комментарии или вопросы можно добавить в конце этой статьи или на [форуме по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="2da56-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="configure-a-policy"></a><span data-ttu-id="2da56-106">Настройка политики</span><span class="sxs-lookup"><span data-stu-id="2da56-106">Configure a policy</span></span>

<span data-ttu-id="2da56-107">Перед началом посмотрите краткий видеообзор:</span><span class="sxs-lookup"><span data-stu-id="2da56-107">Get a quick video overview before you start:</span></span>
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. <span data-ttu-id="2da56-108">Чтобы создать новую политику репликации, щелкните **Инфраструктура Site Recovery** > **Политики репликации** > **+Политика репликации**.</span><span class="sxs-lookup"><span data-stu-id="2da56-108">To create a new replication policy, click **Site Recovery infrastructure** > **Replication Policies** > **+Replication Policy**.</span></span>
2. <span data-ttu-id="2da56-109">На странице **Создать политику репликации** укажите имя политики.</span><span class="sxs-lookup"><span data-stu-id="2da56-109">In **Create replication policy**, specify a policy name.</span></span>
3. <span data-ttu-id="2da56-110">В поле **Пороговое значение RPO**укажите предельное значение целевой точки восстановления (RPO).</span><span class="sxs-lookup"><span data-stu-id="2da56-110">In **RPO threshold**, specify the RPO limit.</span></span> <span data-ttu-id="2da56-111">Это значение указывает, как часто создаются точки восстановления данных.</span><span class="sxs-lookup"><span data-stu-id="2da56-111">This value specifies how often data recovery points are created.</span></span> <span data-ttu-id="2da56-112">Если непрерывная репликация превышает это значение, выдаются оповещения.</span><span class="sxs-lookup"><span data-stu-id="2da56-112">An alert is generated if continuous replication exceeds this limit.</span></span>
4. <span data-ttu-id="2da56-113">В поле **Хранение точки восстановления** укажите продолжительность периода хранения для каждой точки восстановления (в часах).</span><span class="sxs-lookup"><span data-stu-id="2da56-113">In **Recovery point retention**, specify (in hours) how long the retention window is for each recovery point.</span></span> <span data-ttu-id="2da56-114">Реплицированные виртуальные машины можно восстановить до любой точки в рамках этого периода.</span><span class="sxs-lookup"><span data-stu-id="2da56-114">Replicated VMs can be recovered to any point in a window.</span></span> <span data-ttu-id="2da56-115">Для компьютеров, реплицируемых в хранилище класса Premium, поддерживается период удержания до 24 часов, а для хранилище класса Standard — до 72 часов.</span><span class="sxs-lookup"><span data-stu-id="2da56-115">Up to 24 hours retention is supported for machines replicated to premium storage, and 72 hours for standard storage.</span></span>
5. <span data-ttu-id="2da56-116">В поле **Периодичность создания моментальных снимков с согласованием приложений**укажите, с какой периодичностью (в минутах) будут создаваться точки восстановления, содержащие моментальные снимки, согласованные на уровне приложений.</span><span class="sxs-lookup"><span data-stu-id="2da56-116">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="2da56-117">Нажмите кнопку **ОК** , чтобы создать политику.</span><span class="sxs-lookup"><span data-stu-id="2da56-117">Click **OK** to create the policy.</span></span>

    ![Политика репликации](./media/vmware-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="2da56-119">Созданная политика автоматически сопоставляется с облаком сервером конфигурации.</span><span class="sxs-lookup"><span data-stu-id="2da56-119">When you create a new policy it's automatically associated with the configuration server.</span></span> <span data-ttu-id="2da56-120">Для восстановления размещения по умолчанию автоматически создается соответствующая политика.</span><span class="sxs-lookup"><span data-stu-id="2da56-120">By default, a matching policy is automatically created for failback.</span></span> <span data-ttu-id="2da56-121">Например, если политика репликации называется **rep-policy**, то политика восстановления размещения будет называться **rep-policy-failback**.</span><span class="sxs-lookup"><span data-stu-id="2da56-121">For example, if the replication policy is **rep-policy** then the failback policy will be **rep-policy-failback**.</span></span> <span data-ttu-id="2da56-122">Эта политика не используется, пока не будет запущено восстановление размещения из Azure.</span><span class="sxs-lookup"><span data-stu-id="2da56-122">This policy isn't used until you initiate a failback from Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2da56-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2da56-123">Next steps</span></span>

<span data-ttu-id="2da56-124">Перейдите к разделу [Шаг 10. Установка службы Mobility Service](vmware-walkthrough-install-mobility.md).</span><span class="sxs-lookup"><span data-stu-id="2da56-124">Go to [Step 10: Install the Mobility service](vmware-walkthrough-install-mobility.md)</span></span>
