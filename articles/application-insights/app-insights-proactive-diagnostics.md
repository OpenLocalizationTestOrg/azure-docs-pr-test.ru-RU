---
title: "aaaSmart обнаружения в Azure Application Insights | Документы Microsoft"
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
ms.openlocfilehash: f794476088fc69154eda2077b7a5cdc769fab3a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="smart-detection-in-application-insights"></a><span data-ttu-id="f4d6a-103">Интеллектуальное обнаружение в Application Insights</span><span class="sxs-lookup"><span data-stu-id="f4d6a-103">Smart Detection in Application Insights</span></span>
 <span data-ttu-id="f4d6a-104">Функция интеллектуального обнаружения автоматически предупреждает о потенциальных проблемах с производительностью в веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="f4d6a-104">Smart Detection automatically warns you of potential performance problems in your web application.</span></span> <span data-ttu-id="f4d6a-105">Он выполняет упреждающее анализа телеметрии hello, которое приложение отправляет слишком[Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f4d6a-105">It performs proactive analysis of hello telemetry that your app sends too[Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="f4d6a-106">В случае внезапного увеличения частоты сбоев или числа аномальных тенденций в производительности клиента или сервера вы получите оповещение.</span><span class="sxs-lookup"><span data-stu-id="f4d6a-106">If there is a sudden rise in failure rates, or abnormal patterns in client or server performance, you get an alert.</span></span> <span data-ttu-id="f4d6a-107">Эта функция не требует настройки.</span><span class="sxs-lookup"><span data-stu-id="f4d6a-107">This feature needs no configuration.</span></span> <span data-ttu-id="f4d6a-108">Она работает, если приложение отправляет достаточный объем данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="f4d6a-108">It operates if your application sends enough telemetry.</span></span>

<span data-ttu-id="f4d6a-109">Оповещения об обнаружении смарт-доступны как из hello сообщения электронной почты, получаемых, так и из колонки hello смарт-обнаружение.</span><span class="sxs-lookup"><span data-stu-id="f4d6a-109">You can access Smart Detection alerts both from hello emails you receive, and from hello Smart Detection blade.</span></span>

## <a name="review-your-smart-detections"></a><span data-ttu-id="f4d6a-110">Просмотр интеллектуального обнаружения</span><span class="sxs-lookup"><span data-stu-id="f4d6a-110">Review your Smart Detections</span></span>
<span data-ttu-id="f4d6a-111">Просматривать результаты обнаружения можно двумя способами.</span><span class="sxs-lookup"><span data-stu-id="f4d6a-111">You can discover detections in two ways:</span></span>

* <span data-ttu-id="f4d6a-112">**В сообщениях электронной почты** , получаемых из Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f4d6a-112">**You receive an email** from Application Insights.</span></span> <span data-ttu-id="f4d6a-113">Вот типичный пример:</span><span class="sxs-lookup"><span data-stu-id="f4d6a-113">Here's a typical example:</span></span>
  
    ![Оповещение по электронной почте](./media/app-insights-proactive-diagnostics/03.png)
  
    <span data-ttu-id="f4d6a-115">Нажмите большую кнопку tooopen hello более подробно в портал hello.</span><span class="sxs-lookup"><span data-stu-id="f4d6a-115">Click hello big button tooopen more detail in hello portal.</span></span>
* <span data-ttu-id="f4d6a-116">**Плитка смарт-обнаружение Hello** на общие сведения о приложении колонке показывает количество последних оповещений.</span><span class="sxs-lookup"><span data-stu-id="f4d6a-116">**hello Smart Detection tile** on your app's overview blade shows a count of recent alerts.</span></span> <span data-ttu-id="f4d6a-117">Щелкните плитку hello toosee список последних оповещений.</span><span class="sxs-lookup"><span data-stu-id="f4d6a-117">Click hello tile toosee a list of recent alerts.</span></span>

![Просмотр последних результатов обнаружения](./media/app-insights-proactive-diagnostics/04.png)

<span data-ttu-id="f4d6a-119">Выберите оповещения toosee сведения о нем.</span><span class="sxs-lookup"><span data-stu-id="f4d6a-119">Select an alert toosee its details.</span></span>

## <a name="what-problems-are-detected"></a><span data-ttu-id="f4d6a-120">Какие проблемы можно обнаружить?</span><span class="sxs-lookup"><span data-stu-id="f4d6a-120">What problems are detected?</span></span>
<span data-ttu-id="f4d6a-121">Существует три типа обнаружения:</span><span class="sxs-lookup"><span data-stu-id="f4d6a-121">There are three kinds of detection:</span></span>

* <span data-ttu-id="f4d6a-122">[Интеллектуальное обнаружение. Аномальные сбои.](app-insights-proactive-failure-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="f4d6a-122">[Smart detection - Failure Anomalies](app-insights-proactive-failure-diagnostics.md).</span></span> <span data-ttu-id="f4d6a-123">Мы используем машинного обучения tooset hello ожидается Частота сбоев запросов для приложения, сопоставление с нагрузочных тестов и других факторов.</span><span class="sxs-lookup"><span data-stu-id="f4d6a-123">We use machine learning tooset hello expected rate of failed requests for your app, correlating with load and other factors.</span></span> <span data-ttu-id="f4d6a-124">Если частота сбоев hello выйдет за пределы ожидаемого конверт hello, вам будет отправлено оповещение.</span><span class="sxs-lookup"><span data-stu-id="f4d6a-124">If hello failure rate goes outside hello expected envelope, we send an alert.</span></span>
* <span data-ttu-id="f4d6a-125">[Интеллектуальное обнаружение. Аномалии производительности.](app-insights-proactive-performance-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="f4d6a-125">[Smart detection - Performance Anomalies](app-insights-proactive-performance-diagnostics.md).</span></span> <span data-ttu-id="f4d6a-126">Получать уведомления, если время отклика продолжительность операции или зависимость, замедляя базовые сравниваемых toohistorical или определяются аномальных шаблон времени отклика или время загрузки страницы.</span><span class="sxs-lookup"><span data-stu-id="f4d6a-126">You get notifications if response time of an operation or dependency duration is slowing down compared toohistorical baseline or if we identify an anomalous pattern in response time or page load time.</span></span>   
* <span data-ttu-id="f4d6a-127">[Интеллектуальное обнаружение. Неполадки облачной службы Azure.](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/)</span><span class="sxs-lookup"><span data-stu-id="f4d6a-127">[Smart detection - Azure Cloud Service issues](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/).</span></span> <span data-ttu-id="f4d6a-128">Вы получаете оповещения в том случае, если приложение размещено в облачных службах Azure и в экземпляре роли происходят сбои при запуске, частый перезапуск или сбои среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="f4d6a-128">You get alerts if your app is hosted in Azure Cloud Services and a role instance has startup failures, frequent recycling, or runtime crashes.</span></span>

<span data-ttu-id="f4d6a-129">(ссылки на справку hello в каждом уведомлении перейти toohello статьи по этой теме.)</span><span class="sxs-lookup"><span data-stu-id="f4d6a-129">(hello help links in each notification take you toohello relevant articles.)</span></span>

## <a name="video"></a><span data-ttu-id="f4d6a-130">Видео</span><span class="sxs-lookup"><span data-stu-id="f4d6a-130">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="f4d6a-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f4d6a-131">Next steps</span></span>
<span data-ttu-id="f4d6a-132">Эти средства диагностики помогут проверить hello телеметрии из приложения:</span><span class="sxs-lookup"><span data-stu-id="f4d6a-132">These diagnostic tools help you inspect hello telemetry from your app:</span></span>

* [<span data-ttu-id="f4d6a-133">Обозреватель метрик</span><span class="sxs-lookup"><span data-stu-id="f4d6a-133">Metric explorer</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="f4d6a-134">Обозреватель поиска</span><span class="sxs-lookup"><span data-stu-id="f4d6a-134">Search explorer</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="f4d6a-135">Аналитика, мощный язык запросов</span><span class="sxs-lookup"><span data-stu-id="f4d6a-135">Analytics - powerful query language</span></span>](app-insights-analytics-tour.md)

<span data-ttu-id="f4d6a-136">Интеллектуальное обнаружение — это полностью автоматическая функция.</span><span class="sxs-lookup"><span data-stu-id="f4d6a-136">Smart Detection is completely automatic.</span></span> <span data-ttu-id="f4d6a-137">Но возможно хотелось бы tooset некоторые дополнительные предупреждений?</span><span class="sxs-lookup"><span data-stu-id="f4d6a-137">But maybe you'd like tooset up some more alerts?</span></span>

* [<span data-ttu-id="f4d6a-138">Настройка оповещений в Application Insights</span><span class="sxs-lookup"><span data-stu-id="f4d6a-138">Manually configured metric alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="f4d6a-139">Доступность веб-тестов</span><span class="sxs-lookup"><span data-stu-id="f4d6a-139">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md) 

