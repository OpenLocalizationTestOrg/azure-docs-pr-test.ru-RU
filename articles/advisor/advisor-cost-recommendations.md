---
title: "рекомендаций помощник по стоимости aaaAzure | Документы Microsoft"
description: "Используйте помощник по настройке ядра Azure toooptimize hello затраты развертываний Azure."
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
ms.openlocfilehash: 50f70c33a17f550c8753795435cdfddd51e409f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-cost-recommendations"></a><span data-ttu-id="083f1-103">Рекомендации Azure Advisor по затратам</span><span class="sxs-lookup"><span data-stu-id="083f1-103">Advisor Cost recommendations</span></span>

<span data-ttu-id="083f1-104">Advisor помогает оптимизировать и уменьшить общие расходы на Azure, выявляя простаивающие и недостаточно нагруженные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="083f1-104">Advisor helps you optimize and reduce your overall Azure spend by identifying idle and underutilized resources.</span></span> <span data-ttu-id="083f1-105">Может получить стоимости рекомендаций из hello **стоимость** на hello мониторинга ядра СУБД.</span><span class="sxs-lookup"><span data-stu-id="083f1-105">You can get cost recommendations from hello **Cost** tab on hello Advisor dashboard.</span></span>

![Вкладка "Стоимость" в Помощнике](./media/advisor-cost-recommendations/advisor-cost-tab2.png)

## <a name="optimize-virtual-machine-spend-by-resizing-underutilized-instances"></a><span data-ttu-id="083f1-107">Оптимизация затрат на виртуальные машины путем изменения размеров недогруженных экземпляров</span><span class="sxs-lookup"><span data-stu-id="083f1-107">Optimize virtual machine spend by resizing underutilized instances</span></span> 
<span data-ttu-id="083f1-108">Хотя в некоторых сценариях приложение может вызвать низким использованием намеренно, часто поможет сэкономить деньги за счет управления hello размер и количество виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="083f1-108">Although certain application scenarios can result in low utilization by design, you can often save money by managing hello size and number of your virtual machines.</span></span> <span data-ttu-id="083f1-109">Помощник отслеживает использование виртуальных машин на протяжении 14 дней, а затем определяет недостаточно нагруженные виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="083f1-109">Advisor monitors your virtual machine usage for 14 days and then identifies low-utilization virtual machines.</span></span> <span data-ttu-id="083f1-110">Виртуальные машины, у которых использование ресурсов ЦП составляет не больше 5 % и использование ресурсов сети составляет не больше 7 МБ на протяжении 4 или более дней, будут считаться недостаточно нагруженными.</span><span class="sxs-lookup"><span data-stu-id="083f1-110">Virtual machines whose CPU utilization is 5 percent or less and network usage is 7 MB or less for four or more days are considered low-utilization virtual machines.</span></span>

<span data-ttu-id="083f1-111">Помощник по настройке ядра показано hello расчетные затраты на продолжение toorun виртуального компьютера, чтобы вы могли выбрать tooshut его вниз или изменить его размер.</span><span class="sxs-lookup"><span data-stu-id="083f1-111">Advisor shows you hello estimated cost of continuing toorun your virtual machine, so that you can choose tooshut it down or resize it.</span></span>  

![Рекомендации Advisor по затратам на изменение размеров виртуальных машин](./media/advisor-cost-recommendations/advisor-cost-resizevms.png)

## <a name="use-a-cost-effective-solution-toomanage-performance-goals-of-multiple-sql-databases"></a><span data-ttu-id="083f1-113">Использовать целевые показатели производительности экономичное решение toomanage нескольких баз данных SQL</span><span class="sxs-lookup"><span data-stu-id="083f1-113">Use a cost effective solution toomanage performance goals of multiple SQL databases</span></span>
<span data-ttu-id="083f1-114">Advisor определяет экземпляры SQL Server, создание пулов эластичных баз данных для которых дает преимущества.</span><span class="sxs-lookup"><span data-stu-id="083f1-114">Advisor identifies SQL server instances that can benefit from creating elastic database pools.</span></span> <span data-ttu-id="083f1-115">Пулы эластичных баз данных предоставляют toomanage простой и экономичное решение цели производительности hello нескольких баз данных, имеющих различные статистические характеристики интенсивности использования.</span><span class="sxs-lookup"><span data-stu-id="083f1-115">Elastic database pools provide a simple, cost-effective solution toomanage hello performance goals of multiple databases that have varying usage patterns.</span></span> <span data-ttu-id="083f1-116">Дополнительные сведения о пулах эластичных баз данных Azure см. в статье [Что такое пул эластичных БД Azure?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).</span><span class="sxs-lookup"><span data-stu-id="083f1-116">For more information about Azure elastic pools, see [What is an Azure Elastic pool?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).</span></span>

