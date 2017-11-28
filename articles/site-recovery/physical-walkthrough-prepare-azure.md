---
title: "ресурсы Azure tooreplicate aaaPrepare локальной tooAzure физических серверов, с помощью Azure Site Recovery | Документы Microsoft"
description: "Основные сведения, необходимые на месте в Azure перед началом репликации tooAzure локальных серверов, с помощью службы Azure Site Recovery hello"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 4e320d9b-8bb8-46bb-ba21-77c5d16748ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/25/2017
ms.author: raynew
ms.openlocfilehash: b1d008dac278bc7797188a3c9c15f2a3b5fe12d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-prepare-azure-resources-for-physical-server-replication-tooazure"></a><span data-ttu-id="d8a93-103">Шаг 5: Подготовка ресурсов Azure для репликации tooAzure физического сервера</span><span class="sxs-lookup"><span data-stu-id="d8a93-103">Step 5: Prepare Azure resources for physical server replication tooAzure</span></span>


<span data-ttu-id="d8a93-104">Используйте инструкции hello в этой статье tooprepare Azure ресурсы, чтобы можно было реплицировать tooAzure локальных серверов, с помощью hello [Azure Site Recovery](site-recovery-overview.md) службы.</span><span class="sxs-lookup"><span data-stu-id="d8a93-104">Use hello instructions in this article tooprepare Azure resources so that you can replicate on-premises servers tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="d8a93-105">Учет комментарии и вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="d8a93-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="d8a93-106">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="d8a93-106">Before you start</span></span>

<span data-ttu-id="d8a93-107">Убедитесь, что вы прочитали hello [необходимых компонентов](physical-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="d8a93-107">Make sure you've read hello [prerequisites](physical-walkthrough-prerequisites.md).</span></span>

## <a name="set-up-an-azure-account"></a><span data-ttu-id="d8a93-108">Настройка учетной записи Azure</span><span class="sxs-lookup"><span data-stu-id="d8a93-108">Set up an Azure account</span></span>

- <span data-ttu-id="d8a93-109">Получите [учетную запись Microsoft Azure](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="d8a93-109">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="d8a93-110">Начните с [бесплатной пробной версии](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d8a93-110">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="d8a93-111">Проверьте областей hello поддерживается для восстановления сайта в разделе **географическая доступность** в [сведения о ценах Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="d8a93-111">Check hello supported regions for Site Recovery, under **Geographic Availability** in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="d8a93-112">Дополнительные сведения о [цены Site Recovery](site-recovery-faq.md#pricing)и получить hello [сведения о ценах](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="d8a93-112">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get hello [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>



## <a name="set-up-an-azure-network"></a><span data-ttu-id="d8a93-113">Настроить сеть Azure</span><span class="sxs-lookup"><span data-stu-id="d8a93-113">Set up an Azure network</span></span>

- <span data-ttu-id="d8a93-114">Настройка сети Azure.</span><span class="sxs-lookup"><span data-stu-id="d8a93-114">Set up an Azure network.</span></span> <span data-ttu-id="d8a93-115">Виртуальные машины Azure будут размещаться в этой сети при создании после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="d8a93-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="d8a93-116">Восстановление сайта в hello портал Azure можно использовать настройки сетей в [диспетчера ресурсов](../resource-manager-deployment-model.md), или в классическом режиме.</span><span class="sxs-lookup"><span data-stu-id="d8a93-116">Site Recovery in hello Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="d8a93-117">сеть Hello должны находиться в hello же регионе, что hello в хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="d8a93-117">hello network should be in hello same region as hello Recovery Services vault.</span></span>
- <span data-ttu-id="d8a93-118">Ознакомьтесь со сведениями о [ценах на виртуальную сеть](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="d8a93-118">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>
- <span data-ttu-id="d8a93-119">Ознакомьтесь с дополнительными сведениями о [подключении к виртуальным машинам Azure](physical-walkthrough-network.md) после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="d8a93-119">Learn more about [Azure VM connectivity](physical-walkthrough-network.md) after failover.</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="d8a93-120">Настроить учетную запись хранения Azure</span><span class="sxs-lookup"><span data-stu-id="d8a93-120">Set up an Azure storage account</span></span>

- <span data-ttu-id="d8a93-121">Site Recovery реплицирует tooAzure серверах в локальном хранилище.</span><span class="sxs-lookup"><span data-stu-id="d8a93-121">Site Recovery replicates on-premises servers tooAzure storage.</span></span> <span data-ttu-id="d8a93-122">Виртуальные машины Azure создаются из хранилища hello после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="d8a93-122">Azure VMs are created from hello storage after failover occurs.</span></span>
- <span data-ttu-id="d8a93-123">Настройте [учетную запись хранения Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) для реплицированных данных.</span><span class="sxs-lookup"><span data-stu-id="d8a93-123">Set up an [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) for replicated data.</span></span>
- <span data-ttu-id="d8a93-124">Восстановление сайта в hello портал Azure можно использовать учетные записи хранения в диспетчере ресурсов или в классическом режиме.</span><span class="sxs-lookup"><span data-stu-id="d8a93-124">Site Recovery in hello Azure portal can use storage accounts set up in Resource Manager, or in classic mode.</span></span>
- <span data-ttu-id="d8a93-125">Hello учетной записи хранения может быть стандартной или [premium](../storage/common/storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="d8a93-125">hello storage account can be standard or [premium](../storage/common/storage-premium-storage.md).</span></span>
- <span data-ttu-id="d8a93-126">Если вы настроите учетную запись уровня "Премиум", вам также понадобится дополнительная учетная запись уровня "Стандартный" для данных журнала.</span><span class="sxs-lookup"><span data-stu-id="d8a93-126">If you set up a premium account, you will also need an additional standard account for log data.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d8a93-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d8a93-127">Next steps</span></span>

<span data-ttu-id="d8a93-128">Go слишком[шаг 6: Настройка хранилища](physical-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="d8a93-128">Go too[Step 6: Set up a vault](physical-walkthrough-create-vault.md)</span></span>
