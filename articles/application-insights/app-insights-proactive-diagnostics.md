---
title: "Интеллектуальное обнаружение в Azure Application Insights | Документация Майкрософт"
description: "Служба Application Insights автоматически выполняет углубленный анализ телеметрии вашего приложения и предупреждает о потенциальных проблемах."
services: application-insights
documentationcenter: windows
author: rakefetj
manager: carmonm
ms.assetid: 2eeb4a35-c7a1-49f7-9b68-4f4b860938b2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: f203b2a532ea721d9797c67a4750896e3ab2b9f7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="smart-detection-in-application-insights"></a><span data-ttu-id="5cf89-103">Интеллектуальное обнаружение в Application Insights</span><span class="sxs-lookup"><span data-stu-id="5cf89-103">Smart Detection in Application Insights</span></span>
 <span data-ttu-id="5cf89-104">Функция интеллектуального обнаружения автоматически предупреждает о потенциальных проблемах с производительностью в веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="5cf89-104">Smart Detection automatically warns you of potential performance problems in your web application.</span></span> <span data-ttu-id="5cf89-105">Она выполняет упреждающий анализ данных телеметрии, которые приложение отправляет в [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5cf89-105">It performs proactive analysis of the telemetry that your app sends to [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="5cf89-106">В случае внезапного увеличения частоты сбоев или числа аномальных тенденций в производительности клиента или сервера вы получите оповещение.</span><span class="sxs-lookup"><span data-stu-id="5cf89-106">If there is a sudden rise in failure rates, or abnormal patterns in client or server performance, you get an alert.</span></span> <span data-ttu-id="5cf89-107">Эта функция не требует настройки.</span><span class="sxs-lookup"><span data-stu-id="5cf89-107">This feature needs no configuration.</span></span> <span data-ttu-id="5cf89-108">Она работает, если приложение отправляет достаточный объем данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="5cf89-108">It operates if your application sends enough telemetry.</span></span>

<span data-ttu-id="5cf89-109">Оповещения об интеллектуальном обнаружении можно просматривать как в получаемых сообщениях электронной почты, так и в колонке Smart Detection (Интеллектуальное обнаружение).</span><span class="sxs-lookup"><span data-stu-id="5cf89-109">You can access Smart Detection alerts both from the emails you receive, and from the Smart Detection blade.</span></span>

## <a name="review-your-smart-detections"></a><span data-ttu-id="5cf89-110">Просмотр интеллектуального обнаружения</span><span class="sxs-lookup"><span data-stu-id="5cf89-110">Review your Smart Detections</span></span>
<span data-ttu-id="5cf89-111">Просматривать результаты обнаружения можно двумя способами.</span><span class="sxs-lookup"><span data-stu-id="5cf89-111">You can discover detections in two ways:</span></span>

* <span data-ttu-id="5cf89-112">**В сообщениях электронной почты** , получаемых из Application Insights.</span><span class="sxs-lookup"><span data-stu-id="5cf89-112">**You receive an email** from Application Insights.</span></span> <span data-ttu-id="5cf89-113">Вот типичный пример:</span><span class="sxs-lookup"><span data-stu-id="5cf89-113">Here's a typical example:</span></span>
  
    ![Оповещение по электронной почте](./media/app-insights-proactive-diagnostics/03.png)
  
    <span data-ttu-id="5cf89-115">Нажмите большую кнопку, чтобы просмотреть подробные сведения на портале.</span><span class="sxs-lookup"><span data-stu-id="5cf89-115">Click the big button to open more detail in the portal.</span></span>
* <span data-ttu-id="5cf89-116">На плитке **Smart Detection** (Интеллектуальное обнаружение) в колонке "Обзор" отображается количество последних оповещений.</span><span class="sxs-lookup"><span data-stu-id="5cf89-116">**The Smart Detection tile** on your app's overview blade shows a count of recent alerts.</span></span> <span data-ttu-id="5cf89-117">Щелкните плитку, чтобы просмотреть список последних оповещений.</span><span class="sxs-lookup"><span data-stu-id="5cf89-117">Click the tile to see a list of recent alerts.</span></span>

![Просмотр последних результатов обнаружения](./media/app-insights-proactive-diagnostics/04.png)

<span data-ttu-id="5cf89-119">Выберите оповещение, чтобы просмотреть сведения о нем.</span><span class="sxs-lookup"><span data-stu-id="5cf89-119">Select an alert to see its details.</span></span>

## <a name="what-problems-are-detected"></a><span data-ttu-id="5cf89-120">Какие проблемы можно обнаружить?</span><span class="sxs-lookup"><span data-stu-id="5cf89-120">What problems are detected?</span></span>
<span data-ttu-id="5cf89-121">Существует три типа обнаружения:</span><span class="sxs-lookup"><span data-stu-id="5cf89-121">There are three kinds of detection:</span></span>

* <span data-ttu-id="5cf89-122">[Интеллектуальное обнаружение. Аномальные сбои.](app-insights-proactive-failure-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="5cf89-122">[Smart detection - Failure Anomalies](app-insights-proactive-failure-diagnostics.md).</span></span> <span data-ttu-id="5cf89-123">С помощью машинного обучения мы настраиваем для вашего приложения ожидаемое количество неудачно завершенных запросов, сопоставляя его с нагрузкой и другими факторами.</span><span class="sxs-lookup"><span data-stu-id="5cf89-123">We use machine learning to set the expected rate of failed requests for your app, correlating with load and other factors.</span></span> <span data-ttu-id="5cf89-124">Если частота сбоев превысит ожидаемое ограничение, вам будет отправлено предупреждение.</span><span class="sxs-lookup"><span data-stu-id="5cf89-124">If the failure rate goes outside the expected envelope, we send an alert.</span></span>
* <span data-ttu-id="5cf89-125">[Интеллектуальное обнаружение. Аномалии производительности.](app-insights-proactive-performance-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="5cf89-125">[Smart detection - Performance Anomalies](app-insights-proactive-performance-diagnostics.md).</span></span> <span data-ttu-id="5cf89-126">Если время ответа операции или продолжительность зависимости длиннее по сравнению с базовым показателем за предыдущие периоды, или если обнаружен аномальный шаблон времени отклика и времени загрузки страницы, выводится уведомление.</span><span class="sxs-lookup"><span data-stu-id="5cf89-126">You get notifications if response time of an operation or dependency duration is slowing down compared to historical baseline or if we identify an anomalous pattern in response time or page load time.</span></span>   
* <span data-ttu-id="5cf89-127">[Интеллектуальное обнаружение. Неполадки облачной службы Azure.](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/)</span><span class="sxs-lookup"><span data-stu-id="5cf89-127">[Smart detection - Azure Cloud Service issues](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/).</span></span> <span data-ttu-id="5cf89-128">Вы получаете оповещения в том случае, если приложение размещено в облачных службах Azure и в экземпляре роли происходят сбои при запуске, частый перезапуск или сбои среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="5cf89-128">You get alerts if your app is hosted in Azure Cloud Services and a role instance has startup failures, frequent recycling, or runtime crashes.</span></span>

<span data-ttu-id="5cf89-129">(Каждое уведомление содержит ссылки на материалы соответствующих статей.)</span><span class="sxs-lookup"><span data-stu-id="5cf89-129">(The help links in each notification take you to the relevant articles.)</span></span>

## <a name="video"></a><span data-ttu-id="5cf89-130">Видео</span><span class="sxs-lookup"><span data-stu-id="5cf89-130">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="5cf89-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5cf89-131">Next steps</span></span>
<span data-ttu-id="5cf89-132">Эти диагностические средства позволяют проверять данные телеметрии из приложения:</span><span class="sxs-lookup"><span data-stu-id="5cf89-132">These diagnostic tools help you inspect the telemetry from your app:</span></span>

* [<span data-ttu-id="5cf89-133">Обозреватель метрик</span><span class="sxs-lookup"><span data-stu-id="5cf89-133">Metric explorer</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="5cf89-134">Обозреватель поиска</span><span class="sxs-lookup"><span data-stu-id="5cf89-134">Search explorer</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="5cf89-135">Аналитика, мощный язык запросов</span><span class="sxs-lookup"><span data-stu-id="5cf89-135">Analytics - powerful query language</span></span>](app-insights-analytics-tour.md)

<span data-ttu-id="5cf89-136">Интеллектуальное обнаружение — это полностью автоматическая функция.</span><span class="sxs-lookup"><span data-stu-id="5cf89-136">Smart Detection is completely automatic.</span></span> <span data-ttu-id="5cf89-137">но, возможно, вам потребуется настроить некоторые дополнительные оповещения.</span><span class="sxs-lookup"><span data-stu-id="5cf89-137">But maybe you'd like to set up some more alerts?</span></span>

* [<span data-ttu-id="5cf89-138">Настройка оповещений в Application Insights</span><span class="sxs-lookup"><span data-stu-id="5cf89-138">Manually configured metric alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="5cf89-139">Доступность веб-тестов</span><span class="sxs-lookup"><span data-stu-id="5cf89-139">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md) 

