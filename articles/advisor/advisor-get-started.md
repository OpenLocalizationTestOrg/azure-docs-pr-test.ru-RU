---
title: "aaaGet к работе с помощником по Azure | Документы Microsoft"
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
ms.openlocfilehash: 30fc8b8f3823f6f047e46cb9000189f3ccb3d514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-advisor"></a><span data-ttu-id="eda6b-103">Приступая к работе с Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="eda6b-103">Get started with Azure Advisor</span></span>

<span data-ttu-id="eda6b-104">Узнайте, как tooaccess ядра СУБД через hello портал Azure get рекомендации, реализовать рекомендации, поиска для рекомендаций и рекомендаций для обновления.</span><span class="sxs-lookup"><span data-stu-id="eda6b-104">Learn how tooaccess Advisor through hello Azure portal, get recommendations, implement recommendations, search for recommendations, and refresh recommendations.</span></span>

## <a name="get-advisor-recommendations"></a><span data-ttu-id="eda6b-105">Получение рекомендаций Advisor</span><span class="sxs-lookup"><span data-stu-id="eda6b-105">Get Advisor recommendations</span></span>

1. <span data-ttu-id="eda6b-106">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="eda6b-106">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="eda6b-107">Hello левой панели щелкните **дополнительные службы**.</span><span class="sxs-lookup"><span data-stu-id="eda6b-107">In hello left pane, click **More services**.</span></span>

3. <span data-ttu-id="eda6b-108">В hello службы панели меню в разделе **управление и мониторинг**, нажмите кнопку **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="eda6b-108">In hello service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="eda6b-109">отображается панель мониторинга Advisor Hello.</span><span class="sxs-lookup"><span data-stu-id="eda6b-109">hello Advisor dashboard is displayed.</span></span>

   ![Доступ к советнику по Azure с помощью портала Azure hello](./media/advisor-overview/advisor-azure-portal-menu.png) 

4. <span data-ttu-id="eda6b-111">На панели мониторинга Advisor hello выберите hello подписки, для которого требуется получить рекомендации tooreceive.</span><span class="sxs-lookup"><span data-stu-id="eda6b-111">On hello Advisor dashboard, select hello subscription for which you want tooreceive recommendations.</span></span>  
<span data-ttu-id="eda6b-112">панель мониторинга Advisor Hello отображает персонализированной рекомендации для выбранной подписки.</span><span class="sxs-lookup"><span data-stu-id="eda6b-112">hello Advisor dashboard displays personalized recommendations for a selected subscription.</span></span> 

5. <span data-ttu-id="eda6b-113">tooget рекомендации для определенной категории, выберите одну из вкладок hello: **высокий уровень доступности**, **безопасности**, **производительности**, или **стоимость**.</span><span class="sxs-lookup"><span data-stu-id="eda6b-113">tooget recommendations for a particular category, click one of hello tabs: **High Availability**, **Security**, **Performance**, or **Cost**.</span></span>
 
> [!NOTE]
> <span data-ttu-id="eda6b-114">tooaccess рекомендаций Advisor, необходимо сначала *зарегистрировать подписку* помощника по.</span><span class="sxs-lookup"><span data-stu-id="eda6b-114">tooaccess Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="eda6b-115">Подписка зарегистрирована при *владелец подписки* запускает hello hello панели мониторинга и щелкает пункт помощник по настройке ядра **получить рекомендации** кнопки.</span><span class="sxs-lookup"><span data-stu-id="eda6b-115">A subscription is registered when a *subscription Owner* launches hello Advisor dashboard and clicks hello **Get recommendations** button.</span></span> <span data-ttu-id="eda6b-116">Выполнить данную *операцию достаточно всего один раз*.</span><span class="sxs-lookup"><span data-stu-id="eda6b-116">This is a *one-time operation*.</span></span> <span data-ttu-id="eda6b-117">После регистрации подписки hello, можно использовать получать рекомендации помощника по как *владельца*, *участника*, или *чтения* для подписки, группу ресурсов или конкретный ресурс.</span><span class="sxs-lookup"><span data-stu-id="eda6b-117">After hello subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

  ![Панель мониторинга Azure Advisor](./media/advisor-overview/advisor-all-tab.png)

## <a name="get-advisor-recommendation-details-and-implement-a-solution"></a><span data-ttu-id="eda6b-119">Получение сведений о рекомендации Помощника и реализация решения</span><span class="sxs-lookup"><span data-stu-id="eda6b-119">Get Advisor recommendation details, and implement a solution</span></span>

<span data-ttu-id="eda6b-120">Hello **рекомендация** колонки в помощнике по имеются дополнительные сведения о рекомендация hello.</span><span class="sxs-lookup"><span data-stu-id="eda6b-120">hello **Recommendation** blade in Advisor offers additional information about hello recommendation.</span></span> 

