---
title: "Подписка и учетная запись для виртуальных машин Linux в Azure | Документация Майкрософт"
description: "Изучите основные рекомендации по проектированию и реализации, касающиеся подписок и учетных записей в Azure."
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
ms.openlocfilehash: 19695a9960d8e8f0dfca4bf0ca10761fe6ae7ff0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-subscription-and-accounts-guidelines-for-linux-vms"></a><span data-ttu-id="0a344-103">Рекомендации по подпискам и учетным записям Azure для виртуальных машин Linux</span><span class="sxs-lookup"><span data-stu-id="0a344-103">Azure subscription and accounts guidelines for Linux VMs</span></span>

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="0a344-104">Эта статья посвящена различным подходам к управлению подписками и учетными записями по мере расширения среды и базы пользователей.</span><span class="sxs-lookup"><span data-stu-id="0a344-104">This article focuses on understanding how to approach subscription and account management as your environment and user base grows.</span></span>

## <a name="implementation-guidelines-for-subscriptions-and-accounts"></a><span data-ttu-id="0a344-105">Рекомендации по реализации подписок и учетных записей</span><span class="sxs-lookup"><span data-stu-id="0a344-105">Implementation guidelines for subscriptions and accounts</span></span>
<span data-ttu-id="0a344-106">Решения</span><span class="sxs-lookup"><span data-stu-id="0a344-106">Decisions:</span></span>

* <span data-ttu-id="0a344-107">Какие подписки и учетные записи необходимы для размещения рабочей нагрузки ИТ-среды или ИТ-инфраструктуры?</span><span class="sxs-lookup"><span data-stu-id="0a344-107">What set of subscriptions and accounts do you need to host your IT workload or infrastructure?</span></span>
* <span data-ttu-id="0a344-108">Что должна включать в себя иерархия в соответствии с потребностями вашей организации?</span><span class="sxs-lookup"><span data-stu-id="0a344-108">How to break down the hierarchy to fit your organization?</span></span>

<span data-ttu-id="0a344-109">Задачи</span><span class="sxs-lookup"><span data-stu-id="0a344-109">Tasks:</span></span>

* <span data-ttu-id="0a344-110">Определите логическую иерархию организации с точки зрения управления на уровне подписки.</span><span class="sxs-lookup"><span data-stu-id="0a344-110">Define your logical organization hierarchy as you would like to manage it from a subscription level.</span></span>
* <span data-ttu-id="0a344-111">В соответствии с этой логической иерархией определите необходимые учетные записи и подписки в каждой из них.</span><span class="sxs-lookup"><span data-stu-id="0a344-111">To match this logical hierarchy, define the accounts required and subscriptions under each account.</span></span>
* <span data-ttu-id="0a344-112">Создайте набор подписок и учетных записей с использованием соглашения об именовании.</span><span class="sxs-lookup"><span data-stu-id="0a344-112">Create the set of subscriptions and accounts using your naming convention.</span></span>

## <a name="subscriptions-and-accounts"></a><span data-ttu-id="0a344-113">Подписки и учетные записи</span><span class="sxs-lookup"><span data-stu-id="0a344-113">Subscriptions and accounts</span></span>
<span data-ttu-id="0a344-114">Для работы с Azure требуется одна или несколько подписок Azure.</span><span class="sxs-lookup"><span data-stu-id="0a344-114">To work with Azure, you need one or more Azure subscriptions.</span></span> <span data-ttu-id="0a344-115">В них размещаются такие ресурсы, как виртуальные машины или виртуальные сети.</span><span class="sxs-lookup"><span data-stu-id="0a344-115">Resources like virtual machines (VMs) or virtual networks exist in of those subscriptions.</span></span>

* <span data-ttu-id="0a344-116">Как правило, у корпоративных клиентов есть Соглашение о регистрации Enterprise, которое считается ресурсом самого верхнего уровня в иерархии и сопоставлено с одной или несколькими учетными записями.</span><span class="sxs-lookup"><span data-stu-id="0a344-116">Enterprise customers typically have an Enterprise Enrollment, which is the top-most resource in the hierarchy, and is associated to one or more accounts.</span></span>
* <span data-ttu-id="0a344-117">Для клиентов без Соглашения о регистрации Enterprise ресурсом верхнего уровня считается учетная запись.</span><span class="sxs-lookup"><span data-stu-id="0a344-117">For consumers and customers without an Enterprise Enrollment, the top-most resource is the account.</span></span>
* <span data-ttu-id="0a344-118">Подписки сопоставлены с учетными записями. С одной учетной записью может быть связано несколько подписок.</span><span class="sxs-lookup"><span data-stu-id="0a344-118">Subscriptions are associated to accounts, and there can be one or more subscriptions per account.</span></span> <span data-ttu-id="0a344-119">Azure хранит данные для выставления счетов на уровне подписки.</span><span class="sxs-lookup"><span data-stu-id="0a344-119">Azure records billing information at the subscription level.</span></span>

<span data-ttu-id="0a344-120">Так как количество уровней иерархии для связи между учетной записью и подпиской ограничено двумя, важно, чтобы соглашение об именовании для учетных записей и подписок соответствовало требованиям к выставлению счетов.</span><span class="sxs-lookup"><span data-stu-id="0a344-120">Due to the limit of two hierarchy levels on the Account/Subscription relationship, it is important to align the naming convention of accounts and subscriptions to the billing needs.</span></span> <span data-ttu-id="0a344-121">Например, если в транснациональной компании используется Azure, то можно создать по одной учетной записи на регион и управлять подписками на уровне региона.</span><span class="sxs-lookup"><span data-stu-id="0a344-121">For instance, if a global company uses Azure, they might choose to have one account per region, and have subscriptions managed at the region level:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub01.png)

<span data-ttu-id="0a344-122">Например, можно использовать указанную ниже структуру.</span><span class="sxs-lookup"><span data-stu-id="0a344-122">For instance, you might use the following structure:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub02.png)

<span data-ttu-id="0a344-123">Если нужно сопоставить несколько подписок для региона с определенной группой, то соглашение об именовании должно предусматривать способ указания дополнительных данных в имени учетной записи или подписки.</span><span class="sxs-lookup"><span data-stu-id="0a344-123">If a region decides to have more than one subscription associated to a particular group, the naming convention should incorporate a way to encode the extra data on either the account or the subscription name.</span></span> <span data-ttu-id="0a344-124">Такая организация позволяет уплотнять данные для выставления счетов, чтобы можно было создавать уровни иерархии во время отправки отчетов о выставлении счетов.</span><span class="sxs-lookup"><span data-stu-id="0a344-124">This organization allows massaging billing data to generate the new levels of hierarchy during billing reports:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub03.png)

<span data-ttu-id="0a344-125">Организация может выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="0a344-125">The organization could look like the following example:</span></span>

![](media/virtual-machines-common-infrastructure-service-guidelines/sub04.png)

<span data-ttu-id="0a344-126">Мы выставляем детализированные счета в виде скачиваемого файла для одной учетной записи или для всех учетных записей, включенных в Соглашение Enterprise.</span><span class="sxs-lookup"><span data-stu-id="0a344-126">We provide detailed billing via a downloadable file for a single account, or for all accounts in an enterprise agreement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a344-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0a344-127">Next steps</span></span>
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

