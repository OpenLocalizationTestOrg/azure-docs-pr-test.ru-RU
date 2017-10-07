---
title: "aaaSubscription и учетные записи для виртуальных машин Windows в Azure | Документы Microsoft"
description: "Дополнительные сведения о hello ключевые проектирования и реализации рекомендации для подписок и учетных записей в Azure."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 761fa847-78b0-4078-a33a-d95d198d1029
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f9dc712af559b04490be1dc721a9b9f7fe9ed88f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-accounts-guidelines-for-windows-vms"></a><span data-ttu-id="1a840-103">Рекомендации по подпискам и учетным записям Azure для виртуальных машин Windows</span><span class="sxs-lookup"><span data-stu-id="1a840-103">Azure subscription and accounts guidelines for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="1a840-104">Это статье рассматриваются основные сведения о том, как растет tooapproach подписки и управление учетными записями в вашей среде и пользовательской базы.</span><span class="sxs-lookup"><span data-stu-id="1a840-104">This article focuses on understanding how tooapproach subscription and account management as your environment and user base grows.</span></span>

## <a name="implementation-guidelines-for-subscriptions-and-accounts"></a><span data-ttu-id="1a840-105">Рекомендации по реализации подписок и учетных записей</span><span class="sxs-lookup"><span data-stu-id="1a840-105">Implementation guidelines for subscriptions and accounts</span></span>
<span data-ttu-id="1a840-106">Решения</span><span class="sxs-lookup"><span data-stu-id="1a840-106">Decisions:</span></span>

* <span data-ttu-id="1a840-107">Какой набор подписок и учетных записей необходимо toohost рабочей нагрузки ИТ или инфраструктуры?</span><span class="sxs-lookup"><span data-stu-id="1a840-107">What set of subscriptions and accounts do you need toohost your IT workload or infrastructure?</span></span>
* <span data-ttu-id="1a840-108">Как toobreak работу toofit иерархии hello вашей организации?</span><span class="sxs-lookup"><span data-stu-id="1a840-108">How toobreak down hello hierarchy toofit your organization?</span></span>

<span data-ttu-id="1a840-109">Задачи</span><span class="sxs-lookup"><span data-stu-id="1a840-109">Tasks:</span></span>

* <span data-ttu-id="1a840-110">Определение иерархии логическую организацию как toomanage его из уровня подписки.</span><span class="sxs-lookup"><span data-stu-id="1a840-110">Define your logical organization hierarchy as you would like toomanage it from a subscription level.</span></span>
* <span data-ttu-id="1a840-111">toomatch этой логической иерархии определения hello требуются учетные записи и подписки в каждой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="1a840-111">toomatch this logical hierarchy, define hello accounts required and subscriptions under each account.</span></span>
* <span data-ttu-id="1a840-112">Создайте набор hello подписками и учетными записями с помощью имен.</span><span class="sxs-lookup"><span data-stu-id="1a840-112">Create hello set of subscriptions and accounts using your naming convention.</span></span>

## <a name="subscriptions-and-accounts"></a><span data-ttu-id="1a840-113">Подписки и учетные записи</span><span class="sxs-lookup"><span data-stu-id="1a840-113">Subscriptions and accounts</span></span>
<span data-ttu-id="1a840-114">toowork с Azure требуется один или несколько подписок Azure.</span><span class="sxs-lookup"><span data-stu-id="1a840-114">toowork with Azure, you need one or more Azure subscriptions.</span></span> <span data-ttu-id="1a840-115">В них размещаются такие ресурсы, как виртуальные машины или виртуальные сети.</span><span class="sxs-lookup"><span data-stu-id="1a840-115">Resources like virtual machines (VMs) or virtual networks exist in of those subscriptions.</span></span>

* <span data-ttu-id="1a840-116">Корпоративные клиенты обычно имеют регистрации на предприятии, который hello ресурсов верхнего уровня в иерархии hello и связанные tooone или несколько учетных записей.</span><span class="sxs-lookup"><span data-stu-id="1a840-116">Enterprise customers typically have an Enterprise Enrollment, which is hello top-most resource in hello hierarchy, and is associated tooone or more accounts.</span></span>
* <span data-ttu-id="1a840-117">Для клиентов без регистрации на предприятии потребителей ресурсов hello верхнего уровня — учетная запись hello.</span><span class="sxs-lookup"><span data-stu-id="1a840-117">For consumers and customers without an Enterprise Enrollment, hello top-most resource is hello account.</span></span>
* <span data-ttu-id="1a840-118">Подписки, связанные tooaccounts и может быть один или несколько подписок на учетную запись.</span><span class="sxs-lookup"><span data-stu-id="1a840-118">Subscriptions are associated tooaccounts, and there can be one or more subscriptions per account.</span></span> <span data-ttu-id="1a840-119">Выставление счетов сведения на уровне подписки hello Azure записей.</span><span class="sxs-lookup"><span data-stu-id="1a840-119">Azure records billing information at hello subscription level.</span></span>

<span data-ttu-id="1a840-120">Из-за предел toohello две иерархии уровней на связь hello учетной записи и подписки это важно tooalign hello именования toohello учетными записями и подписками, выставление счетов потребностей.</span><span class="sxs-lookup"><span data-stu-id="1a840-120">Due toohello limit of two hierarchy levels on hello Account/Subscription relationship, it is important tooalign hello naming convention of accounts and subscriptions toohello billing needs.</span></span> <span data-ttu-id="1a840-121">Для экземпляра глобальной компании использует Azure, они могут выбрать учетную запись toohave один по регионам, и иметь подписок, управляемых в hello уровень регион:</span><span class="sxs-lookup"><span data-stu-id="1a840-121">For instance, if a global company uses Azure, they might choose toohave one account per region, and have subscriptions managed at hello region level:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub01.png)

<span data-ttu-id="1a840-122">Например можно использовать hello следующие структуры:</span><span class="sxs-lookup"><span data-stu-id="1a840-122">For instance, you might use hello following structure:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub02.png)

<span data-ttu-id="1a840-123">Если область решает toohave больше, чем одной подписке связанного tooa определенной группы, соглашение об именовании hello должно учитываться tooencode способом hello дополнительные данные в учетной записи hello или имя подписки hello.</span><span class="sxs-lookup"><span data-stu-id="1a840-123">If a region decides toohave more than one subscription associated tooa particular group, hello naming convention should incorporate a way tooencode hello extra data on either hello account or hello subscription name.</span></span> <span data-ttu-id="1a840-124">Такая организация позволяет уплотнения выставления счетов данных toogenerate hello новых уровней иерархии во время выставления счетов отчетов:</span><span class="sxs-lookup"><span data-stu-id="1a840-124">This organization allows massaging billing data toogenerate hello new levels of hierarchy during billing reports:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub03.png)

<span data-ttu-id="1a840-125">Hello организации может выглядеть как следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="1a840-125">hello organization could look like hello following example:</span></span>

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub04.png)

<span data-ttu-id="1a840-126">Мы выставляем детализированные счета в виде скачиваемого файла для одной учетной записи или для всех учетных записей, включенных в Соглашение Enterprise.</span><span class="sxs-lookup"><span data-stu-id="1a840-126">We provide detailed billing via a downloadable file for a single account, or for all accounts in an enterprise agreement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a840-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1a840-127">Next steps</span></span>
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

