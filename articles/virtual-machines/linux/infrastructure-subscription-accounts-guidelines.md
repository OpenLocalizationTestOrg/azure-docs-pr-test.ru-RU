---
title: "aaaSubscription и учетной записи для виртуальных машин Linux в Azure | Документы Microsoft"
description: "Дополнительные сведения о hello ключевые проектирования и реализации рекомендации для подписок и учетных записей в Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 19343826-7eef-42a1-98be-4ec65b0f377a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9025a40783c008310ebd0f674deb4a9001ae974a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-accounts-guidelines-for-linux-vms"></a><span data-ttu-id="4fd71-103">Рекомендации по подпискам и учетным записям Azure для виртуальных машин Linux</span><span class="sxs-lookup"><span data-stu-id="4fd71-103">Azure subscription and accounts guidelines for Linux VMs</span></span>

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="4fd71-104">Это статье рассматриваются основные сведения о том, как растет tooapproach подписки и управление учетными записями в вашей среде и пользовательской базы.</span><span class="sxs-lookup"><span data-stu-id="4fd71-104">This article focuses on understanding how tooapproach subscription and account management as your environment and user base grows.</span></span>

## <a name="implementation-guidelines-for-subscriptions-and-accounts"></a><span data-ttu-id="4fd71-105">Рекомендации по реализации подписок и учетных записей</span><span class="sxs-lookup"><span data-stu-id="4fd71-105">Implementation guidelines for subscriptions and accounts</span></span>
<span data-ttu-id="4fd71-106">Решения</span><span class="sxs-lookup"><span data-stu-id="4fd71-106">Decisions:</span></span>

* <span data-ttu-id="4fd71-107">Какой набор подписок и учетных записей необходимо toohost рабочей нагрузки ИТ или инфраструктуры?</span><span class="sxs-lookup"><span data-stu-id="4fd71-107">What set of subscriptions and accounts do you need toohost your IT workload or infrastructure?</span></span>
* <span data-ttu-id="4fd71-108">Как toobreak работу toofit иерархии hello вашей организации?</span><span class="sxs-lookup"><span data-stu-id="4fd71-108">How toobreak down hello hierarchy toofit your organization?</span></span>

<span data-ttu-id="4fd71-109">Задачи</span><span class="sxs-lookup"><span data-stu-id="4fd71-109">Tasks:</span></span>

* <span data-ttu-id="4fd71-110">Определение иерархии логическую организацию как toomanage его из уровня подписки.</span><span class="sxs-lookup"><span data-stu-id="4fd71-110">Define your logical organization hierarchy as you would like toomanage it from a subscription level.</span></span>
* <span data-ttu-id="4fd71-111">toomatch этой логической иерархии определения hello требуются учетные записи и подписки в каждой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="4fd71-111">toomatch this logical hierarchy, define hello accounts required and subscriptions under each account.</span></span>
* <span data-ttu-id="4fd71-112">Создайте набор hello подписками и учетными записями с помощью имен.</span><span class="sxs-lookup"><span data-stu-id="4fd71-112">Create hello set of subscriptions and accounts using your naming convention.</span></span>

## <a name="subscriptions-and-accounts"></a><span data-ttu-id="4fd71-113">Подписки и учетные записи</span><span class="sxs-lookup"><span data-stu-id="4fd71-113">Subscriptions and accounts</span></span>
<span data-ttu-id="4fd71-114">toowork с Azure требуется один или несколько подписок Azure.</span><span class="sxs-lookup"><span data-stu-id="4fd71-114">toowork with Azure, you need one or more Azure subscriptions.</span></span> <span data-ttu-id="4fd71-115">В них размещаются такие ресурсы, как виртуальные машины или виртуальные сети.</span><span class="sxs-lookup"><span data-stu-id="4fd71-115">Resources like virtual machines (VMs) or virtual networks exist in of those subscriptions.</span></span>

* <span data-ttu-id="4fd71-116">Корпоративные клиенты обычно имеют регистрации на предприятии, который hello ресурсов верхнего уровня в иерархии hello и связанные tooone или несколько учетных записей.</span><span class="sxs-lookup"><span data-stu-id="4fd71-116">Enterprise customers typically have an Enterprise Enrollment, which is hello top-most resource in hello hierarchy, and is associated tooone or more accounts.</span></span>
* <span data-ttu-id="4fd71-117">Для клиентов без регистрации на предприятии потребителей ресурсов hello верхнего уровня — учетная запись hello.</span><span class="sxs-lookup"><span data-stu-id="4fd71-117">For consumers and customers without an Enterprise Enrollment, hello top-most resource is hello account.</span></span>
* <span data-ttu-id="4fd71-118">Подписки, связанные tooaccounts и может быть один или несколько подписок на учетную запись.</span><span class="sxs-lookup"><span data-stu-id="4fd71-118">Subscriptions are associated tooaccounts, and there can be one or more subscriptions per account.</span></span> <span data-ttu-id="4fd71-119">Выставление счетов сведения на уровне подписки hello Azure записей.</span><span class="sxs-lookup"><span data-stu-id="4fd71-119">Azure records billing information at hello subscription level.</span></span>

<span data-ttu-id="4fd71-120">Из-за предел toohello две иерархии уровней на связь hello учетной записи и подписки это важно tooalign hello именования toohello учетными записями и подписками, выставление счетов потребностей.</span><span class="sxs-lookup"><span data-stu-id="4fd71-120">Due toohello limit of two hierarchy levels on hello Account/Subscription relationship, it is important tooalign hello naming convention of accounts and subscriptions toohello billing needs.</span></span> <span data-ttu-id="4fd71-121">Для экземпляра глобальной компании использует Azure, они могут выбрать учетную запись toohave один по регионам, и иметь подписок, управляемых в hello уровень регион:</span><span class="sxs-lookup"><span data-stu-id="4fd71-121">For instance, if a global company uses Azure, they might choose toohave one account per region, and have subscriptions managed at hello region level:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub01.png)

<span data-ttu-id="4fd71-122">Например можно использовать hello следующие структуры:</span><span class="sxs-lookup"><span data-stu-id="4fd71-122">For instance, you might use hello following structure:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub02.png)

<span data-ttu-id="4fd71-123">Если область решает toohave больше, чем одной подписке связанного tooa определенной группы, соглашение об именовании hello должно учитываться tooencode способом hello дополнительные данные в учетной записи hello или имя подписки hello.</span><span class="sxs-lookup"><span data-stu-id="4fd71-123">If a region decides toohave more than one subscription associated tooa particular group, hello naming convention should incorporate a way tooencode hello extra data on either hello account or hello subscription name.</span></span> <span data-ttu-id="4fd71-124">Такая организация позволяет уплотнения выставления счетов данных toogenerate hello новых уровней иерархии во время выставления счетов отчетов:</span><span class="sxs-lookup"><span data-stu-id="4fd71-124">This organization allows massaging billing data toogenerate hello new levels of hierarchy during billing reports:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub03.png)

<span data-ttu-id="4fd71-125">Hello организации может выглядеть как следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="4fd71-125">hello organization could look like hello following example:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub04.png)

<span data-ttu-id="4fd71-126">Мы выставляем детализированные счета в виде скачиваемого файла для одной учетной записи или для всех учетных записей, включенных в Соглашение Enterprise.</span><span class="sxs-lookup"><span data-stu-id="4fd71-126">We provide detailed billing via a downloadable file for a single account, or for all accounts in an enterprise agreement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4fd71-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4fd71-127">Next steps</span></span>
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

