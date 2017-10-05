---
title: "Рекомендации Azure Advisor по производительности | Документация Майкрософт"
description: "Используйте Помощник для оптимизации производительности развернутых служб Azure."
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
ms.openlocfilehash: 5fb86c60b2d1f258dde5636ff8854b6f30f7f1c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="advisor-performance-recommendations"></a><span data-ttu-id="07dcf-103">Рекомендации Azure Advisor по производительности</span><span class="sxs-lookup"><span data-stu-id="07dcf-103">Advisor Performance recommendations</span></span>

<span data-ttu-id="07dcf-104">Рекомендации по производительности, предложенные Помощником по Azure, помогают улучшить работу, повысить производительность и увеличить скорость реагирования критически важных бизнес-приложений.</span><span class="sxs-lookup"><span data-stu-id="07dcf-104">Azure Advisor performance recommendations help improve the speed and responsiveness of your business-critical applications.</span></span> <span data-ttu-id="07dcf-105">Получить рекомендации Помощника по производительности можно на вкладке **Производительность** панели мониторинга Помощника.</span><span class="sxs-lookup"><span data-stu-id="07dcf-105">You can get performance recommendations from Advisor on the **Performance** tab of the Advisor dashboard.</span></span>

![Вкладка "Производительность" в Advisor](./media/advisor-performance-recommendations/advisor-performance-tab.png)

## <a name="improve-database-performance-with-sql-db-advisor"></a><span data-ttu-id="07dcf-107">Повышение производительности базы данных с помощью Помощника по базам данных SQL</span><span class="sxs-lookup"><span data-stu-id="07dcf-107">Improve database performance with SQL DB Advisor</span></span>

<span data-ttu-id="07dcf-108">Advisor предоставляет согласованное сводное представление с рекомендациями для всех ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="07dcf-108">Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources.</span></span> <span data-ttu-id="07dcf-109">Advisor интегрируется с Помощником по базам данных SQL, чтобы вы могли получить рекомендации по повышению производительности базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="07dcf-109">It integrates with SQL Database Advisor to bring you recommendations for improving the performance of your SQL Azure database.</span></span> <span data-ttu-id="07dcf-110">Помощник по базам данных SQL оценивает производительность ваших баз данных SQL, анализируя журнал использования.</span><span class="sxs-lookup"><span data-stu-id="07dcf-110">SQL Database Advisor assesses the performance of your SQL Azure databases by analyzing your usage history.</span></span> <span data-ttu-id="07dcf-111">После этого он предлагает рекомендации, наиболее подходящие для типовых нагрузок в вашей базе данных.</span><span class="sxs-lookup"><span data-stu-id="07dcf-111">It then offers recommendations that are best suited for running the database’s typical workload.</span></span> 

> [!NOTE]
> <span data-ttu-id="07dcf-112">Чтобы рекомендации сформировались, база данных должна постоянно использоваться на протяжении примерно одной недели.</span><span class="sxs-lookup"><span data-stu-id="07dcf-112">To get recommendations, a database must have about a week of usage, and within that week there must be some consistent activity.</span></span> <span data-ttu-id="07dcf-113">Помощник по базам данных SQL обеспечивает более эффективную оптимизацию при стабильном потоке запросов, чем на основе случайных всплесков активности.</span><span class="sxs-lookup"><span data-stu-id="07dcf-113">SQL Database Advisor can optimize more easily for consistent query patterns than for random bursts of activity.</span></span>

<span data-ttu-id="07dcf-114">Дополнительные сведения о Помощнике по базам данных SQL см. в разделе [Помощник по работе с базами данных SQL](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/).</span><span class="sxs-lookup"><span data-stu-id="07dcf-114">For more information about SQL Database Advisor, see [SQL Database Advisor](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/).</span></span>

![Рекомендации по базе данных SQL](./media/advisor-performance-recommendations/advisor-performance-sql.png)

## <a name="improve-redis-cache-performance-and-reliability"></a><span data-ttu-id="07dcf-116">Повышение надежности и производительности кэша Redis</span><span class="sxs-lookup"><span data-stu-id="07dcf-116">Improve Redis Cache performance and reliability</span></span>

<span data-ttu-id="07dcf-117">Помощник выявляет экземпляры кэша Redis, на производительность которых может отрицательно влиять использование большого объема памяти, нагрузка на сервер, пропускная способность сети или большое количество клиентских подключений.</span><span class="sxs-lookup"><span data-stu-id="07dcf-117">Advisor identifies Redis Cache instances where performance may be adversely affected by high memory usage, server load, network bandwidth, or a large number of client connections.</span></span> <span data-ttu-id="07dcf-118">Он также предоставляет практические рекомендации, позволяющие избежать возможных проблем.</span><span class="sxs-lookup"><span data-stu-id="07dcf-118">Advisor also provides best practices recommendations to help you avoid potential issues.</span></span> <span data-ttu-id="07dcf-119">Дополнительные сведения о рекомендациях по кэшу Redis см. в разделе [Помощник по кэшу Redis](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor).</span><span class="sxs-lookup"><span data-stu-id="07dcf-119">For more information about Redis Cache recommendations, see [Redis Cache Advisor](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor).</span></span>


