---
title: "Статистика aaaReal времени в Azure CDN | Документы Microsoft"
description: "Статистические данные в режиме реального времени предоставляет в реальном времени данных о производительности hello Azure CDN при доставке содержимого tooyour клиентов."
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
ms.openlocfilehash: 68900a5092b767e45c1fdf9cef2cd03f55f38a6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-stats-in-microsoft-azure-cdn"></a><span data-ttu-id="c1680-103">Статистика в реальном времени в сети CDN Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="c1680-103">Real-time stats in Microsoft Azure CDN</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="c1680-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="c1680-104">Overview</span></span>
<span data-ttu-id="c1680-105">В этом документе содержатся сведения о статистике в реальном времени в сети CDN Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="c1680-105">This document explains real-time stats in Microsoft Azure CDN.</span></span>  <span data-ttu-id="c1680-106">Эта функция предоставляет данные в реальном времени, такие как пропускной способности, состояния кэша и tooyour одновременных подключений CDN профиля при доставке содержимого tooyour клиентов.</span><span class="sxs-lookup"><span data-stu-id="c1680-106">This functionality provides real-time data, such as bandwidth, cache statuses, and concurrent connections tooyour CDN profile when delivering content tooyour clients.</span></span> <span data-ttu-id="c1680-107">Благодаря этому постоянный мониторинг работоспособности hello службы в любое время, включая вещание события.</span><span class="sxs-lookup"><span data-stu-id="c1680-107">This enables continuous monitoring of hello health of your service at any time, including go-live events.</span></span>

<span data-ttu-id="c1680-108">доступны следующие графики Hello.</span><span class="sxs-lookup"><span data-stu-id="c1680-108">hello following graphs are available:</span></span>

