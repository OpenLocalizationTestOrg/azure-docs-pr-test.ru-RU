---
title: "aaaUsing hello администратора и пользователя порталы в стек Azure | Документы Microsoft"
description: "Узнайте hello различия между hello порталы администратора и пользователя в Azure стека."
services: azure-stack
documentationcenter: 
author: twooley
manager: byronr
editor: 
ms.assetid: 02c7ff03-874e-4951-b591-28166b7a7a79
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: twooley
ms.openlocfilehash: 5e940749917e4aade26483a79bcc238346bf94f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-administrator-and-user-portals-in-azure-stack"></a><span data-ttu-id="3f827-103">С помощью hello порталы администратора и пользователя в стек Azure</span><span class="sxs-lookup"><span data-stu-id="3f827-103">Using hello administrator and user portals in Azure Stack</span></span>

<span data-ttu-id="3f827-104">Существует два портала Azure стека; Здравствуйте, административный портал и портал пользователей hello (также называется tooas hello *клиента* портала).</span><span class="sxs-lookup"><span data-stu-id="3f827-104">There are two portals in Azure Stack; hello administrator portal and hello user portal (also referred tooas hello *tenant* portal).</span></span> <span data-ttu-id="3f827-105">порталы Hello, поддерживаемых отдельными экземплярами диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="3f827-105">hello portals are backed by separate instances of Azure Resource Manager.</span></span>

<span data-ttu-id="3f827-106">Hello следующей таблице показано, как tooconnect toohello порталов и конечные точки диспетчера tooResource в среде Azure стека Development Kit.</span><span class="sxs-lookup"><span data-stu-id="3f827-106">hello following table shows how tooconnect toohello portals and tooResource Manager endpoints in an Azure Stack Development Kit environment.</span></span>

|  <span data-ttu-id="3f827-107">Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="3f827-107">Portal</span></span> | <span data-ttu-id="3f827-108">URL-адрес портала</span><span class="sxs-lookup"><span data-stu-id="3f827-108">Portal URL</span></span> | <span data-ttu-id="3f827-109">URL-адрес конечной точки диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="3f827-109">Resource Manager endpoint URL</span></span> |   
| -------- | ------------- | ------- |  
| <span data-ttu-id="3f827-110">Администратор</span><span class="sxs-lookup"><span data-stu-id="3f827-110">Administrator</span></span> | <span data-ttu-id="3f827-111">https://adminportal.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="3f827-111">https://adminportal.local.azurestack.external</span></span>  | <span data-ttu-id="3f827-112">https://adminmanagement.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="3f827-112">https://adminmanagement.local.azurestack.external</span></span>  |  
| <span data-ttu-id="3f827-113">Пользователь</span><span class="sxs-lookup"><span data-stu-id="3f827-113">User</span></span> | <span data-ttu-id="3f827-114">https://Portal.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="3f827-114">https://portal.local.azurestack.external</span></span> | <span data-ttu-id="3f827-115">https://Management.local.azurestack.external</span><span class="sxs-lookup"><span data-stu-id="3f827-115">https://management.local.azurestack.external</span></span>  |
| | |

## <a name="hello-administrator-portal"></a><span data-ttu-id="3f827-116">портал администратора Hello</span><span class="sxs-lookup"><span data-stu-id="3f827-116">hello administrator portal</span></span>

<span data-ttu-id="3f827-117">портал администратора Hello позволяет облака оператор tooperform административного или оперативного задачам.</span><span class="sxs-lookup"><span data-stu-id="3f827-117">hello administrator portal enables a cloud operator tooperform administrative and operational tasks.</span></span> <span data-ttu-id="3f827-118">Оператор облака можно использовать следующие функции:</span><span class="sxs-lookup"><span data-stu-id="3f827-118">A cloud operator can do things such as:</span></span>
* <span data-ttu-id="3f827-119">Монитор работоспособности и предупреждений</span><span class="sxs-lookup"><span data-stu-id="3f827-119">monitor health and alerts</span></span>
* <span data-ttu-id="3f827-120">Управление емкостью</span><span class="sxs-lookup"><span data-stu-id="3f827-120">manage capacity</span></span>
* <span data-ttu-id="3f827-121">Заполнение hello marketplace</span><span class="sxs-lookup"><span data-stu-id="3f827-121">populate hello marketplace</span></span>
* <span data-ttu-id="3f827-122">Создание планов и предложения</span><span class="sxs-lookup"><span data-stu-id="3f827-122">create plans and offers</span></span>
* <span data-ttu-id="3f827-123">Создание подписки для клиентов</span><span class="sxs-lookup"><span data-stu-id="3f827-123">create subscriptions for tenants</span></span>

