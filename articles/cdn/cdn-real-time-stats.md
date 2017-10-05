---
title: "Статистика в режиме реального времени в Azure CDN | Документация Майкрософт"
description: "Статистика в реальном времени предоставляет актуальные данные о производительности сети Azure CDN при доставке содержимого клиентам."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: c7989340-1172-4315-acbb-186ba34dd52a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: e9b9522de6b2c54dc794b00100ffe358296ecfdd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="real-time-stats-in-microsoft-azure-cdn"></a><span data-ttu-id="c68ad-103">Статистика в реальном времени в сети CDN Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="c68ad-103">Real-time stats in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="c68ad-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="c68ad-104">Overview</span></span>
<span data-ttu-id="c68ad-105">В этом документе содержатся сведения о статистике в реальном времени в сети CDN Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="c68ad-105">This document explains real-time stats in Microsoft Azure CDN.</span></span>  <span data-ttu-id="c68ad-106">Эта функция предоставляет данные в реальном времени, например о пропускной способности, состоянии кэша и числе одновременных подключений к профилю сети CDN, при доставке содержимого клиентам.</span><span class="sxs-lookup"><span data-stu-id="c68ad-106">This functionality provides real-time data, such as bandwidth, cache statuses, and concurrent connections to your CDN profile when delivering content to your clients.</span></span> <span data-ttu-id="c68ad-107">Благодаря этому обеспечивается постоянный мониторинг работоспособности службы, в том числе событий запуска.</span><span class="sxs-lookup"><span data-stu-id="c68ad-107">This enables continuous monitoring of the health of your service at any time, including go-live events.</span></span>

<span data-ttu-id="c68ad-108">Доступны следующие диаграммы:</span><span class="sxs-lookup"><span data-stu-id="c68ad-108">The following graphs are available:</span></span>

