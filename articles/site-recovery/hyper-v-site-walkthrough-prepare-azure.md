---
title: "с помощью Azure Site Recovery виртуальных машин Hyper-V (без System Center VMM) tooAzure aaaPrepare ресурсы Azure tooreplicate | Документы Microsoft"
description: "Основные сведения, необходимые на месте в Azure перед началом репликации с помощью Azure Site Recovery tooAzure виртуальных машин Hyper-V (без VMM)"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 28fa722c-675e-4637-98eb-7ccbf3806d69
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: f659e300c39253b0eaf7218bee9d39b11682edb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-tooazure"></a><span data-ttu-id="a4ceb-103">Шаг 5: Подготовка ресурсов Azure для tooAzure репликации Hyper-V</span><span class="sxs-lookup"><span data-stu-id="a4ceb-103">Step 5: Prepare Azure resources for Hyper-V replication tooAzure</span></span>

<span data-ttu-id="a4ceb-104">Используйте инструкции hello в этой статье tooprepare Azure, чтобы можно было реплицировать локальные ресурсы виртуальных машин Hyper-V (без System Center VMM) с помощью hello tooAzure [Azure Site Recovery](site-recovery-overview.md) службы.</span><span class="sxs-lookup"><span data-stu-id="a4ceb-104">Use hello instructions in this article tooprepare Azure resources so that you can replicate on-premises Hyper-V VMs (without System Center VMM) tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="a4ceb-105">После считывания в этой статье, отправлять любые комментарии внизу hello или задавайте технические вопросы на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="a4ceb-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="a4ceb-106">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="a4ceb-106">Before you start</span></span>

