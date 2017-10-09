---
title: "Необходимые условия hello aaaReview для репликации tooAzure по Hyper-V (без System Center VMM) с помощью Azure Site Recovery | Документы Microsoft"
description: "Описание предварительных требований hello для настройки репликации, отработки отказа и восстановления локальных виртуальных машин Hyper-V tooAzure с Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 7ef3fb46-52f5-4c8a-b1a1-658c2305762a
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 3eefc3b7e3982ec6c413c1db7f7784863f9c701d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-hyper-v-without-vmm-tooazure-replication"></a><span data-ttu-id="e6b7f-103">Шаг 2: Просмотрите hello необходимые условия для tooAzure репликации Hyper-V (без VMM)</span><span class="sxs-lookup"><span data-stu-id="e6b7f-103">Step 2: Review hello prerequisites for Hyper-V (without VMM) tooAzure replication</span></span>

<span data-ttu-id="e6b7f-104">Предварительные требования Hello, приведены в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="e6b7f-104">hello prerequisites are summarized in hello table.</span></span>


<span data-ttu-id="e6b7f-105">**Предварительные требования**</span><span class="sxs-lookup"><span data-stu-id="e6b7f-105">**Prerequisite**</span></span> | <span data-ttu-id="e6b7f-106">**Дополнительные сведения**</span><span class="sxs-lookup"><span data-stu-id="e6b7f-106">**Details**</span></span> 
--- | --- 
<span data-ttu-id="e6b7f-107">**Таблицы Azure**</span><span class="sxs-lookup"><span data-stu-id="e6b7f-107">**Azure**</span></span> | <span data-ttu-id="e6b7f-108">Ознакомьтесь с [требованиями Azure](site-recovery-prereq.md#azure-requirements).</span><span class="sxs-lookup"><span data-stu-id="e6b7f-108">Learn about [Azure requirements](site-recovery-prereq.md#azure-requirements).</span></span>
<span data-ttu-id="e6b7f-109">**Локальные серверы**</span><span class="sxs-lookup"><span data-stu-id="e6b7f-109">**On-premises servers**</span></span> | <span data-ttu-id="e6b7f-110">[Дополнительные сведения](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) о требованиях для узлов Hyper-V hello в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="e6b7f-110">[Learn more](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) about requirements for hello on-premises Hyper-V hosts.</span></span>
<span data-ttu-id="e6b7f-111">**Локальные виртуальные машины Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="e6b7f-111">**On-premises Hyper-V VMs**</span></span> | <span data-ttu-id="e6b7f-112">Виртуальные машины, нужно tooreplicate должна быть запущена [поддерживаемой операционной системы](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)и соответствовать [Azure необходимые условия](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="e6b7f-112">VMs you want tooreplicate should be running a [supported operating system](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions), and conform with [Azure prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
<span data-ttu-id="e6b7f-113">**URL-адреса Azure**</span><span class="sxs-lookup"><span data-stu-id="e6b7f-113">**Azure URLs**</span></span> | <span data-ttu-id="e6b7f-114">Узлы Hyper-V требуется доступ к toothese URL-адреса:</span><span class="sxs-lookup"><span data-stu-id="e6b7f-114">Hyper-V hosts need access toothese URLs:</span></span><br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> <span data-ttu-id="e6b7f-115">Если правила брандмауэра на основе адресов IP, убедитесь, что они позволяют tooAzure связи.</span><span class="sxs-lookup"><span data-stu-id="e6b7f-115">If you have IP address-based firewall rules, ensure they allow communication tooAzure.</span></span><br/></br> <span data-ttu-id="e6b7f-116">Разрешить hello [диапазоны IP-адресов центра обработки данных Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)и hello порта HTTPS (443).</span><span class="sxs-lookup"><span data-stu-id="e6b7f-116">Allow hello [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and hello HTTPS (443) port.</span></span><br/></br> <span data-ttu-id="e6b7f-117">Разрешить диапазоны IP-адресов для hello регион Azure, подписки и Запад США (используется для контроля доступа и удостоверений).</span><span class="sxs-lookup"><span data-stu-id="e6b7f-117">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>



## <a name="next-steps"></a><span data-ttu-id="e6b7f-118">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e6b7f-118">Next steps</span></span>

- <span data-ttu-id="e6b7f-119">При выполнении полного развертывания, перейдите в слишком[Step 3: Планирование емкости](hyper-v-site-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="e6b7f-119">If you're doing a full deployment, go too[Step 3: Plan capacity](hyper-v-site-walkthrough-capacity.md)</span></span>
- <span data-ttu-id="e6b7f-120">Если вы выполняете развертывание простых тестов, слишком перейдите[шаг 4: Планирование сети](hyper-v-site-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="e6b7f-120">If you're doing a simple test deployment, go too[Step 4: Plan networking](hyper-v-site-walkthrough-network.md).</span></span>