<span data-ttu-id="3f827-124">Оператор облака можно также создать ресурсы, такие как виртуальных машин, виртуальных сетей и учетные записи хранения.</span><span class="sxs-lookup"><span data-stu-id="3f827-124">A cloud operator can also create resources such as virtual machines, virtual networks, and storage accounts.</span></span>

 ![портал администратора Hello](media/azure-stack-manage-portals/image1.png)

 ## <a name="hello-user-portal"></a><span data-ttu-id="3f827-126">Hello пользовательского портала</span><span class="sxs-lookup"><span data-stu-id="3f827-126">hello user portal</span></span>

 <span data-ttu-id="3f827-127">пользовательский портал Hello не предоставляет доступа tooany hello администратора или рабочих возможностей hello администратора портала.</span><span class="sxs-lookup"><span data-stu-id="3f827-127">hello user portal does not provide access tooany of hello administrative or operational capabilities of hello administrator portal.</span></span> <span data-ttu-id="3f827-128">В пользовательском портале hello пользователя можно подписаться toopublic предложений и использовать hello служб, которые становятся доступными через эти предложения.</span><span class="sxs-lookup"><span data-stu-id="3f827-128">In hello user portal, a user can subscribe toopublic offers, and use hello services that are made available through those offers.</span></span>

  ![Hello пользовательского портала](media/azure-stack-manage-portals/image2.png)
 
 ## <a name="subscription-behavior"></a><span data-ttu-id="3f827-130">Поведение подписки</span><span class="sxs-lookup"><span data-stu-id="3f827-130">Subscription behavior</span></span>
 
 <span data-ttu-id="3f827-131">Убедитесь, что вы понимаете следующие различия между поведение подписки на порталах hello двух hello.</span><span class="sxs-lookup"><span data-stu-id="3f827-131">Make sure that you understand hello following differences between subscription behavior in hello two portals.</span></span>

 <span data-ttu-id="3f827-132">Портал администратора:</span><span class="sxs-lookup"><span data-stu-id="3f827-132">Administrator portal:</span></span>
* <span data-ttu-id="3f827-133">Имеется только одна подписка, которая доступна на портале администратора hello.</span><span class="sxs-lookup"><span data-stu-id="3f827-133">There is only one subscription that is available in hello administrator portal.</span></span> <span data-ttu-id="3f827-134">Эта подписка является hello *подписки поставщика по умолчанию*.</span><span class="sxs-lookup"><span data-stu-id="3f827-134">This subscription is hello *Default Provider Subscription*.</span></span> <span data-ttu-id="3f827-135">Невозможно добавить другие подписки для использования на портале администратора hello.</span><span class="sxs-lookup"><span data-stu-id="3f827-135">You can't add any other subscriptions for use in hello administrator portal.</span></span>
* <span data-ttu-id="3f827-136">Как оператор облака можно добавить подписки для пользователей (включая себя) из портала администратора hello.</span><span class="sxs-lookup"><span data-stu-id="3f827-136">As a cloud operator, you can add subscriptions for your users (including yourself) from hello administrator portal.</span></span> <span data-ttu-id="3f827-137">Доступ и использование этих подписок с hello пользовательского портала пользователей (включая себя).</span><span class="sxs-lookup"><span data-stu-id="3f827-137">Users (including yourself) can access and use these subscriptions from hello user portal.</span></span>

  >[!NOTE]
  <span data-ttu-id="3f827-138">Из-за hello Azure Resource Manager разделение подписки определяются порталов.</span><span class="sxs-lookup"><span data-stu-id="3f827-138">Because of hello Azure Resource Manager separation, subscriptions do not cross portals.</span></span> <span data-ttu-id="3f827-139">Например можно с помощью оператора облака входит toohello пользовательский портал, не сможете hello подписки поставщика по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3f827-139">For example, if you as a cloud operator signs in toohello user portal, you can't access hello Default Provider Subscription.</span></span> <span data-ttu-id="3f827-140">Таким образом нет доступа к tooany административных функций.</span><span class="sxs-lookup"><span data-stu-id="3f827-140">Therefore, you don't have access tooany administrative functions.</span></span> <span data-ttu-id="3f827-141">Можно создать подписки для текущего пользователя из открытых предложений, но считаются пользователя клиента.</span><span class="sxs-lookup"><span data-stu-id="3f827-141">You can create subscriptions for yourself from public offers, but you are considered a tenant user.</span></span>

<span data-ttu-id="3f827-142">Портал пользователей:</span><span class="sxs-lookup"><span data-stu-id="3f827-142">User portal:</span></span>
* <span data-ttu-id="3f827-143">Hello пользователя портала учетной записи может иметь несколько подписок.</span><span class="sxs-lookup"><span data-stu-id="3f827-143">In hello user portal, an account can have multiple subscriptions.</span></span>

  >[!NOTE]
  <span data-ttu-id="3f827-144">В среде kit hello разработки, если пользователь клиента относится toohello один каталог как оператор облака hello, они являются не сможет войти в портал администратора toohello.</span><span class="sxs-lookup"><span data-stu-id="3f827-144">In hello development kit environment, if a tenant user belongs toohello same directory as hello cloud operator, they are not blocked from signing in toohello administrator portal.</span></span> <span data-ttu-id="3f827-145">Однако они недоступны некоторые административные функции hello.</span><span class="sxs-lookup"><span data-stu-id="3f827-145">However, they can't access any of hello administrative functions.</span></span> <span data-ttu-id="3f827-146">Кроме того, они не удается добавить подписки или доступа предоставляет доступные toothem вносятся в hello пользовательского портала.</span><span class="sxs-lookup"><span data-stu-id="3f827-146">Also, they can't add subscriptions or access offers that are made available toothem in hello user portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f827-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3f827-147">Next steps</span></span>

[<span data-ttu-id="3f827-148">Подключение tooAzure стека</span><span class="sxs-lookup"><span data-stu-id="3f827-148">Connect tooAzure Stack</span></span>](azure-stack-connect-azure-stack.md)

[<span data-ttu-id="3f827-149">Область управления в стек Azure</span><span class="sxs-lookup"><span data-stu-id="3f827-149">Region management in Azure Stack</span></span>](azure-stack-region-management.md)
