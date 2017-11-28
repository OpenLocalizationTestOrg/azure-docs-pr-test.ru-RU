---
title: "Подготовка ресурсов Azure для репликации виртуальных машин VMware из локальной среды в Azure с помощью Azure Site Recovery | Документация Майкрософт"
description: "Эта статья содержит сведения о компонентах, которые необходимо настроить в Azure, прежде чем приступить к репликации виртуальных машин VMware из локальной среды в Azure с помощью Azure Site Recovery."
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
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 40abff72278c9f8d9f701023fd473fe52c17b421
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="step-5-prepare-azure-resources-for-vmware-replication-to-azure"></a><span data-ttu-id="97f6c-103">Шаг 5. Подготовка ресурсов Azure для репликации из VMWare в Azure</span><span class="sxs-lookup"><span data-stu-id="97f6c-103">Step 5: Prepare Azure resources for VMWare replication to Azure</span></span>


<span data-ttu-id="97f6c-104">Используйте инструкции этой статьи, чтобы подготовить ресурсы Azure для репликации виртуальных машин из локальной среды в Azure с помощью службы [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="97f6c-104">Use the instructions in this article to prepare Azure resources so that you can replicate on-premises machines to Azure using the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="97f6c-105">Комментарии или вопросы можно добавить в конце этой статьи или на [форуме по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="97f6c-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="97f6c-106">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="97f6c-106">Before you start</span></span>

<span data-ttu-id="97f6c-107">Ознакомьтесь со статьей о [предварительных требованиях](vmware-walkthrough-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="97f6c-107">Make sure you've read the [prerequisites](vmware-walkthrough-prerequisites.md)</span></span>

## <a name="set-up-an-azure-account"></a><span data-ttu-id="97f6c-108">Настройка учетной записи Azure</span><span class="sxs-lookup"><span data-stu-id="97f6c-108">Set up an Azure account</span></span>

- <span data-ttu-id="97f6c-109">Получите [учетную запись Microsoft Azure](http://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="97f6c-109">Get a [Microsoft Azure account](http://azure.microsoft.com/).</span></span>
- <span data-ttu-id="97f6c-110">Начните с [бесплатной пробной версии](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="97f6c-110">You can start with a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
- <span data-ttu-id="97f6c-111">Сведения о поддерживаемых регионах для Site Recovery см. в разделе "Географическая доступность" на странице [цен на службу Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="97f6c-111">Check the supported regions for Site Recovery, Under Geographic Availability in [Azure Site Recovery Pricing Details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
- <span data-ttu-id="97f6c-112">Ознакомьтесь с расходами [при использования Site Recovery](site-recovery-faq.md#pricing) и [сведениями о ценах](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="97f6c-112">Learn about [Site Recovery pricing](site-recovery-faq.md#pricing), and get the [pricing details](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>



## <a name="set-up-an-azure-network"></a><span data-ttu-id="97f6c-113">Настроить сеть</span><span class="sxs-lookup"><span data-stu-id="97f6c-113">Set up an Azure network</span></span>

- <span data-ttu-id="97f6c-114">Настройка сети Azure.</span><span class="sxs-lookup"><span data-stu-id="97f6c-114">Set up an Azure network.</span></span> <span data-ttu-id="97f6c-115">Виртуальные машины Azure будут размещаться в этой сети при создании после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="97f6c-115">Azure VMs are placed in this network when they're created after failover.</span></span>
- <span data-ttu-id="97f6c-116">Используя службу Site Recovery на портале Azure, можно настроить сети в [Resource Manager](../resource-manager-deployment-model.md) или в классическом режиме.</span><span class="sxs-lookup"><span data-stu-id="97f6c-116">Site Recovery in the Azure portal can use networks set up in [Resource Manager](../resource-manager-deployment-model.md), or in classic mode.</span></span>
- <span data-ttu-id="97f6c-117">Сеть должна располагаться в том же регионе, что и хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="97f6c-117">The network should be in the same region as the Recovery Services vault</span></span>
- <span data-ttu-id="97f6c-118">Ознакомьтесь со сведениями о [ценах на виртуальную сеть](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="97f6c-118">Learn about [virtual network pricing](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>
- <span data-ttu-id="97f6c-119">Ознакомьтесь с дополнительными сведениями о [подключении к виртуальным машинам Azure](site-recovery-network-design.md) после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="97f6c-119">Learn more about [Azure VM connectivity](site-recovery-network-design.md) after failover.</span></span>


## <a name="set-up-an-azure-storage-account"></a><span data-ttu-id="97f6c-120">Настроить учетную запись хранения Azure</span><span class="sxs-lookup"><span data-stu-id="97f6c-120">Set up an Azure storage account</span></span>

- <span data-ttu-id="97f6c-121">Служба Site Recovery реплицирует локальные машины в службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="97f6c-121">Site Recovery replicates on-premises machines to Azure storage.</span></span> <span data-ttu-id="97f6c-122">После отработки отказа виртуальные машины Azure создаются из хранилища.</span><span class="sxs-lookup"><span data-stu-id="97f6c-122">Azure VMs are created from the storage after failover occurs.</span></span>
- <span data-ttu-id="97f6c-123">Настройте [учетную запись хранения Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) для реплицированных данных.</span><span class="sxs-lookup"><span data-stu-id="97f6c-123">Set up an [Azure storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) for replicated data.</span></span>
- <span data-ttu-id="97f6c-124">Используя службу Site Recovery на портале Azure, можно настроить учетные записи хранения в Resource Manager или в классическом режиме.</span><span class="sxs-lookup"><span data-stu-id="97f6c-124">Site Recovery in the Azure portal can use storage accounts set up in Resource Manager, or in classic mode.</span></span>
- <span data-ttu-id="97f6c-125">Учетная запись хранения может быть уровня "Стандартный" или [Премиум](../storage/common/storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="97f6c-125">The storage account can be standard or [premium](../storage/common/storage-premium-storage.md).</span></span>
- <span data-ttu-id="97f6c-126">Если вы настроите учетную запись уровня "Премиум", вам также понадобится дополнительная учетная запись уровня "Стандартный" для данных журнала.</span><span class="sxs-lookup"><span data-stu-id="97f6c-126">If you set up a premium account, you will also need an additional standard account for log data.</span></span>


## <a name="next-steps"></a><span data-ttu-id="97f6c-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="97f6c-127">Next steps</span></span>

<span data-ttu-id="97f6c-128">Перейдите к разделу [Шаг 6. Подготовка ресурсов VMware](vmware-walkthrough-prepare-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="97f6c-128">Go to [Step 6: Prepare VMware resources](vmware-walkthrough-prepare-vmware.md)</span></span>