<span data-ttu-id="a4ceb-107">Убедитесь, что вы прочитали hello [предварительные требования](hyper-v-site-walkthrough-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="a4ceb-107">Make sure you've read hello [prerequisites](hyper-v-site-walkthrough-prerequisites.md)</span></span>

## <a name="set-up-an-azure-account"></a><span data-ttu-id="a4ceb-108">Настройка учетной записи Azure</span><span class="sxs-lookup"><span data-stu-id="a4ceb-108">Set up an Azure account</span></span>

- <span data-ttu-id="a4ceb-109">Получите [учетную запись Microsoft Azure](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="a4ceb-109">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="a4ceb-110">Начните с [бесплатной пробной версии](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a4ceb-110">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="a4ceb-111">Проверьте областей hello поддерживается для восстановления сайта в группе географическая доступность в [сведения о ценах Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="a4ceb-111">Check hello supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="a4ceb-112">Дополнительные сведения о [цены Site Recovery](site-recovery-faq.md#pricing)и получить hello [сведения о ценах](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="a4ceb-112">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get hello [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>


## <a name="set-up-an-azure-network"></a><span data-ttu-id="a4ceb-113">Настроить сеть Azure</span><span class="sxs-lookup"><span data-stu-id="a4ceb-113">Set up an Azure network</span></span>

- <span data-ttu-id="a4ceb-114">Настройка сети Azure.</span><span class="sxs-lookup"><span data-stu-id="a4ceb-114">Set up an Azure network.</span></span> <span data-ttu-id="a4ceb-115">Виртуальные машины Azure будут размещаться в этой сети при создании после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="a4ceb-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="a4ceb-116">сеть Hello должны находиться в hello же регионе, что hello в хранилище службы восстановления</span><span class="sxs-lookup"><span data-stu-id="a4ceb-116">hello network should be in hello same region as hello Recovery Services vault</span></span>
- <span data-ttu-id="a4ceb-117">Восстановление сайта в hello портал Azure можно использовать настройки сетей в [диспетчера ресурсов](../resource-manager-deployment-model.md), или в классическом режиме.</span><span class="sxs-lookup"><span data-stu-id="a4ceb-117">Site Recovery in hello Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="a4ceb-118">Рекомендуется настроить сеть перед началом работы.</span><span class="sxs-lookup"><span data-stu-id="a4ceb-118">We recommend you set up a network before you begin.</span></span> <span data-ttu-id="a4ceb-119">Если этого не сделать, то необходимо toodo его во время развертывания службы восстановления сайтов.</span><span class="sxs-lookup"><span data-stu-id="a4ceb-119">If you don't, you need toodo it during Site Recovery deployment.</span></span>
- <span data-ttu-id="a4ceb-120">Ознакомьтесь со сведениями о [ценах на виртуальную сеть](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="a4ceb-120">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="a4ceb-121">Настроить учетную запись хранения Azure</span><span class="sxs-lookup"><span data-stu-id="a4ceb-121">Set up an Azure storage account</span></span>

- <span data-ttu-id="a4ceb-122">Site Recovery реплицирует tooAzure машин в локальном хранилище.</span><span class="sxs-lookup"><span data-stu-id="a4ceb-122">Site Recovery replicates on-premises machines tooAzure storage.</span></span> <span data-ttu-id="a4ceb-123">Виртуальные машины Azure создаются из хранилища hello после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="a4ceb-123">Azure VMs are created from hello storage after failover occurs.</span></span>
- <span data-ttu-id="a4ceb-124">Настройка standard и premium [учетной записи хранилища Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) tooAzure репликации toohold данных.</span><span class="sxs-lookup"><span data-stu-id="a4ceb-124">Set up a standard/premium [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) toohold data replicated tooAzure.</span></span>
- <span data-ttu-id="a4ceb-125">[Хранилище Premium](../storage/common/storage-premium-storage.md) обычно используется для виртуальных машин, требующих постоянно высокое производительности операций ввода-ВЫВОДА и toohost низкую задержку операций ввода-ВЫВОДА интенсивных рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="a4ceb-125">[Premium storage](../storage/common/storage-premium-storage.md) is typically used for virtual machines that need a consistently high IO performance, and low latency toohost IO intensive workloads.</span></span>
- <span data-ttu-id="a4ceb-126">Если вы хотите toouse toostore учетной записи premium реплицированные данные, необходимо также стандартные журналы учетной записи хранения toostore репликации, отслеживания текущих изменений tooon локальные данные.</span><span class="sxs-lookup"><span data-stu-id="a4ceb-126">If you want toouse a premium account toostore replicated data, you also need a standard storage account toostore replication logs that capture ongoing changes tooon-premises data.</span></span>
- <span data-ttu-id="a4ceb-127">В зависимости от модели ресурсов hello хотите toouse отработку отказа виртуальных машин Azure, настройте учетную запись в [режим диспетчера ресурсов](../storage/common/storage-create-storage-account.md), или [классический режим](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="a4ceb-127">Depending on hello resource model you want toouse for failed over Azure VMs, you set up an account in [Resource Manager mode](../storage/common/storage-create-storage-account.md), or [classic mode](../storage/common/storage-create-storage-account.md).</span></span>
- <span data-ttu-id="a4ceb-128">Рекомендуется настроить учетную запись хранения до начала работы.</span><span class="sxs-lookup"><span data-stu-id="a4ceb-128">We recommend that you set up a storage account before you begin.</span></span> <span data-ttu-id="a4ceb-129">Если не требуется toodo его во время развертывания службы восстановления сайтов.</span><span class="sxs-lookup"><span data-stu-id="a4ceb-129">If you don't you need toodo it during Site Recovery deployment.</span></span> <span data-ttu-id="a4ceb-130">Hello должны находиться в hello же регионе, что hello в хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="a4ceb-130">hello accounts must be in hello same region as hello Recovery Services vault.</span></span>
- <span data-ttu-id="a4ceb-131">Не удается переместить использовать учетные записи хранения с Site Recovery для групп ресурсов в hello же подписки, или в разных подписках.</span><span class="sxs-lookup"><span data-stu-id="a4ceb-131">You can't move storage accounts used by Site Recovery across resource groups within hello same subscription, or across different subscriptions.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a4ceb-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a4ceb-132">Next steps</span></span>

<span data-ttu-id="a4ceb-133">Go слишком[шаг 6: ресурсы Подготовка Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)</span><span class="sxs-lookup"><span data-stu-id="a4ceb-133">Go too[Step 6: Prepare Hyper-V resources](hyper-v-site-walkthrough-prepare-hyper-v.md)</span></span>