## <a name="improve-app-service-performance-and-reliability"></a><span data-ttu-id="07dcf-120">Повышение надежности и производительности службы приложений</span><span class="sxs-lookup"><span data-stu-id="07dcf-120">Improve App Service performance and reliability</span></span>

<span data-ttu-id="07dcf-121">Azure Advisor объединяет практические рекомендации по улучшению работы службы приложений и обнаружению соответствующих возможностей платформы.</span><span class="sxs-lookup"><span data-stu-id="07dcf-121">Azure Advisor integrates best practices recommendations for improving your App Services experience and discovering relevant platform capabilities.</span></span> <span data-ttu-id="07dcf-122">Ниже приведены примеры рекомендаций по службам приложений:</span><span class="sxs-lookup"><span data-stu-id="07dcf-122">Examples of App Services recommendations are:</span></span>
* <span data-ttu-id="07dcf-123">обнаружение экземпляров, исчерпавших ресурсы памяти или ЦП во время выполнения приложений, и описание вариантов устранения;</span><span class="sxs-lookup"><span data-stu-id="07dcf-123">Detection of instances where memory or CPU resources are exhausted by app runtimes with mitigation options.</span></span>
* <span data-ttu-id="07dcf-124">обнаружение экземпляров, для которых совместное размещение ресурсов, например веб-приложений и баз данных, может повысить производительность и снизить стоимость.</span><span class="sxs-lookup"><span data-stu-id="07dcf-124">Detection of instances where collocating resources like web apps and databases can improve performance and lower cost.</span></span> 

<span data-ttu-id="07dcf-125">Дополнительные сведения о рекомендациях по службам приложений см. в разделе [Рекомендации по использованию службы приложений Azure](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/).</span><span class="sxs-lookup"><span data-stu-id="07dcf-125">For more information about App Services recommendations, see [Best Practices for Azure App Service](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/).</span></span>
<span data-ttu-id="07dcf-126">![Рекомендации по службам приложений](./media/advisor-performance-recommendations/advisor-performance-app-service.png)</span><span class="sxs-lookup"><span data-stu-id="07dcf-126">![App Services recommendations](./media/advisor-performance-recommendations/advisor-performance-app-service.png)</span></span>

## <a name="how-to-access-performance-recommendations-in-advisor"></a><span data-ttu-id="07dcf-127">Как получить доступ к рекомендации по производительности в Advisor</span><span class="sxs-lookup"><span data-stu-id="07dcf-127">How to access Performance recommendations in Advisor</span></span>

1. <span data-ttu-id="07dcf-128">Выполните вход на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="07dcf-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="07dcf-129">На панели слева щелкните **Больше служб**.</span><span class="sxs-lookup"><span data-stu-id="07dcf-129">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="07dcf-130">В области меню служб в разделе **Мониторинг и управление** щелкните **Помощник по Azure**.</span><span class="sxs-lookup"><span data-stu-id="07dcf-130">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="07dcf-131">Отображается панель мониторинга Помощника.</span><span class="sxs-lookup"><span data-stu-id="07dcf-131">The Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="07dcf-132">На панели мониторинга Помощника выберите вкладку **Производительность**.</span><span class="sxs-lookup"><span data-stu-id="07dcf-132">On the Advisor dashboard, click the **Performance** tab.</span></span>

5. <span data-ttu-id="07dcf-133">Выберите подписку, для которой вы хотите получать рекомендации, и щелкните **Получить рекомендации**.</span><span class="sxs-lookup"><span data-stu-id="07dcf-133">Select the subscription for which you want to receive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="07dcf-134">Для доступа к рекомендациям Помощника необходимо сначала *зарегистрировать* в нем свою подписку.</span><span class="sxs-lookup"><span data-stu-id="07dcf-134">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="07dcf-135">Подписка регистрируется, когда *владелец подписки* открывает панель мониторинга Помощника и нажимает кнопку **Получить рекомендации**.</span><span class="sxs-lookup"><span data-stu-id="07dcf-135">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="07dcf-136">Выполнить данную *операцию достаточно всего один раз*.</span><span class="sxs-lookup"><span data-stu-id="07dcf-136">This is a *one-time operation*.</span></span> <span data-ttu-id="07dcf-137">После регистрации подписки рекомендации Помощника могут просматривать *владельцы*, *участники* или *читатели* подписки, группы ресурсов или конкретного ресурса.</span><span class="sxs-lookup"><span data-stu-id="07dcf-137">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07dcf-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="07dcf-138">Next steps</span></span>

<span data-ttu-id="07dcf-139">Чтобы узнать больше о рекомендациях Помощника, ознакомьтесь с приведенными ниже материалами.</span><span class="sxs-lookup"><span data-stu-id="07dcf-139">To learn more about Advisor recommendations, see:</span></span>

* [<span data-ttu-id="07dcf-140">Общие сведения об Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="07dcf-140">Introduction to Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="07dcf-141">Приступая к работе с Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="07dcf-141">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="07dcf-142">Рекомендации Azure Advisor по затратам</span><span class="sxs-lookup"><span data-stu-id="07dcf-142">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="07dcf-143">Рекомендации Azure Advisor по высокой доступности</span><span class="sxs-lookup"><span data-stu-id="07dcf-143">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)
* [<span data-ttu-id="07dcf-144">Рекомендации Azure Advisor по безопасности</span><span class="sxs-lookup"><span data-stu-id="07dcf-144">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)