1. <span data-ttu-id="eda6b-121">Войдите в toohello [портал Azure](https://portal.azure.com)и запустите [Azure Advisor](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="eda6b-121">Sign in toohello [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="eda6b-122">На hello **получать рекомендации помощника по** панели мониторинга, щелкните **получить рекомендации**.</span><span class="sxs-lookup"><span data-stu-id="eda6b-122">On hello **Advisor recommendations** dashboard, click **Get recommendations**.</span></span>

3. <span data-ttu-id="eda6b-123">В списке hello рекомендаций выберите рекомендации, которые должны tooreview подробно.</span><span class="sxs-lookup"><span data-stu-id="eda6b-123">In hello list of recommendations, click a recommendation that you want tooreview in detail.</span></span>  
<span data-ttu-id="eda6b-124">Hello **рекомендация** колонке отображается.</span><span class="sxs-lookup"><span data-stu-id="eda6b-124">hello **Recommendation** blade is displayed.</span></span>

4. <span data-ttu-id="eda6b-125">На hello **рекомендации** колонки, просмотрите сведения о действиях, можно выполнять tooresolve потенциальную проблему, или воспользоваться преимуществами возможности снизить издержки.</span><span class="sxs-lookup"><span data-stu-id="eda6b-125">On hello **Recommendations** blade, review information about actions that you can perform tooresolve a potential issue, or take advantage of a cost-saving opportunity.</span></span> 
  
  ![Рекомендации помощника по колонке Hello](./media/advisor-overview/advisor-recommendation-action-example.png)

## <a name="search-for-advisor-recommendations"></a><span data-ttu-id="eda6b-127">Поиск рекомендаций Advisor</span><span class="sxs-lookup"><span data-stu-id="eda6b-127">Search for Advisor recommendations</span></span>

<span data-ttu-id="eda6b-128">Можно найти рекомендации для определенной подписки или группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="eda6b-128">You can search for recommendations for a particular subscription or resource group.</span></span> <span data-ttu-id="eda6b-129">Можно также выполнять поиск рекомендаций по состоянию.</span><span class="sxs-lookup"><span data-stu-id="eda6b-129">You can also search for recommendations by status.</span></span>

1. <span data-ttu-id="eda6b-130">Войдите в toohello [портал Azure](https://portal.azure.com)и запустите [Azure Advisor](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="eda6b-130">Sign in toohello [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="eda6b-131">Выполните поиск рекомендаций с помощью фильтра по подписке, группе ресурсов и состоянию рекомендации (**Активно** или **Отложена**).</span><span class="sxs-lookup"><span data-stu-id="eda6b-131">Search for recommendations by filtering for subscriptions, resource groups, and recommendation status (**Active** or **Snoozed**).</span></span>

3. <span data-ttu-id="eda6b-132">Щелкните критерии фильтра поиска toodisplay список рекомендаций помощник по настройке ядра, основанных на **получить рекомендации**.</span><span class="sxs-lookup"><span data-stu-id="eda6b-132">toodisplay a list of Advisor recommendations that are based on your search-filter criteria, click **Get recommendations**.</span></span>

  ![Критерии фильтра поиска в Помощнике](./media/advisor-get-started/advisor-search.png)

## <a name="snooze-or-dismiss-advisor-recommendations"></a><span data-ttu-id="eda6b-134">Отложить или закрыть рекомендации Помощника</span><span class="sxs-lookup"><span data-stu-id="eda6b-134">Snooze or dismiss Advisor recommendations</span></span>

1. <span data-ttu-id="eda6b-135">Войдите в toohello [портал Azure](https://portal.azure.com)и запустите [Azure Advisor](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="eda6b-135">Sign in toohello [Azure portal](https://portal.azure.com), and then start [Azure Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2. <span data-ttu-id="eda6b-136">Нажмите кнопку **получить рекомендации**и выберите в hello список рекомендаций, рекомендации.</span><span class="sxs-lookup"><span data-stu-id="eda6b-136">Click **Get recommendations**, and then, in hello list of recommendations, click a recommendation.</span></span>

3. <span data-ttu-id="eda6b-137">На hello **рекомендация** колонка, щелкните **отложить**.</span><span class="sxs-lookup"><span data-stu-id="eda6b-137">On hello **Recommendation** blade, click **Snooze**.</span></span>  

   ![Пример действия из рекомендации Advisor](./media/advisor-get-started/advisor-snooze.png)

4. <span data-ttu-id="eda6b-139">Укажите отложить период времени, или установите **никогда** toodismiss hello рекомендации.</span><span class="sxs-lookup"><span data-stu-id="eda6b-139">Specify a snooze time period, or select **Never** toodismiss hello recommendation.</span></span>


## <a name="next-steps"></a><span data-ttu-id="eda6b-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="eda6b-140">Next steps</span></span>

<span data-ttu-id="eda6b-141">в разделе toolearn Дополнительные сведения о помощнике по:</span><span class="sxs-lookup"><span data-stu-id="eda6b-141">toolearn more about Advisor, see:</span></span>
* [<span data-ttu-id="eda6b-142">Введение tooAzure Advisor</span><span class="sxs-lookup"><span data-stu-id="eda6b-142">Introduction tooAzure Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="eda6b-143">Рекомендации Azure Advisor по высокой доступности</span><span class="sxs-lookup"><span data-stu-id="eda6b-143">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)
* [<span data-ttu-id="eda6b-144">Рекомендации Azure Advisor по безопасности</span><span class="sxs-lookup"><span data-stu-id="eda6b-144">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)
-  [<span data-ttu-id="eda6b-145">Рекомендации Azure Advisor по производительности</span><span class="sxs-lookup"><span data-stu-id="eda6b-145">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="eda6b-146">Рекомендации Azure Advisor по затратам</span><span class="sxs-lookup"><span data-stu-id="eda6b-146">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
