---
title: "Приступая к работе с Azure Advisor | Документация Майкрософт"
description: "Приступая к работе с Azure Advisor"
services: advisor
documentationcenter: NA
author: manbeenkohli
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/10/2017
ms.author: makohli
ms.openlocfilehash: a662841bebda460d4225e080f16705b3f16fdc46
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-advisor"></a><span data-ttu-id="e75fc-103">Приступая к работе с Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="e75fc-103">Get started with Azure Advisor</span></span>

<span data-ttu-id="e75fc-104">Узнайте, как воспользоваться Помощником на портале Azure и как получить, реализовать, найти и обновить рекомендации.</span><span class="sxs-lookup"><span data-stu-id="e75fc-104">Learn how to access Advisor through the Azure portal, get recommendations, implement recommendations, search for recommendations, and refresh recommendations.</span></span>

## <a name="get-advisor-recommendations"></a><span data-ttu-id="e75fc-105">Получение рекомендаций Advisor</span><span class="sxs-lookup"><span data-stu-id="e75fc-105">Get Advisor recommendations</span></span>

1. <span data-ttu-id="e75fc-106">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e75fc-106">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="e75fc-107">На панели слева щелкните **Больше служб**.</span><span class="sxs-lookup"><span data-stu-id="e75fc-107">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="e75fc-108">В области меню служб в разделе **Мониторинг и управление** щелкните **Помощник по Azure**.</span><span class="sxs-lookup"><span data-stu-id="e75fc-108">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="e75fc-109">Отображается панель мониторинга Помощника.</span><span class="sxs-lookup"><span data-stu-id="e75fc-109">The Advisor dashboard is displayed.</span></span>

   ![Как воспользоваться Azure Advisor с помощью портала Azure](./media/advisor-overview/advisor-azure-portal-menu.png) 

4. <span data-ttu-id="e75fc-111">На панели мониторинга Помощника выберите подписку, для которой вы хотите получать рекомендации.</span><span class="sxs-lookup"><span data-stu-id="e75fc-111">On the Advisor dashboard, select the subscription for which you want to receive recommendations.</span></span>  
<span data-ttu-id="e75fc-112">Панель мониторинга Advisor отображает персонализированные рекомендации для выбранной подписки.</span><span class="sxs-lookup"><span data-stu-id="e75fc-112">The Advisor dashboard displays personalized recommendations for a selected subscription.</span></span> 

5. <span data-ttu-id="e75fc-113">Чтобы получить рекомендации в определенной категории, щелкните одну из вкладок: **Высокая доступность**, **Безопасность**, **Производительность** или **Стоимость**.</span><span class="sxs-lookup"><span data-stu-id="e75fc-113">To get recommendations for a particular category, click one of the tabs: **High Availability**, **Security**, **Performance**, or **Cost**.</span></span>
 
> [!NOTE]
> <span data-ttu-id="e75fc-114">Для доступа к рекомендациям Помощника необходимо сначала *зарегистрировать* в нем свою подписку.</span><span class="sxs-lookup"><span data-stu-id="e75fc-114">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="e75fc-115">Подписка регистрируется, когда *владелец подписки* открывает панель мониторинга Помощника и нажимает кнопку **Получить рекомендации**.</span><span class="sxs-lookup"><span data-stu-id="e75fc-115">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="e75fc-116">Выполнить данную *операцию достаточно всего один раз*.</span><span class="sxs-lookup"><span data-stu-id="e75fc-116">This is a *one-time operation*.</span></span> <span data-ttu-id="e75fc-117">После регистрации подписки рекомендации Помощника могут просматривать *владельцы*, *участники* или *читатели* подписки, группы ресурсов или конкретного ресурса.</span><span class="sxs-lookup"><span data-stu-id="e75fc-117">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

  ![Панель мониторинга Azure Advisor](./media/advisor-overview/advisor-all-tab.png)

## <a name="get-advisor-recommendation-details-and-implement-a-solution"></a><span data-ttu-id="e75fc-119">Получение сведений о рекомендации Помощника и реализация решения</span><span class="sxs-lookup"><span data-stu-id="e75fc-119">Get Advisor recommendation details, and implement a solution</span></span>

<span data-ttu-id="e75fc-120">Колонка **Рекомендация** в Помощнике содержит дополнительные сведения о рекомендации.</span><span class="sxs-lookup"><span data-stu-id="e75fc-120">The **Recommendation** blade in Advisor offers additional information about the recommendation.</span></span> 