* [<span data-ttu-id="c1680-109">Пропускная способность</span><span class="sxs-lookup"><span data-stu-id="c1680-109">Bandwidth</span></span>](#bandwidth)
* [<span data-ttu-id="c1680-110">Коды состояний</span><span class="sxs-lookup"><span data-stu-id="c1680-110">Status Codes</span></span>](#status-codes)
* [<span data-ttu-id="c1680-111">Состояния кэша</span><span class="sxs-lookup"><span data-stu-id="c1680-111">Cache Statuses</span></span>](#cache-statuses)
* [<span data-ttu-id="c1680-112">Подключения</span><span class="sxs-lookup"><span data-stu-id="c1680-112">Connections</span></span>](#connections)

## <a name="accessing-real-time-stats"></a><span data-ttu-id="c1680-113">Доступ к статистике в реальном времени</span><span class="sxs-lookup"><span data-stu-id="c1680-113">Accessing real-time stats</span></span>
1. <span data-ttu-id="c1680-114">В hello [портала Azure](https://portal.azure.com), Обзор профиля CDN tooyour.</span><span class="sxs-lookup"><span data-stu-id="c1680-114">In hello [Azure Portal](https://portal.azure.com), browse tooyour CDN profile.</span></span>
   
    ![Колонка профиля сети CDN](./media/cdn-real-time-stats/cdn-profile-blade.png)
2. <span data-ttu-id="c1680-116">В колонке профиля CDN hello выберите hello **управление** кнопки.</span><span class="sxs-lookup"><span data-stu-id="c1680-116">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![Кнопка управления в колонке профиля CDN](./media/cdn-real-time-stats/cdn-manage-btn.png)
   
    <span data-ttu-id="c1680-118">Открытие портала управления CDN Hello.</span><span class="sxs-lookup"><span data-stu-id="c1680-118">hello CDN management portal opens.</span></span>
3. <span data-ttu-id="c1680-119">Наведите указатель мыши hello **Analytics** , а затем наведите указатель мыши hello **статистики в реальном времени** всплывающим меню.</span><span class="sxs-lookup"><span data-stu-id="c1680-119">Hover over hello **Analytics** tab, then hover over hello **Real-Time Stats** flyout.</span></span>  <span data-ttu-id="c1680-120">Щелкните **Большой HTTP-объект**.</span><span class="sxs-lookup"><span data-stu-id="c1680-120">Click on **HTTP Large Object**.</span></span>
   
    ![Портал управления CDN](./media/cdn-real-time-stats/cdn-premium-portal.png)
   
    <span data-ttu-id="c1680-122">Отобразятся три диаграммы в режиме реального времени stats Hello.</span><span class="sxs-lookup"><span data-stu-id="c1680-122">hello real-time stats graphs are displayed.</span></span>

<span data-ttu-id="c1680-123">Каждый из диаграмм hello отображает статистику реального времени для интервала времени hello выбран запуск при загрузке страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="c1680-123">Each of hello graphs displays real-time statistics for hello selected time span, starting when hello page loads.</span></span>  <span data-ttu-id="c1680-124">графы Hello автоматическое обновление каждые несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="c1680-124">hello graphs update automatically every few seconds.</span></span>  <span data-ttu-id="c1680-125">Hello **обновление Graph** кнопки, если он имеется, приведет к очистке graph hello, после чего он отобразит только hello выбранных данных.</span><span class="sxs-lookup"><span data-stu-id="c1680-125">hello **Refresh Graph** button, if present, will clear hello graph, after which it will only display hello selected data.</span></span>

## <a name="bandwidth"></a><span data-ttu-id="c1680-126">Пропускная способность</span><span class="sxs-lookup"><span data-stu-id="c1680-126">Bandwidth</span></span>
![Диаграмма "Пропускная способность"](./media/cdn-real-time-stats/cdn-bandwidth.png)

<span data-ttu-id="c1680-128">Hello **пропускной способности** гистограмма отображает hello объем пропускной способности, используемой для текущей платформы hello по hello выбран интервал времени.</span><span class="sxs-lookup"><span data-stu-id="c1680-128">hello **Bandwidth** graph displays hello amount of bandwidth used for hello current platform over hello selected time span.</span></span> <span data-ttu-id="c1680-129">Hello затененная часть графа hello указывает использование пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="c1680-129">hello shaded portion of hello graph indicates bandwidth usage.</span></span> <span data-ttu-id="c1680-130">Hello точный объем пропускной способности, используемой в данный момент отображается непосредственно под hello линейный график.</span><span class="sxs-lookup"><span data-stu-id="c1680-130">hello exact amount of bandwidth currently being used is displayed directly below hello line graph.</span></span>

## <a name="status-codes"></a><span data-ttu-id="c1680-131">Коды состояний</span><span class="sxs-lookup"><span data-stu-id="c1680-131">Status Codes</span></span>
![Диаграмма "Код состояния"](./media/cdn-real-time-stats/cdn-status-codes.png)

<span data-ttu-id="c1680-133">Hello **коды состояния** граф показывает, как часто происходит определенные коды ответа HTTP по hello выбран интервал времени.</span><span class="sxs-lookup"><span data-stu-id="c1680-133">hello **Status Codes** graph indicates how often certain HTTP response codes are occurring over hello selected time span.</span></span>

> [!TIP]
> <span data-ttu-id="c1680-134">Описание каждого параметра кода состояния HTTP см. в разделе [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx) (Коды состояний HTTP в сети Azure CDN).</span><span class="sxs-lookup"><span data-stu-id="c1680-134">For a description of each HTTP status code option, see [Azure CDN HTTP Status Codes](https://msdn.microsoft.com/library/mt759238.aspx).</span></span>
> 
> 

<span data-ttu-id="c1680-135">Непосредственно над диаграммой hello отображается список кодов состояния HTTP.</span><span class="sxs-lookup"><span data-stu-id="c1680-135">A list of HTTP status codes is displayed directly above hello graph.</span></span> <span data-ttu-id="c1680-136">Этот список указывает каждого кода состояния, которое может быть включено в график hello и hello текущее число вхождений в секунду для этого кода состояния.</span><span class="sxs-lookup"><span data-stu-id="c1680-136">This list indicates each status code that can be included in hello line graph and hello current number of occurrences per second for that status code.</span></span> <span data-ttu-id="c1680-137">По умолчанию для каждого из этих кодов hello графике отображается строки.</span><span class="sxs-lookup"><span data-stu-id="c1680-137">By default, a line is displayed for each of these status codes in hello graph.</span></span> <span data-ttu-id="c1680-138">Тем не менее вы можете tooonly коды состояния hello монитора, которые имеют специальное значение для конфигурации CDN.</span><span class="sxs-lookup"><span data-stu-id="c1680-138">However, you can choose tooonly monitor hello status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="c1680-139">toodo это, проверьте коды состояния hello требуемого снимите все остальные параметры, а затем выберите **обновление Graph**.</span><span class="sxs-lookup"><span data-stu-id="c1680-139">toodo this, check hello desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="c1680-140">Можно временно скрыть данные журнала для определенного кода состояния.</span><span class="sxs-lookup"><span data-stu-id="c1680-140">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="c1680-141">Условные обозначения hello непосредственно под hello graph щелкните hello код состояния, который будет использоваться toohide.</span><span class="sxs-lookup"><span data-stu-id="c1680-141">From hello legend directly below hello graph, click hello status code you want toohide.</span></span> <span data-ttu-id="c1680-142">Код состояния Hello будет скрыт из графа hello немедленно.</span><span class="sxs-lookup"><span data-stu-id="c1680-142">hello status code will be immediately hidden from hello graph.</span></span> <span data-ttu-id="c1680-143">Повторное нажатие указанный код состояния вызовет toobe этот параметр, отображаются снова.</span><span class="sxs-lookup"><span data-stu-id="c1680-143">Clicking that status code again will cause that option toobe displayed again.</span></span>

## <a name="cache-statuses"></a><span data-ttu-id="c1680-144">Состояния кэша</span><span class="sxs-lookup"><span data-stu-id="c1680-144">Cache Statuses</span></span>
![Диаграмма "Состояния кэша"](./media/cdn-real-time-stats/cdn-cache-status.png)

<span data-ttu-id="c1680-146">Hello **состояния кэша** граф показывает, как часто происходит определенные виды состояния кэша по hello выбран интервал времени.</span><span class="sxs-lookup"><span data-stu-id="c1680-146">hello **Cache Statuses** graph indicates how often certain types of cache statuses are occurring over hello selected time span.</span></span> 

> [!TIP]
> <span data-ttu-id="c1680-147">Описание каждого параметра кода состояния кэша см. в разделе [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx) (Коды состояний кэша в сети Azure CDN).</span><span class="sxs-lookup"><span data-stu-id="c1680-147">For a description of each cache status code option, see [Azure CDN Cache Status Codes](https://msdn.microsoft.com/library/mt759237.aspx).</span></span>
> 
> 

<span data-ttu-id="c1680-148">Список кодов состояния кэша отображается непосредственно над диаграммой hello.</span><span class="sxs-lookup"><span data-stu-id="c1680-148">A list of cache status codes is displayed directly above hello graph.</span></span> <span data-ttu-id="c1680-149">Этот список указывает каждого кода состояния, которое может быть включено в график hello и hello текущее число вхождений в секунду для этого кода состояния.</span><span class="sxs-lookup"><span data-stu-id="c1680-149">This list indicates each status code that can be included in hello line graph and hello current number of occurrences per second for that status code.</span></span> <span data-ttu-id="c1680-150">По умолчанию для каждого из этих кодов hello графике отображается строки.</span><span class="sxs-lookup"><span data-stu-id="c1680-150">By default, a line is displayed for each of these status codes in hello graph.</span></span> <span data-ttu-id="c1680-151">Тем не менее вы можете tooonly коды состояния hello монитора, которые имеют специальное значение для конфигурации CDN.</span><span class="sxs-lookup"><span data-stu-id="c1680-151">However, you can choose tooonly monitor hello status codes that have special significance for your CDN configuration.</span></span> <span data-ttu-id="c1680-152">toodo это, проверьте коды состояния hello требуемого снимите все остальные параметры, а затем выберите **обновление Graph**.</span><span class="sxs-lookup"><span data-stu-id="c1680-152">toodo this, check hello desired status codes and clear all other options, then click **Refresh Graph**.</span></span> 

<span data-ttu-id="c1680-153">Можно временно скрыть данные журнала для определенного кода состояния.</span><span class="sxs-lookup"><span data-stu-id="c1680-153">You can temporarily hide logged data for a particular status code.</span></span>  <span data-ttu-id="c1680-154">Условные обозначения hello непосредственно под hello graph щелкните hello код состояния, который будет использоваться toohide.</span><span class="sxs-lookup"><span data-stu-id="c1680-154">From hello legend directly below hello graph, click hello status code you want toohide.</span></span> <span data-ttu-id="c1680-155">Код состояния Hello будет скрыт из графа hello немедленно.</span><span class="sxs-lookup"><span data-stu-id="c1680-155">hello status code will be immediately hidden from hello graph.</span></span> <span data-ttu-id="c1680-156">Повторное нажатие указанный код состояния вызовет toobe этот параметр, отображаются снова.</span><span class="sxs-lookup"><span data-stu-id="c1680-156">Clicking that status code again will cause that option toobe displayed again.</span></span>

## <a name="connections"></a><span data-ttu-id="c1680-157">Подключения</span><span class="sxs-lookup"><span data-stu-id="c1680-157">Connections</span></span>
![Диаграмма "Подключения"](./media/cdn-real-time-stats/cdn-connections.png)

<span data-ttu-id="c1680-159">На этом графике указывает, сколько подключения были установленного tooyour пограничные серверы.</span><span class="sxs-lookup"><span data-stu-id="c1680-159">This graph indicates how many connections have been established tooyour edge servers.</span></span> <span data-ttu-id="c1680-160">Подключение устанавливается при каждом запросе к ресурсу, который проходит через сеть CDN.</span><span class="sxs-lookup"><span data-stu-id="c1680-160">Each request for an asset that passes through our CDN results in a connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1680-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c1680-161">Next Steps</span></span>
* <span data-ttu-id="c1680-162">Получение уведомлений с помощью [оповещения в режиме реального времени в Azure CDN](cdn-real-time-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="c1680-162">Get notified with [Real-time alerts in Azure CDN](cdn-real-time-alerts.md)</span></span>
* <span data-ttu-id="c1680-163">Дополнительные сведения о [расширенных HTTP-отчетах](cdn-advanced-http-reports.md).</span><span class="sxs-lookup"><span data-stu-id="c1680-163">Dig deeper with [advanced HTTP reports](cdn-advanced-http-reports.md)</span></span>
* <span data-ttu-id="c1680-164">[Анализ вариантов использования CDN Azure](cdn-analyze-usage-patterns.md).</span><span class="sxs-lookup"><span data-stu-id="c1680-164">Analyze [usage patterns](cdn-analyze-usage-patterns.md)</span></span>