![Рекомендации Advisor по затратам на пулы эластичных баз данных](./media/advisor-cost-recommendations/advisor-cost-elasticdbpools.png)

## <a name="how-tooaccess-cost-recommendations-in-azure-advisor"></a><span data-ttu-id="083f1-118">Как tooaccess стоимости рекомендации в помощнике по Azure</span><span class="sxs-lookup"><span data-stu-id="083f1-118">How tooaccess cost recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="083f1-119">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="083f1-119">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="083f1-120">Hello левой панели щелкните **дополнительные службы**.</span><span class="sxs-lookup"><span data-stu-id="083f1-120">In hello left pane, click **More services**.</span></span>

3. <span data-ttu-id="083f1-121">В hello службы панели меню в разделе **управление и мониторинг**, нажмите кнопку **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="083f1-121">In hello service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="083f1-122">отображается панель мониторинга Advisor Hello.</span><span class="sxs-lookup"><span data-stu-id="083f1-122">hello Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="083f1-123">На панели мониторинга Advisor hello, нажмите кнопку hello **стоимость** вкладки.</span><span class="sxs-lookup"><span data-stu-id="083f1-123">On hello Advisor dashboard, click hello **Cost** tab.</span></span>

5. <span data-ttu-id="083f1-124">Выберите подписку hello, для которого требуется tooreceive рекомендации и нажмите кнопку **получить рекомендации**.</span><span class="sxs-lookup"><span data-stu-id="083f1-124">Select hello subscription for which you want tooreceive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="083f1-125">tooaccess рекомендаций Advisor, необходимо сначала *зарегистрировать подписку* помощника по.</span><span class="sxs-lookup"><span data-stu-id="083f1-125">tooaccess Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="083f1-126">Подписка зарегистрирована при *владелец подписки* запускает hello hello панели мониторинга и щелкает пункт помощник по настройке ядра **получить рекомендации** кнопки.</span><span class="sxs-lookup"><span data-stu-id="083f1-126">A subscription is registered when a *subscription Owner* launches hello Advisor dashboard and clicks hello **Get recommendations** button.</span></span> <span data-ttu-id="083f1-127">Выполнить данную *операцию достаточно всего один раз*.</span><span class="sxs-lookup"><span data-stu-id="083f1-127">This is a *one-time operation*.</span></span> <span data-ttu-id="083f1-128">После регистрации подписки hello, можно использовать получать рекомендации помощника по как *владельца*, *участника*, или *чтения* для подписки, группу ресурсов или конкретный ресурс.</span><span class="sxs-lookup"><span data-stu-id="083f1-128">After hello subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="083f1-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="083f1-129">Next steps</span></span>

<span data-ttu-id="083f1-130">в разделе toolearn Дополнительные сведения о рекомендаций помощник по настройке ядра:</span><span class="sxs-lookup"><span data-stu-id="083f1-130">toolearn more about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="083f1-131">Введение tooAdvisor</span><span class="sxs-lookup"><span data-stu-id="083f1-131">Introduction tooAdvisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="083f1-132">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="083f1-132">Get Started</span></span>](advisor-get-started.md)
* [<span data-ttu-id="083f1-133">Рекомендации Azure Advisor по производительности</span><span class="sxs-lookup"><span data-stu-id="083f1-133">Advisor Performance recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="083f1-134">Рекомендации Azure Advisor по высокой доступности</span><span class="sxs-lookup"><span data-stu-id="083f1-134">Advisor High Availability recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="083f1-135">Рекомендации Azure Advisor по безопасности</span><span class="sxs-lookup"><span data-stu-id="083f1-135">Advisor Security recommendations</span></span>](advisor-cost-recommendations.md)