1. <span data-ttu-id="e75fc-121">Войдите на [портал Azure](https://portal.azure.com) и откройте [Помощник по Azure](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="e75fc-121">Sign in to the [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="e75fc-122">На панели мониторинга **Рекомендации помощника** щелкните **Получить рекомендации**.</span><span class="sxs-lookup"><span data-stu-id="e75fc-122">On the **Advisor recommendations** dashboard, click **Get recommendations**.</span></span>

3. <span data-ttu-id="e75fc-123">В списке щелкните рекомендацию, дополнительные сведения о которой вы хотите просмотреть.</span><span class="sxs-lookup"><span data-stu-id="e75fc-123">In the list of recommendations, click a recommendation that you want to review in detail.</span></span>  
<span data-ttu-id="e75fc-124">Откроется колонка **Рекомендация**.</span><span class="sxs-lookup"><span data-stu-id="e75fc-124">The **Recommendation** blade is displayed.</span></span>

4. <span data-ttu-id="e75fc-125">В колонке **Рекомендации** просмотрите сведения о действиях, которые необходимо выполнить, чтобы устранить потенциальную проблему или воспользоваться возможностью сократить расходы.</span><span class="sxs-lookup"><span data-stu-id="e75fc-125">On the **Recommendations** blade, review information about actions that you can perform to resolve a potential issue, or take advantage of a cost-saving opportunity.</span></span> 
  
  ![Колонка "Рекомендация" Помощника](./media/advisor-overview/advisor-recommendation-action-example.png)

## <a name="search-for-advisor-recommendations"></a><span data-ttu-id="e75fc-127">Поиск рекомендаций Advisor</span><span class="sxs-lookup"><span data-stu-id="e75fc-127">Search for Advisor recommendations</span></span>

<span data-ttu-id="e75fc-128">Можно найти рекомендации для определенной подписки или группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e75fc-128">You can search for recommendations for a particular subscription or resource group.</span></span> <span data-ttu-id="e75fc-129">Можно также выполнять поиск рекомендаций по состоянию.</span><span class="sxs-lookup"><span data-stu-id="e75fc-129">You can also search for recommendations by status.</span></span>

1. <span data-ttu-id="e75fc-130">Войдите на [портал Azure](https://portal.azure.com) и откройте [Помощник по Azure](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="e75fc-130">Sign in to the [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="e75fc-131">Выполните поиск рекомендаций с помощью фильтра по подписке, группе ресурсов и состоянию рекомендации (**Активно** или **Отложена**).</span><span class="sxs-lookup"><span data-stu-id="e75fc-131">Search for recommendations by filtering for subscriptions, resource groups, and recommendation status (**Active** or **Snoozed**).</span></span>

3. <span data-ttu-id="e75fc-132">Чтобы получить список рекомендаций Помощника в соответствии с заданными фильтрами поиска, щелкните **Получить рекомендации**.</span><span class="sxs-lookup"><span data-stu-id="e75fc-132">To display a list of Advisor recommendations that are based on your search-filter criteria, click **Get recommendations**.</span></span>

  ![Критерии фильтра поиска в Помощнике](./media/advisor-get-started/advisor-search.png)

## <a name="snooze-or-dismiss-advisor-recommendations"></a><span data-ttu-id="e75fc-134">Отложить или закрыть рекомендации Помощника</span><span class="sxs-lookup"><span data-stu-id="e75fc-134">Snooze or dismiss Advisor recommendations</span></span>

1. <span data-ttu-id="e75fc-135">Войдите на [портал Azure](https://portal.azure.com) и откройте [Помощник по Azure](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="e75fc-135">Sign in to the [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="e75fc-136">Щелкните **Получить рекомендации**, а затем в списке выберите нужную рекомендацию.</span><span class="sxs-lookup"><span data-stu-id="e75fc-136">Click **Get recommendations**, and then, in the list of recommendations, click a recommendation.</span></span>

3. <span data-ttu-id="e75fc-137">В колонке **Рекомендация** щелкните **Отложить**.</span><span class="sxs-lookup"><span data-stu-id="e75fc-137">On the **Recommendation** blade, click **Snooze**.</span></span>  

   ![Пример действия из рекомендации Advisor](./media/advisor-get-started/advisor-snooze.png)

4. <span data-ttu-id="e75fc-139">Укажите период времени, на который откладывается рекомендация, или выберите значение **Никогда**, чтобы закрыть ее.</span><span class="sxs-lookup"><span data-stu-id="e75fc-139">Specify a snooze time period, or select **Never** to dismiss the recommendation.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e75fc-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e75fc-140">Next steps</span></span>

<span data-ttu-id="e75fc-141">Дополнительные сведения о Помощнике см. в таких разделах.</span><span class="sxs-lookup"><span data-stu-id="e75fc-141">To learn more about Advisor, see:</span></span>
* [<span data-ttu-id="e75fc-142">Общие сведения об Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="e75fc-142">Introduction to Azure Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="e75fc-143">Рекомендации Azure Advisor по высокой доступности</span><span class="sxs-lookup"><span data-stu-id="e75fc-143">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)
* [<span data-ttu-id="e75fc-144">Рекомендации Azure Advisor по безопасности</span><span class="sxs-lookup"><span data-stu-id="e75fc-144">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)
-  [<span data-ttu-id="e75fc-145">Рекомендации Azure Advisor по производительности</span><span class="sxs-lookup"><span data-stu-id="e75fc-145">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="e75fc-146">Рекомендации Azure Advisor по затратам</span><span class="sxs-lookup"><span data-stu-id="e75fc-146">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
