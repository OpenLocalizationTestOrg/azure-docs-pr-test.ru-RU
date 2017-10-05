---
title: "Рекомендации Azure Advisor по безопасности | Документация Майкрософт"
description: "Используйте Azure Advisor для повышения безопасности развернутых служб Azure."
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 53be05593c3733ccb27979a3a026414013125779
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="advisor-security-recommendations"></a><span data-ttu-id="6d99e-103">Рекомендации Azure Advisor по безопасности</span><span class="sxs-lookup"><span data-stu-id="6d99e-103">Advisor Security recommendations</span></span>

<span data-ttu-id="6d99e-104">Помощник по Azure предоставляет согласованное сводное представление с рекомендациями для всех ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="6d99e-104">Azure Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources.</span></span> <span data-ttu-id="6d99e-105">Advisor интегрируется с центром безопасности Azure, чтобы вы могли получить рекомендации по безопасности.</span><span class="sxs-lookup"><span data-stu-id="6d99e-105">It integrates with Azure Security Center to bring you security recommendations.</span></span> <span data-ttu-id="6d99e-106">Эти рекомендации можно получить на вкладке **Безопасность** панели мониторинга Помощника.</span><span class="sxs-lookup"><span data-stu-id="6d99e-106">You can get security recommendations from the **Security** tab on the Advisor dashboard.</span></span>

![Кнопка "Безопасность" в Помощнике](./media/advisor-security-recommendations/advisor-security-tab.png)

<span data-ttu-id="6d99e-108">Центр безопасности помогает вам выявлять и предотвращать угрозы, а также принимать ответные меры благодаря более полной информации о состоянии ресурсов Azure и контролю над их безопасностью.</span><span class="sxs-lookup"><span data-stu-id="6d99e-108">Security Center helps you prevent, detect, and respond to threats with increased visibility into and control over the security of your Azure resources.</span></span> <span data-ttu-id="6d99e-109">Он периодически анализирует состояние безопасности ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="6d99e-109">It periodically analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="6d99e-110">Когда Центр безопасности выявляет потенциальные уязвимости системы безопасности, он создает рекомендации.</span><span class="sxs-lookup"><span data-stu-id="6d99e-110">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="6d99e-111">Рекомендации помогают настраивать необходимые элементы управления.</span><span class="sxs-lookup"><span data-stu-id="6d99e-111">The recommendations guide you through the process of configuring the controls you need.</span></span> 

![Вкладка "Безопасность" в Помощнике](./media/advisor-security-recommendations/advisor-security-recommendations.png)

<span data-ttu-id="6d99e-113">Дополнительные сведения о рекомендациях по безопасности см. в разделе [Управление рекомендациями по безопасности в Центре безопасности Azure](https://azure.microsoft.com/en-us/documentation/articles/security-center-recommendations/).</span><span class="sxs-lookup"><span data-stu-id="6d99e-113">For more information about security recommendations, see [Managing security recommendations in Azure Security Center](https://azure.microsoft.com/en-us/documentation/articles/security-center-recommendations/).</span></span>

## <a name="how-to-access-security-recommendations-in-azure-advisor"></a><span data-ttu-id="6d99e-114">Как получить доступ к рекомендации по безопасности в Помощнике по Azure</span><span class="sxs-lookup"><span data-stu-id="6d99e-114">How to access Security recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="6d99e-115">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6d99e-115">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="6d99e-116">На панели слева щелкните **Больше служб**.</span><span class="sxs-lookup"><span data-stu-id="6d99e-116">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="6d99e-117">В области меню служб в разделе **Мониторинг и управление** щелкните **Помощник по Azure**.</span><span class="sxs-lookup"><span data-stu-id="6d99e-117">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="6d99e-118">Отображается панель мониторинга Помощника.</span><span class="sxs-lookup"><span data-stu-id="6d99e-118">The Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="6d99e-119">На панели мониторинга Помощника выберите вкладку **Безопасность**.</span><span class="sxs-lookup"><span data-stu-id="6d99e-119">On the Advisor dashboard, click the **Security** tab.</span></span>

5. <span data-ttu-id="6d99e-120">Выберите подписку, для которой вы хотите получать рекомендации, и щелкните **Получить рекомендации**.</span><span class="sxs-lookup"><span data-stu-id="6d99e-120">Select the subscription for which you want to receive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="6d99e-121">Для доступа к рекомендациям Помощника необходимо сначала *зарегистрировать* в нем свою подписку.</span><span class="sxs-lookup"><span data-stu-id="6d99e-121">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="6d99e-122">Подписка регистрируется, когда *владелец подписки* открывает панель мониторинга Помощника и нажимает кнопку **Получить рекомендации**.</span><span class="sxs-lookup"><span data-stu-id="6d99e-122">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="6d99e-123">Выполнить данную *операцию достаточно всего один раз*.</span><span class="sxs-lookup"><span data-stu-id="6d99e-123">This is a *one-time operation*.</span></span> <span data-ttu-id="6d99e-124">После регистрации подписки рекомендации Помощника могут просматривать *владельцы*, *участники* или *читатели* подписки, группы ресурсов или конкретного ресурса.</span><span class="sxs-lookup"><span data-stu-id="6d99e-124">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d99e-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6d99e-125">Next steps</span></span>

<span data-ttu-id="6d99e-126">Чтобы узнать больше о рекомендациях Помощника, ознакомьтесь с приведенными ниже материалами.</span><span class="sxs-lookup"><span data-stu-id="6d99e-126">To learn more about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="6d99e-127">Общие сведения об Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="6d99e-127">Introduction to Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="6d99e-128">Приступая к работе с Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="6d99e-128">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="6d99e-129">Рекомендации Azure Advisor по затратам</span><span class="sxs-lookup"><span data-stu-id="6d99e-129">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="6d99e-130">Рекомендации Azure Advisor по производительности</span><span class="sxs-lookup"><span data-stu-id="6d99e-130">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="6d99e-131">Рекомендации Azure Advisor по высокой доступности</span><span class="sxs-lookup"><span data-stu-id="6d99e-131">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)


 
