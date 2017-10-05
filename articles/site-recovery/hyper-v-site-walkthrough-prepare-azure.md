---
title: "Подготовка ресурсов Azure для репликации виртуальных машин Hyper-V (без System Center VMM) в Azure с помощью Azure Site Recovery | Документация Майкрософт"
description: "Основные сведения о том, что нужно сделать в среде Azure перед началом репликации виртуальных машин Hyper-V (без VMM) в Azure с помощью Azure Site Recovery"
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
ms.openlocfilehash: 1a30cadaab7e053184f0be133f1da5bfddc1fd91
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="step-5-prepare-azure-resources-for-hyper-v-replication-to-azure"></a><span data-ttu-id="33381-103">Шаг 5. Подготовка ресурсов Azure для репликации Hyper-V в Azure</span><span class="sxs-lookup"><span data-stu-id="33381-103">Step 5: Prepare Azure resources for Hyper-V replication to Azure</span></span>

<span data-ttu-id="33381-104">Воспользуйтесь инструкциями из этой статьи, чтобы с помощью службы [Azure Site Recovery](site-recovery-overview.md) подготовить ресурсы Azure для репликации локальных виртуальных машин Hyper-V (без в System Center VMM) Azure.</span><span class="sxs-lookup"><span data-stu-id="33381-104">Use the instructions in this article to prepare Azure resources so that you can replicate on-premises Hyper-V VMs (without System Center VMM) to Azure using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="33381-105">Комментарии или вопросы технического характера можно добавить в конце этой статьи или на [форуме по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="33381-105">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="33381-106">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="33381-106">Before you start</span></span>

<span data-ttu-id="33381-107">Ознакомьтесь со статьей о [предварительных требованиях](hyper-v-site-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="33381-107">Make sure you've read the [prerequisites](hyper-v-site-walkthrough-prerequisites.md)</span></span>

## <a name="set-up-an-azure-account"></a><span data-ttu-id="33381-108">Настройка учетной записи Azure</span><span class="sxs-lookup"><span data-stu-id="33381-108">Set up an Azure account</span></span>

- <span data-ttu-id="33381-109">Получите [учетную запись Microsoft Azure](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="33381-109">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="33381-110">Начните с [бесплатной пробной версии](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="33381-110">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="33381-111">Сведения о поддерживаемых регионах для Site Recovery см. в разделе "Географическая доступность" на странице [цен на службу Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="33381-111">Check the supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="33381-112">Ознакомьтесь с расходами [при использования Site Recovery](site-recovery-faq.md#pricing) и [сведениями о ценах](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="33381-112">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get the [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>


## <a name="set-up-an-azure-network"></a><span data-ttu-id="33381-113">Настроить сеть</span><span class="sxs-lookup"><span data-stu-id="33381-113">Set up an Azure network</span></span>

- <span data-ttu-id="33381-114">Настройка сети Azure.</span><span class="sxs-lookup"><span data-stu-id="33381-114">Set up an Azure network.</span></span> <span data-ttu-id="33381-115">Виртуальные машины Azure будут размещаться в этой сети при создании после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="33381-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="33381-116">Сеть должна располагаться в том же регионе, что и хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="33381-116">The network should be in the same region as the Recovery Services vault</span></span>
- <span data-ttu-id="33381-117">Служба Site Recovery на портале Azure может использовать сети, настроенные в режиме [Resource Manager](../resource-manager-deployment-model.md) или в классическом режиме.</span><span class="sxs-lookup"><span data-stu-id="33381-117">Site Recovery in the Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="33381-118">Рекомендуется настроить сеть перед началом работы.</span><span class="sxs-lookup"><span data-stu-id="33381-118">We recommend you set up a network before you begin.</span></span> <span data-ttu-id="33381-119">В противном случае это нужно будет сделать во время развертывания службы Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="33381-119">If you don't, you need to do it during Site Recovery deployment.</span></span>
- <span data-ttu-id="33381-120">Ознакомьтесь со сведениями о [ценах на виртуальную сеть](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="33381-120">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="33381-121">Настроить учетную запись хранения Azure</span><span class="sxs-lookup"><span data-stu-id="33381-121">Set up an Azure storage account</span></span>

- <span data-ttu-id="33381-122">Служба Site Recovery реплицирует локальные машины в службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="33381-122">Site Recovery replicates on-premises machines to Azure storage.</span></span> <span data-ttu-id="33381-123">Виртуальные машины Azure создаются из хранилища после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="33381-123">Azure VMs are created from the storage after failover occurs.</span></span>
- <span data-ttu-id="33381-124">Для хранения данных, реплицированных в Azure, понадобится настроить [учетную запись хранения Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) класса "Стандартный" или Premium.</span><span class="sxs-lookup"><span data-stu-id="33381-124">Set up a standard/premium [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) to hold data replicated to Azure.</span></span>
- <span data-ttu-id="33381-125">[Хранилище класса Premium](../storage/common/storage-premium-storage.md) обычно используется для виртуальных машин, которым постоянно требуется высокая производительность ввода-вывода и малая задержка для размещения интенсивных рабочих нагрузок ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="33381-125">[Premium storage](../storage/common/storage-premium-storage.md) is typically used for virtual machines that need a consistently high IO performance, and low latency to host IO intensive workloads.</span></span>
- <span data-ttu-id="33381-126">Если для хранения реплицированных данных вы будете использовать учетную запись хранения класса Premium, потребуется дополнительная учетная запись хранения класса Standard для хранения журналов репликации, в которые записываются текущие изменения локальных данных.</span><span class="sxs-lookup"><span data-stu-id="33381-126">If you want to use a premium account to store replicated data, you also need a standard storage account to store replication logs that capture ongoing changes to on-premises data.</span></span>
- <span data-ttu-id="33381-127">В зависимости от модели ресурсов, которую будут использовать виртуальные машины Azure после отработки отказа, для учетной записи необходимо настроить [режим Resource Manager](../storage/common/storage-create-storage-account.md) или [классический режим](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="33381-127">Depending on the resource model you want to use for failed over Azure VMs, you set up an account in [Resource Manager mode](../storage/common/storage-create-storage-account.md), or [classic mode](../storage/common/storage-create-storage-account.md).</span></span>
- <span data-ttu-id="33381-128">Рекомендуется настроить учетную запись хранения до начала работы.</span><span class="sxs-lookup"><span data-stu-id="33381-128">We recommend that you set up a storage account before you begin.</span></span> <span data-ttu-id="33381-129">В противном случае это нужно будет сделать во время развертывания службы Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="33381-129">If you don't you need to do it during Site Recovery deployment.</span></span> <span data-ttu-id="33381-130">Учетные записи должны находиться в том же регионе, что и хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="33381-130">The accounts must be in the same region as the Recovery Services vault.</span></span>
- <span data-ttu-id="33381-131">Учетные записи хранения, используемые для Site Recovery, нельзя перемещать между группами в одной подписке или между разными подписками.</span><span class="sxs-lookup"><span data-stu-id="33381-131">You can't move storage accounts used by Site Recovery across resource groups within the same subscription, or across different subscriptions.</span></span>


## <a name="next-steps"></a><span data-ttu-id="33381-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="33381-132">Next steps</span></span>

<span data-ttu-id="33381-133">Перейдите к статье [Step 6: Prepare on-premises VMware replication to Azure](hyper-v-site-walkthrough-prepare-hyper-v.md) (Шаг 6. Подготовка ресурсов Hyper-V).</span><span class="sxs-lookup"><span data-stu-id="33381-133">Go to [Step 6: Prepare Hyper-V resources](hyper-v-site-walkthrough-prepare-hyper-v.md)</span></span>