* [<span data-ttu-id="c68ad-109">Пропускная способность</span><span class="sxs-lookup"><span data-stu-id="c68ad-109">Bandwidth</span></span>](#bandwidth)
* [<span data-ttu-id="c68ad-110">Коды состояний</span><span class="sxs-lookup"><span data-stu-id="c68ad-110">Status Codes</span></span>](#status-codes)
* [<span data-ttu-id="c68ad-111">Состояния кэша</span><span class="sxs-lookup"><span data-stu-id="c68ad-111">Cache Statuses</span></span>](#cache-statuses)
* [<span data-ttu-id="c68ad-112">Подключения</span><span class="sxs-lookup"><span data-stu-id="c68ad-112">Connections</span></span>](#connections)

## <a name="accessing-real-time-stats"></a><span data-ttu-id="c68ad-113">Доступ к статистике в реальном времени</span><span class="sxs-lookup"><span data-stu-id="c68ad-113">Accessing real-time stats</span></span>
1. <span data-ttu-id="c68ad-114">На [портале Azure](https://portal.azure.com)перейдите к профилю CDN.</span><span class="sxs-lookup"><span data-stu-id="c68ad-114">In the [Azure Portal](https://portal.azure.com), browse to your CDN profile.</span></span>
   
    ![Колонка профиля сети CDN](./media/cdn-real-time-stats/cdn-profile-blade.png)
2. <span data-ttu-id="c68ad-116">В колонке профиля сети CDN нажмите кнопку **Управление** .</span><span class="sxs-lookup"><span data-stu-id="c68ad-116">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![Кнопка управления в колонке профиля CDN](./media/cdn-real-time-stats/cdn-manage-btn.png)
   
    <span data-ttu-id="c68ad-118">Откроется портал управления CDN.</span><span class="sxs-lookup"><span data-stu-id="c68ad-118">The CDN management portal opens.</span></span>
3. <span data-ttu-id="c68ad-119">Наведите указатель на вкладку **Аналитика**, а затем на всплывающее окно **Real-Time Stats** (Статистика в реальном времени).</span><span class="sxs-lookup"><span data-stu-id="c68ad-119">Hover over the **Analytics** tab, then hover over the **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="c68ad-120">Щелкните **Большой HTTP-объект**.</span><span class="sxs-lookup"><span data-stu-id="c68ad-120">Click on **HTTP Large Object**.</span></span>
   
    ![Портал управления CDN](./media/cdn-real-time-stats/cdn-premium-portal.png)
   
    <span data-ttu-id="c68ad-122">Отобразятся диаграммы статистических данных в реальном времени.</span><span class="sxs-lookup"><span data-stu-id="c68ad-122">The real-time stats graphs are displayed.</span></span>

<span data-ttu-id="c68ad-123">На каждой диаграмме отображается статистика в реальном времени за определенный период. Они запускаются при загрузке страницы</span><span class="sxs-lookup"><span data-stu-id="c68ad-123">Each of the graphs displays real-time statistics for the selected time span, starting when the page loads.</span></span>  <span data-ttu-id="c68ad-124">Они запускаются при загрузке страницы и автоматически обновляются каждые несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="c68ad-124">The graphs update automatically every few seconds.</span></span>  <span data-ttu-id="c68ad-125">Кнопка **Refresh Graph** (Обновить диаграмму), если она присутствует, позволяет очистить данные на диаграмме, после чего отобразятся только выбранные данные.</span><span class="sxs-lookup"><span data-stu-id="c68ad-125">The **Refresh Graph** button, if present, will clear the graph, after which it will only display the selected data.</span></span>

## <a name="bandwidth"></a><span data-ttu-id="c68ad-126">Пропускная способность</span><span class="sxs-lookup"><span data-stu-id="c68ad-126">Bandwidth</span></span>
![Диаграмма "Пропускная способность"](./media/cdn-real-time-stats/cdn-bandwidth.png)

<span data-ttu-id="c68ad-128">На диаграмме **Пропускная способность** отображается объем пропускной способности, использовавшийся для текущей платформы за выбранный период времени.</span><span class="sxs-lookup"><span data-stu-id="c68ad-128">The **Bandwidth** graph displays the amount of bandwidth used for the current platform over the selected time span.</span></span> <span data-ttu-id="c68ad-129">На затененной части диаграммы показано использование пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="c68ad-129">The shaded portion of the graph indicates bandwidth usage.</span></span> <span data-ttu-id="c68ad-130">Точный объем пропускной способности, используемой в данный момент, отображается непосредственно под линейной диаграммой.</span><span class="sxs-lookup"><span data-stu-id="c68ad-130">The exact amount of bandwidth currently being used is displayed directly below the line graph.</span></span>

## <a name="status-codes"></a><span data-ttu-id="c68ad-131">Коды состояний</span><span class="sxs-lookup"><span data-stu-id="c68ad-131">Status Codes</span></span>
![Диаграмма "Код состояния"](./media/cdn-real-time-stats/cdn-status-codes.png)

<span data-ttu-id="c68ad-133">На диаграмме **Коды состояний** показана частота возникновения определенных кодов HTTP-ответов за выбранный период времени.</span><span class="sxs-lookup"><span data-stu-id="c68ad-133">The **Status Codes** graph indicates how often certain HTTP response codes are occurring over the selected time span.</span></span>

> [!TIP]
> <span data-ttu-id="c68ad-134">Описание каждого параметра кода состояния HTTP см. в разделе [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx) (Коды состояний HTTP в сети Azure CDN).</span><span class="sxs-lookup"><span data-stu-id="c68ad-134">For a description of each HTTP status code option, see [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx).</span></span>
> 
> 

<span data-ttu-id="c68ad-135">Список кодов состояний HTTP находится непосредственно над диаграммой.</span><span class="sxs-lookup"><span data-stu-id="c68ad-135">A list of HTTP status codes is displayed directly above the graph.</span></span> <span data-ttu-id="c68ad-136">В списке приводится каждый код состояния, который может быть включен в линейную диаграмму, и текущее количество вхождений в секунду этого кода состояния.</span><span class="sxs-lookup"><span data-stu-id="c68ad-136">This list indicates each status code that can be included in the line graph and the current number of occurrences per second for that status code.</span></span> <span data-ttu-id="c68ad-137">По умолчанию отображается строка для каждого кода состояния в диаграмме.</span><span class="sxs-lookup"><span data-stu-id="c68ad-137">By default, a line is displayed for each of these status codes in the graph.</span></span> <span data-ttu-id="c68ad-138">Однако можно отслеживать только те коды состояний, которые имеют особое значение для конфигурации сети CDN.</span><span class="sxs-lookup"><span data-stu-id="c68ad-138">However, you can choose to only monitor the status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="c68ad-139">Для этого проверьте требуемые коды состояний и очистите все другие параметры, а затем нажмите кнопку **Refresh Graph**(Обновить диаграмму).</span><span class="sxs-lookup"><span data-stu-id="c68ad-139">To do this, check the desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="c68ad-140">Можно временно скрыть данные журнала для определенного кода состояния.</span><span class="sxs-lookup"><span data-stu-id="c68ad-140">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="c68ad-141">В условных обозначениях непосредственно под диаграммой щелкните код состояния, который нужно скрыть.</span><span class="sxs-lookup"><span data-stu-id="c68ad-141">From the legend directly below the graph, click the status code you want to hide.</span></span> <span data-ttu-id="c68ad-142">Код состояния сразу же пропадет из диаграммы.</span><span class="sxs-lookup"><span data-stu-id="c68ad-142">The status code will be immediately hidden from the graph.</span></span> <span data-ttu-id="c68ad-143">Если щелкнуть этот код состояния еще раз, он снова появится на диаграмме.</span><span class="sxs-lookup"><span data-stu-id="c68ad-143">Clicking that status code again will cause that option to be displayed again.</span></span>

## <a name="cache-statuses"></a><span data-ttu-id="c68ad-144">Состояния кэша</span><span class="sxs-lookup"><span data-stu-id="c68ad-144">Cache Statuses</span></span>
![Диаграмма "Состояния кэша"](./media/cdn-real-time-stats/cdn-cache-status.png)

<span data-ttu-id="c68ad-146">На диаграмме **Состояния кэша** показана частота возникновения определенных типов состояний кэша за выбранный период времени.</span><span class="sxs-lookup"><span data-stu-id="c68ad-146">The **Cache Statuses** graph indicates how often certain types of cache statuses are occurring over the selected time span.</span></span> 

> [!TIP]
> <span data-ttu-id="c68ad-147">Описание каждого параметра кода состояния кэша см. в разделе [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx) (Коды состояний кэша в сети Azure CDN).</span><span class="sxs-lookup"><span data-stu-id="c68ad-147">For a description of each cache status code option, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx).</span></span>
> 
> 

<span data-ttu-id="c68ad-148">Список кодов состояний кэша находится непосредственно над диаграммой.</span><span class="sxs-lookup"><span data-stu-id="c68ad-148">A list of cache status codes is displayed directly above the graph.</span></span> <span data-ttu-id="c68ad-149">В списке приводится каждый код состояния, который может быть включен в линейную диаграмму, и текущее количество вхождений в секунду этого кода состояния.</span><span class="sxs-lookup"><span data-stu-id="c68ad-149">This list indicates each status code that can be included in the line graph and the current number of occurrences per second for that status code.</span></span> <span data-ttu-id="c68ad-150">По умолчанию отображается строка для каждого кода состояния в диаграмме.</span><span class="sxs-lookup"><span data-stu-id="c68ad-150">By default, a line is displayed for each of these status codes in the graph.</span></span> <span data-ttu-id="c68ad-151">Однако можно отслеживать только те коды состояний, которые имеют особое значение для конфигурации сети CDN.</span><span class="sxs-lookup"><span data-stu-id="c68ad-151">However, you can choose to only monitor the status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="c68ad-152">Для этого проверьте требуемые коды состояний и очистите все другие параметры, а затем нажмите кнопку **Refresh Graph**(Обновить диаграмму).</span><span class="sxs-lookup"><span data-stu-id="c68ad-152">To do this, check the desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="c68ad-153">Можно временно скрыть данные журнала для определенного кода состояния.</span><span class="sxs-lookup"><span data-stu-id="c68ad-153">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="c68ad-154">В условных обозначениях непосредственно под диаграммой щелкните код состояния, который нужно скрыть.</span><span class="sxs-lookup"><span data-stu-id="c68ad-154">From the legend directly below the graph, click the status code you want to hide.</span></span> <span data-ttu-id="c68ad-155">Код состояния сразу же пропадет из диаграммы.</span><span class="sxs-lookup"><span data-stu-id="c68ad-155">The status code will be immediately hidden from the graph.</span></span> <span data-ttu-id="c68ad-156">Если щелкнуть этот код состояния еще раз, он снова появится на диаграмме.</span><span class="sxs-lookup"><span data-stu-id="c68ad-156">Clicking that status code again will cause that option to be displayed again.</span></span>

## <a name="connections"></a><span data-ttu-id="c68ad-157">Подключения</span><span class="sxs-lookup"><span data-stu-id="c68ad-157">Connections</span></span>
![Диаграмма "Подключения"](./media/cdn-real-time-stats/cdn-connections.png)

<span data-ttu-id="c68ad-159">На этой диаграмме показано количество подключений, установленных с пограничными серверами.</span><span class="sxs-lookup"><span data-stu-id="c68ad-159">This graph indicates how many connections have been established to your edge servers.</span></span> <span data-ttu-id="c68ad-160">Подключение устанавливается при каждом запросе к ресурсу, который проходит через сеть CDN.</span><span class="sxs-lookup"><span data-stu-id="c68ad-160">Each request for an asset that passes through our CDN results in a connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c68ad-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c68ad-161">Next Steps</span></span>
* <span data-ttu-id="c68ad-162">Получение уведомлений с помощью [оповещения в режиме реального времени в Azure CDN](cdn-real-time-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="c68ad-162">Get notified with [Real-time alerts in Azure CDN](cdn-real-time-alerts.md)</span></span>
* <span data-ttu-id="c68ad-163">Дополнительные сведения о [расширенных HTTP-отчетах](cdn-advanced-http-reports.md).</span><span class="sxs-lookup"><span data-stu-id="c68ad-163">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="c68ad-164">[Анализ вариантов использования CDN Azure](cdn-analyze-usage-patterns.md).</span><span class="sxs-lookup"><span data-stu-id="c68ad-164">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

