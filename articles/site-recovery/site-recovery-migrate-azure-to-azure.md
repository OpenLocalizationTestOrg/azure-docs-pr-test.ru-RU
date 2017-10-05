---
title: "Миграция виртуальных машин IaaS в Azure между регионами Azure | Документация Майкрософт"
description: "Используйте службу Site Recovery для переноса виртуальных машин IaaS Azure из одного региона Azure в другой."
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
ms.openlocfilehash: ef2972c077a2b1dd2b2fd6ce53cc6560520ea870
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-azure-iaas-virtual-machines-between-azure-regions-with-azure-site-recovery"></a><span data-ttu-id="f12e8-103">Перенос виртуальных машин IaaS Azure между регионами Azure с помощью Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="f12e8-103">Migrate Azure IaaS virtual machines between Azure regions with Azure Site Recovery</span></span>
## <a name="overview"></a><span data-ttu-id="f12e8-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="f12e8-104">Overview</span></span>
<span data-ttu-id="f12e8-105">Вас приветствует служба Azure Site Recovery!</span><span class="sxs-lookup"><span data-stu-id="f12e8-105">Welcome to Azure Site Recovery!</span></span> <span data-ttu-id="f12e8-106">Воспользуйтесь этой статьей для выполнения переноса виртуальных машин Azure из одного региона Azure в другой.</span><span class="sxs-lookup"><span data-stu-id="f12e8-106">Use this article if you want to migrate Azure VMs between Azure regions.</span></span> <span data-ttu-id="f12e8-107">Перед началом работы обратите внимание на следующее:</span><span class="sxs-lookup"><span data-stu-id="f12e8-107">Before you start, note that:</span></span>

* <span data-ttu-id="f12e8-108">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: модель Azure Resource Manager и классическая модель.</span><span class="sxs-lookup"><span data-stu-id="f12e8-108">Azure has two different deployment models for creating and working with resources: Azure Resource Manager and classic.</span></span> <span data-ttu-id="f12e8-109">Кроме того, Azure предоставляет два портала — классический портал Azure, поддерживающий классическую модель развертывания, и портал Azure, поддерживающий обе модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="f12e8-109">Azure also has two portals – the Azure classic portal that supports the classic deployment model, and the Azure portal with support for both deployment models.</span></span> <span data-ttu-id="f12e8-110">Основные шаги, необходимые для выполнения переноса, одинаковы при настройке Site Recovery как с помощью модели Resource Manager, так и с помощью классической модели.</span><span class="sxs-lookup"><span data-stu-id="f12e8-110">The basic steps for migration are the same whether you're configuring Site Recovery in Resource Manager or in classic.</span></span> <span data-ttu-id="f12e8-111">Приводимые в этой статье элементы пользовательского интерфейса и снимки экрана относятся к порталу Azure.</span><span class="sxs-lookup"><span data-stu-id="f12e8-111">However the UI instructions and screenshots in this article are relevant for the Azure portal.</span></span>
* <span data-ttu-id="f12e8-112">**В настоящее время поддерживается только перенос из одного региона в другой. Вы можете выполнить отработку отказа виртуальных машин из одного региона Azure в другой, но не сможете выполнить обратную отработку отказа этих виртуальных машин.**</span><span class="sxs-lookup"><span data-stu-id="f12e8-112">**Currently you can only migrate from one region to another. You can fail over VMs from one Azure region to another, but you can't fail them back again.**</span></span>

<span data-ttu-id="f12e8-113">Комментарии или вопросы можно добавить в конце этой статьи или на [форуме по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="f12e8-113">Post any comments or questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f12e8-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f12e8-114">Prerequisites</span></span>
<span data-ttu-id="f12e8-115">Вот что нужно для этого развертывания:</span><span class="sxs-lookup"><span data-stu-id="f12e8-115">Here's what you need for this deployment:</span></span>

* <span data-ttu-id="f12e8-116">**Виртуальные машины IaaS**— виртуальные машины, которые требуется перенести.</span><span class="sxs-lookup"><span data-stu-id="f12e8-116">**IaaS virtual machines**: The VMs you want to migrate.</span></span> <span data-ttu-id="f12e8-117">При переносе виртуальных машин используйте те же инструкции, что и для физических компьютеров.</span><span class="sxs-lookup"><span data-stu-id="f12e8-117">You migrate these VMs by treating them as physical machines.</span></span>

## <a name="deployment-steps"></a><span data-ttu-id="f12e8-118">Шаги по развертыванию</span><span class="sxs-lookup"><span data-stu-id="f12e8-118">Deployment steps</span></span>
<span data-ttu-id="f12e8-119">В этом разделе описаны шаги по развертыванию на новом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="f12e8-119">This section describes the deployment steps in the new Azure portal.</span></span>

1. <span data-ttu-id="f12e8-120">[Создайте хранилище](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="f12e8-120">[Create a vault](site-recovery-vmware-to-azure.md).</span></span>
2. <span data-ttu-id="f12e8-121">[Включите репликацию](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="f12e8-121">[Enable replication](site-recovery-vmware-to-azure.md).</span></span> <span data-ttu-id="f12e8-122">Включите репликацию для виртуальных машин, которые требуется перенести, и выберите Azure в качестве источника.</span><span class="sxs-lookup"><span data-stu-id="f12e8-122">Enable replication for the VMs you want to migrate, and choose Azure as source.</span></span> 
3. <span data-ttu-id="f12e8-123">[ Запустите внеплановую отработку отказа](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="f12e8-123">[ Run an unplanned failover](site-recovery-failover.md).</span></span> <span data-ttu-id="f12e8-124">После завершения начальной репликации вы можете запустить внеплановую отработку отказа из одного региона Azure в другой.</span><span class="sxs-lookup"><span data-stu-id="f12e8-124">After initial replication is complete, you can run an unplanned failover from one Azure region to another.</span></span> <span data-ttu-id="f12e8-125">При необходимости вы можете создать план восстановления и запустить внеплановую отработку отказа, чтобы перенести несколько виртуальных машин между регионами.</span><span class="sxs-lookup"><span data-stu-id="f12e8-125">Optionally, you can create a recovery plan and run an unplanned failover, to migrate multiple virtual machines between regions.</span></span> <span data-ttu-id="f12e8-126">[Узнайте подробнее](site-recovery-create-recovery-plans.md) о планах восстановления.</span><span class="sxs-lookup"><span data-stu-id="f12e8-126">[Learn more](site-recovery-create-recovery-plans.md) about recovery plans.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f12e8-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f12e8-127">Next steps</span></span>
<span data-ttu-id="f12e8-128">Сведения о других сценариях репликации см. в статье [Что такое Site Recovery?](site-recovery-overview.md)</span><span class="sxs-lookup"><span data-stu-id="f12e8-128">Learn more about other replication scenarios in [What is Azure Site Recovery?](site-recovery-overview.md)</span></span>
