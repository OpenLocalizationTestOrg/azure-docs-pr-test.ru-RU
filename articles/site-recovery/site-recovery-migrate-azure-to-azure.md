---
title: "aaaMigrate виртуальные машины IaaS Azure между регионами Azure | Документы Microsoft"
description: "Используйте виртуальные машины Azure IaaS Azure Site Recovery toomigrate из tooanother один регион Azure."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8a29e0d9-0010-4739-972f-02b8bdf360f6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: c84dc77716b8d19969eab60707ed1332ca39b893
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-iaas-virtual-machines-between-azure-regions-with-azure-site-recovery"></a><span data-ttu-id="8cfb6-103">Перенос виртуальных машин IaaS Azure между регионами Azure с помощью Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="8cfb6-103">Migrate Azure IaaS virtual machines between Azure regions with Azure Site Recovery</span></span>
## <a name="overview"></a><span data-ttu-id="8cfb6-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="8cfb6-104">Overview</span></span>
<span data-ttu-id="8cfb6-105">Вас приветствует tooAzure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="8cfb6-105">Welcome tooAzure Site Recovery!</span></span> <span data-ttu-id="8cfb6-106">В этой статье следует используйте, если необходимо, чтобы виртуальные машины Azure toomigrate между регионами Azure.</span><span class="sxs-lookup"><span data-stu-id="8cfb6-106">Use this article if you want toomigrate Azure VMs between Azure regions.</span></span> <span data-ttu-id="8cfb6-107">Перед началом работы обратите внимание на следующее:</span><span class="sxs-lookup"><span data-stu-id="8cfb6-107">Before you start, note that:</span></span>

* <span data-ttu-id="8cfb6-108">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: модель Azure Resource Manager и классическая модель.</span><span class="sxs-lookup"><span data-stu-id="8cfb6-108">Azure has two different deployment models for creating and working with resources: Azure Resource Manager and classic.</span></span> <span data-ttu-id="8cfb6-109">Azure также содержит два портала — hello классический портал Azure, поддерживающий hello классической модели развертывания и hello портал Azure с поддержкой обе модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="8cfb6-109">Azure also has two portals – hello Azure classic portal that supports hello classic deployment model, and hello Azure portal with support for both deployment models.</span></span> <span data-ttu-id="8cfb6-110">Hello основные шаги для миграции: hello же ли в диспетчере ресурсов или в классическом настраиваете Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="8cfb6-110">hello basic steps for migration are hello same whether you're configuring Site Recovery in Resource Manager or in classic.</span></span> <span data-ttu-id="8cfb6-111">Однако hello инструкции пользовательского интерфейса и снимки экрана в этой статье относятся к hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8cfb6-111">However hello UI instructions and screenshots in this article are relevant for hello Azure portal.</span></span>
* <span data-ttu-id="8cfb6-112">**В настоящее время только можно переносить из одного региона tooanother. Можно выполнить переход виртуальных машин из одного региона Azure tooanother, но вы не удается восстановить после сбоя их еще раз.**</span><span class="sxs-lookup"><span data-stu-id="8cfb6-112">**Currently you can only migrate from one region tooanother. You can fail over VMs from one Azure region tooanother, but you can't fail them back again.**</span></span>

<span data-ttu-id="8cfb6-113">Отправьте все комментарии или вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="8cfb6-113">Post any comments or questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8cfb6-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8cfb6-114">Prerequisites</span></span>
<span data-ttu-id="8cfb6-115">Вот что нужно для этого развертывания:</span><span class="sxs-lookup"><span data-stu-id="8cfb6-115">Here's what you need for this deployment:</span></span>

* <span data-ttu-id="8cfb6-116">**Виртуальные машины IaaS**: hello требуется toomigrate виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="8cfb6-116">**IaaS virtual machines**: hello VMs you want toomigrate.</span></span> <span data-ttu-id="8cfb6-117">При переносе виртуальных машин используйте те же инструкции, что и для физических компьютеров.</span><span class="sxs-lookup"><span data-stu-id="8cfb6-117">You migrate these VMs by treating them as physical machines.</span></span>

## <a name="deployment-steps"></a><span data-ttu-id="8cfb6-118">Шаги по развертыванию</span><span class="sxs-lookup"><span data-stu-id="8cfb6-118">Deployment steps</span></span>
<span data-ttu-id="8cfb6-119">Этот раздел описывает шаги развертывания hello hello новый портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8cfb6-119">This section describes hello deployment steps in hello new Azure portal.</span></span>

1. <span data-ttu-id="8cfb6-120">[Создайте хранилище](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="8cfb6-120">[Create a vault](site-recovery-vmware-to-azure.md).</span></span>
2. <span data-ttu-id="8cfb6-121">[Включите репликацию](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="8cfb6-121">[Enable replication](site-recovery-vmware-to-azure.md).</span></span> <span data-ttu-id="8cfb6-122">Включите репликацию hello виртуальные машины toomigrate и задайте Azure в качестве источника.</span><span class="sxs-lookup"><span data-stu-id="8cfb6-122">Enable replication for hello VMs you want toomigrate, and choose Azure as source.</span></span> 
3. <span data-ttu-id="8cfb6-123">[ Запустите внеплановую отработку отказа](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="8cfb6-123">[ Run an unplanned failover](site-recovery-failover.md).</span></span> <span data-ttu-id="8cfb6-124">После завершения начальной репликации запускаются незапланированной отработки отказа из одного региона Azure tooanother.</span><span class="sxs-lookup"><span data-stu-id="8cfb6-124">After initial replication is complete, you can run an unplanned failover from one Azure region tooanother.</span></span> <span data-ttu-id="8cfb6-125">При необходимости можно создать план восстановления и запускать несколько виртуальных машин незапланированной отработки отказа, toomigrate между регионами.</span><span class="sxs-lookup"><span data-stu-id="8cfb6-125">Optionally, you can create a recovery plan and run an unplanned failover, toomigrate multiple virtual machines between regions.</span></span> <span data-ttu-id="8cfb6-126">[Узнайте подробнее](site-recovery-create-recovery-plans.md) о планах восстановления.</span><span class="sxs-lookup"><span data-stu-id="8cfb6-126">[Learn more](site-recovery-create-recovery-plans.md) about recovery plans.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8cfb6-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8cfb6-127">Next steps</span></span>
<span data-ttu-id="8cfb6-128">Сведения о других сценариях репликации см. в статье [Что такое Site Recovery?](site-recovery-overview.md)</span><span class="sxs-lookup"><span data-stu-id="8cfb6-128">Learn more about other replication scenarios in [What is Azure Site Recovery?](site-recovery-overview.md)</span></span>
