---
title: "рекомендации по повышению производительности Advisor aaaAzure | Документы Microsoft"
description: "Используйте Советник по производительности hello toooptimize развертываний Azure."
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
ms.openlocfilehash: eb3d928664717f6f322132ac740f42015f56b76e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-performance-recommendations"></a><span data-ttu-id="ec8fd-103">Рекомендации Azure Advisor по производительности</span><span class="sxs-lookup"><span data-stu-id="ec8fd-103">Advisor Performance recommendations</span></span>

<span data-ttu-id="ec8fd-104">Рекомендации по повышению производительности Azure помощник по настройке ядра помочь повысить скорость hello и скорость реагирования важнейших бизнес-приложений.</span><span class="sxs-lookup"><span data-stu-id="ec8fd-104">Azure Advisor performance recommendations help improve hello speed and responsiveness of your business-critical applications.</span></span> <span data-ttu-id="ec8fd-105">Рекомендации по повышению производительности можно получить из ядра СУБД на hello **производительности** hello мониторинга ядра СУБД.</span><span class="sxs-lookup"><span data-stu-id="ec8fd-105">You can get performance recommendations from Advisor on hello **Performance** tab of hello Advisor dashboard.</span></span>

![Вкладка "Производительность" в Advisor](./media/advisor-performance-recommendations/advisor-performance-tab.png)

## <a name="improve-database-performance-with-sql-db-advisor"></a><span data-ttu-id="ec8fd-107">Повышение производительности базы данных с помощью Помощника по базам данных SQL</span><span class="sxs-lookup"><span data-stu-id="ec8fd-107">Improve database performance with SQL DB Advisor</span></span>

<span data-ttu-id="ec8fd-108">Advisor предоставляет согласованное сводное представление с рекомендациями для всех ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="ec8fd-108">Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources.</span></span> <span data-ttu-id="ec8fd-109">Она интегрируется с toobring помощник по настройке ядра базы данных SQL вы рекомендации по улучшению производительности hello базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="ec8fd-109">It integrates with SQL Database Advisor toobring you recommendations for improving hello performance of your SQL Azure database.</span></span> <span data-ttu-id="ec8fd-110">Помощник по настройке ядра базы данных SQL оценивает hello производительности баз данных SQL Azure путем анализа вашего журнала использования.</span><span class="sxs-lookup"><span data-stu-id="ec8fd-110">SQL Database Advisor assesses hello performance of your SQL Azure databases by analyzing your usage history.</span></span> <span data-ttu-id="ec8fd-111">Затем оно предлагает рекомендации, которые лучше всего подходят для выполнения типичных hello базы данных рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="ec8fd-111">It then offers recommendations that are best suited for running hello database’s typical workload.</span></span> 

> [!NOTE]
> <span data-ttu-id="ec8fd-112">рекомендации tooget базы данных должен иметь примерно одну неделю, использования и в течение этой недели должен быть некоторые согласованные действия.</span><span class="sxs-lookup"><span data-stu-id="ec8fd-112">tooget recommendations, a database must have about a week of usage, and within that week there must be some consistent activity.</span></span> <span data-ttu-id="ec8fd-113">Помощник по базам данных SQL обеспечивает более эффективную оптимизацию при стабильном потоке запросов, чем на основе случайных всплесков активности.</span><span class="sxs-lookup"><span data-stu-id="ec8fd-113">SQL Database Advisor can optimize more easily for consistent query patterns than for random bursts of activity.</span></span>

<span data-ttu-id="ec8fd-114">Дополнительные сведения о Помощнике по базам данных SQL см. в разделе [Помощник по работе с базами данных SQL](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/).</span><span class="sxs-lookup"><span data-stu-id="ec8fd-114">For more information about SQL Database Advisor, see [SQL Database Advisor](https://azure.microsoft.com/en-us/documentation/articles/sql-database-advisor/).</span></span>

![Рекомендации по базе данных SQL](./media/advisor-performance-recommendations/advisor-performance-sql.png)

## <a name="improve-redis-cache-performance-and-reliability"></a><span data-ttu-id="ec8fd-116">Повышение надежности и производительности кэша Redis</span><span class="sxs-lookup"><span data-stu-id="ec8fd-116">Improve Redis Cache performance and reliability</span></span>

<span data-ttu-id="ec8fd-117">Помощник выявляет экземпляры кэша Redis, на производительность которых может отрицательно влиять использование большого объема памяти, нагрузка на сервер, пропускная способность сети или большое количество клиентских подключений.</span><span class="sxs-lookup"><span data-stu-id="ec8fd-117">Advisor identifies Redis Cache instances where performance may be adversely affected by high memory usage, server load, network bandwidth, or a large number of client connections.</span></span> <span data-ttu-id="ec8fd-118">Advisor также дает лучшие методики рекомендации toohelp избежать потенциальных проблем.</span><span class="sxs-lookup"><span data-stu-id="ec8fd-118">Advisor also provides best practices recommendations toohelp you avoid potential issues.</span></span> <span data-ttu-id="ec8fd-119">Дополнительные сведения о рекомендациях по кэшу Redis см. в разделе [Помощник по кэшу Redis](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor).</span><span class="sxs-lookup"><span data-stu-id="ec8fd-119">For more information about Redis Cache recommendations, see [Redis Cache Advisor](https://azure.microsoft.com/en-us/documentation/articles/cache-configure/#redis-cache-advisor).</span></span>


## <a name="improve-app-service-performance-and-reliability"></a><span data-ttu-id="ec8fd-120">Повышение надежности и производительности службы приложений</span><span class="sxs-lookup"><span data-stu-id="ec8fd-120">Improve App Service performance and reliability</span></span>

<span data-ttu-id="ec8fd-121">Azure Advisor объединяет практические рекомендации по улучшению работы службы приложений и обнаружению соответствующих возможностей платформы.</span><span class="sxs-lookup"><span data-stu-id="ec8fd-121">Azure Advisor integrates best practices recommendations for improving your App Services experience and discovering relevant platform capabilities.</span></span> <span data-ttu-id="ec8fd-122">Ниже приведены примеры рекомендаций по службам приложений:</span><span class="sxs-lookup"><span data-stu-id="ec8fd-122">Examples of App Services recommendations are:</span></span>
* <span data-ttu-id="ec8fd-123">обнаружение экземпляров, исчерпавших ресурсы памяти или ЦП во время выполнения приложений, и описание вариантов устранения;</span><span class="sxs-lookup"><span data-stu-id="ec8fd-123">Detection of instances where memory or CPU resources are exhausted by app runtimes with mitigation options.</span></span>
* <span data-ttu-id="ec8fd-124">обнаружение экземпляров, для которых совместное размещение ресурсов, например веб-приложений и баз данных, может повысить производительность и снизить стоимость.</span><span class="sxs-lookup"><span data-stu-id="ec8fd-124">Detection of instances where collocating resources like web apps and databases can improve performance and lower cost.</span></span> 

<span data-ttu-id="ec8fd-125">Дополнительные сведения о рекомендациях по службам приложений см. в разделе [Рекомендации по использованию службы приложений Azure](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/).</span><span class="sxs-lookup"><span data-stu-id="ec8fd-125">For more information about App Services recommendations, see [Best Practices for Azure App Service](https://azure.microsoft.com/en-us/documentation/articles/app-service-best-practices/).</span></span>
<span data-ttu-id="ec8fd-126">![Рекомендации по службам приложений](./media/advisor-performance-recommendations/advisor-performance-app-service.png)</span><span class="sxs-lookup"><span data-stu-id="ec8fd-126">![App Services recommendations](./media/advisor-performance-recommendations/advisor-performance-app-service.png)</span></span>

## <a name="how-tooaccess-performance-recommendations-in-advisor"></a><span data-ttu-id="ec8fd-127">Как tooaccess рекомендации по повышению производительности в помощнике настройки ядра</span><span class="sxs-lookup"><span data-stu-id="ec8fd-127">How tooaccess Performance recommendations in Advisor</span></span>

1. <span data-ttu-id="ec8fd-128">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ec8fd-128">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="ec8fd-129">Hello левой панели щелкните **дополнительные службы**.</span><span class="sxs-lookup"><span data-stu-id="ec8fd-129">In hello left pane, click **More services**.</span></span>

3. <span data-ttu-id="ec8fd-130">В hello службы панели меню в разделе **управление и мониторинг**, нажмите кнопку **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="ec8fd-130">In hello service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="ec8fd-131">отображается панель мониторинга Advisor Hello.</span><span class="sxs-lookup"><span data-stu-id="ec8fd-131">hello Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="ec8fd-132">На панели мониторинга Advisor hello, нажмите кнопку hello **производительности** вкладки.</span><span class="sxs-lookup"><span data-stu-id="ec8fd-132">On hello Advisor dashboard, click hello **Performance** tab.</span></span>

5. <span data-ttu-id="ec8fd-133">Выберите подписку hello, для которого требуется tooreceive рекомендации и нажмите кнопку **получить рекомендации**.</span><span class="sxs-lookup"><span data-stu-id="ec8fd-133">Select hello subscription for which you want tooreceive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="ec8fd-134">tooaccess рекомендаций Advisor, необходимо сначала *зарегистрировать подписку* помощника по.</span><span class="sxs-lookup"><span data-stu-id="ec8fd-134">tooaccess Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="ec8fd-135">Подписка зарегистрирована при *владелец подписки* запускает hello hello панели мониторинга и щелкает пункт помощник по настройке ядра **получить рекомендации** кнопки.</span><span class="sxs-lookup"><span data-stu-id="ec8fd-135">A subscription is registered when a *subscription Owner* launches hello Advisor dashboard and clicks hello **Get recommendations** button.</span></span> <span data-ttu-id="ec8fd-136">Выполнить данную *операцию достаточно всего один раз*.</span><span class="sxs-lookup"><span data-stu-id="ec8fd-136">This is a *one-time operation*.</span></span> <span data-ttu-id="ec8fd-137">После регистрации подписки hello, можно использовать получать рекомендации помощника по как *владельца*, *участника*, или *чтения* для подписки, группу ресурсов или конкретный ресурс.</span><span class="sxs-lookup"><span data-stu-id="ec8fd-137">After hello subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec8fd-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ec8fd-138">Next steps</span></span>

<span data-ttu-id="ec8fd-139">в разделе toolearn Дополнительные сведения о рекомендаций помощник по настройке ядра:</span><span class="sxs-lookup"><span data-stu-id="ec8fd-139">toolearn more about Advisor recommendations, see:</span></span>

* [<span data-ttu-id="ec8fd-140">Введение tooAdvisor</span><span class="sxs-lookup"><span data-stu-id="ec8fd-140">Introduction tooAdvisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="ec8fd-141">Приступая к работе с Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="ec8fd-141">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="ec8fd-142">Рекомендации Azure Advisor по затратам</span><span class="sxs-lookup"><span data-stu-id="ec8fd-142">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="ec8fd-143">Рекомендации Azure Advisor по высокой доступности</span><span class="sxs-lookup"><span data-stu-id="ec8fd-143">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)
* [<span data-ttu-id="ec8fd-144">Рекомендации Azure Advisor по безопасности</span><span class="sxs-lookup"><span data-stu-id="ec8fd-144">Advisor Security recommendations</span></span>](advisor-security-recommendations.md)

