---
title: "Анализ aaaUser хранения для веб-приложений с помощью Azure Application Insights | Документы Microsoft"
description: "Сколько пользователей возвращает tooyour приложения?"
services: application-insights
documentationcenter: 
author: botatoes
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/03/2017
ms.author: bwren
ms.openlocfilehash: 8bcee5f1611afbd69016ec3eef27832c304762a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="user-retention-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="830ef-103">Анализ удержания пользователей веб-приложений с помощью Application Insights</span><span class="sxs-lookup"><span data-stu-id="830ef-103">User retention analysis for web applications with Application Insights</span></span>

<span data-ttu-id="830ef-104">возможность хранения Hello в [Azure Application Insights](app-insights-overview.md) помогает анализировать число пользователей, возвращают tooyour приложения и как часто они выполнять конкретные задачи и достижения целей.</span><span class="sxs-lookup"><span data-stu-id="830ef-104">hello retention feature in [Azure Application Insights](app-insights-overview.md) helps you analyze how many users return tooyour app, and how often they perform particular tasks or achieve goals.</span></span> <span data-ttu-id="830ef-105">Например при запуске игры сайта можно сравнить hello количеством пользователей, которые вернули toohello узла после потери игры с номером hello, возврата после успешному выполнению.</span><span class="sxs-lookup"><span data-stu-id="830ef-105">For example, if you run a game site, you could compare hello numbers of users who return toohello site after losing a game with hello number who return after winning.</span></span> <span data-ttu-id="830ef-106">Эти сведения помогут улучшить взаимодействие с пользователем и свою бизнес-стратегию.</span><span class="sxs-lookup"><span data-stu-id="830ef-106">This knowledge can help you improve both your user experience and your business strategy.</span></span>

## <a name="get-started"></a><span data-ttu-id="830ef-107">Начало работы</span><span class="sxs-lookup"><span data-stu-id="830ef-107">Get started</span></span>

<span data-ttu-id="830ef-108">Если данные в средство хранения hello в портале Application Insights hello, еще отсутствует [узнать, как tooget к работе со средствами использования hello](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="830ef-108">If you don't yet see data in hello retention tool in hello Application Insights portal, [learn how tooget started with hello usage tools](app-insights-usage-overview.md).</span></span>

## <a name="hello-retention-tool"></a><span data-ttu-id="830ef-109">Средство хранения Hello</span><span class="sxs-lookup"><span data-stu-id="830ef-109">hello Retention tool</span></span>

![Инструмент "Хранение"](./media/app-insights-usage-retention/retention.png)

1. <span data-ttu-id="830ef-111">Hello инструментов позволяет пользователям toocreate новых хранения отчетов, откройте существующих хранения отчетов, сохранить текущий отчет хранения или сохранить как, отменить изменения, внесенные toosaved отчеты, обновить данные в отчете hello, отчет с помощью электронной почты или прямую ссылку и hello доступа страница документации.</span><span class="sxs-lookup"><span data-stu-id="830ef-111">hello toolbar allows users toocreate new retention reports, open existing retention reports, save current retention report or save as, revert changes made toosaved reports, refresh data on hello report, share report via email or direct link, and access hello documentation page.</span></span> 
2. <span data-ttu-id="830ef-112">По умолчанию инструмент "Удержание" отображает всех пользователей, которые выполнили какие-либо операции, а затем вернулись и выполнили дополнительные операции в течение определенного периода.</span><span class="sxs-lookup"><span data-stu-id="830ef-112">By default, retention shows all users who did anything then came back and did anything else over a period.</span></span> <span data-ttu-id="830ef-113">Можно выбрать другое сочетание события toonarrow hello фокус на действия пользователя.</span><span class="sxs-lookup"><span data-stu-id="830ef-113">You can select different combination of events toonarrow hello focus on specific user activities.</span></span>
3. <span data-ttu-id="830ef-114">Добавьте один или несколько фильтров по свойствам.</span><span class="sxs-lookup"><span data-stu-id="830ef-114">Add one or more filters on properties.</span></span> <span data-ttu-id="830ef-115">Например, можно сосредоточиться на пользователях в определенной стране или регионе.</span><span class="sxs-lookup"><span data-stu-id="830ef-115">For example, you can focus on users in a particular country or region.</span></span> <span data-ttu-id="830ef-116">Нажмите кнопку **обновление** после настройки фильтров hello.</span><span class="sxs-lookup"><span data-stu-id="830ef-116">Click **Update** after setting hello filters.</span></span> 
4. <span data-ttu-id="830ef-117">Hello общая диаграмма хранения со сводкой хранения пользователя по hello указанного периода времени.</span><span class="sxs-lookup"><span data-stu-id="830ef-117">hello overall retention chart shows a summary of user retention across hello selected time period.</span></span> 
5. <span data-ttu-id="830ef-118">Hello Сетка отображает hello число пользователей храниться соответствующим построителя запросов toohello в #2.</span><span class="sxs-lookup"><span data-stu-id="830ef-118">hello grid shows hello number of users retained according toohello query builder in #2.</span></span> <span data-ttu-id="830ef-119">Каждая строка представляет группы пользователей, выполнившего любого события в период показанное время hello.</span><span class="sxs-lookup"><span data-stu-id="830ef-119">Each row represents a cohort of users who performed any event in hello time period shown.</span></span> <span data-ttu-id="830ef-120">Каждой ячейки в строке приветствия показывает, сколько этой группы возвращаются по крайней мере один раз в течение более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="830ef-120">Each cell in hello row shows how many of that cohort returned at least once in a later period.</span></span> <span data-ttu-id="830ef-121">Некоторые пользователи могут возвращаться в нескольких периодах.</span><span class="sxs-lookup"><span data-stu-id="830ef-121">Some users may return in more than one period.</span></span> 
6. <span data-ttu-id="830ef-122">Hello аналитики карты отображают пять верхних событий вызывающей стороны и пяти top возвращаются события toogive пользователей лучше понять их хранения отчетов.</span><span class="sxs-lookup"><span data-stu-id="830ef-122">hello insights cards show top five initiating events, and top five returned events toogive users a better understanding of their retention report.</span></span> 

![Наведение указателя мыши на компонент "Удержание"](./media/app-insights-usage-retention/hover.png)

<span data-ttu-id="830ef-124">Пользователей можно навести на ячейки на кнопки hello хранения инструмент tooaccess hello аналитики и всплывающие подсказки о том, какие ячейки hello означает.</span><span class="sxs-lookup"><span data-stu-id="830ef-124">Users can hover over cells on hello retention tool tooaccess hello analytics button and tool tips explaining what hello cell means.</span></span> <span data-ttu-id="830ef-125">Кнопка Analytics Hello возвращает средство аналитики toohello пользователей с заранее заданный запрос toogenerate пользователей из ячейки hello.</span><span class="sxs-lookup"><span data-stu-id="830ef-125">hello Analytics button takes users toohello Analytics tool with a pre-populated query toogenerate users from hello cell.</span></span> 

## <a name="use-business-events-tootrack-retention"></a><span data-ttu-id="830ef-126">Используйте хранения tootrack событий для бизнеса</span><span class="sxs-lookup"><span data-stu-id="830ef-126">Use business events tootrack retention</span></span>

<span data-ttu-id="830ef-127">tooget hello чаще хранения анализ, события мер, представляющих значительные бизнес-операции.</span><span class="sxs-lookup"><span data-stu-id="830ef-127">tooget hello most useful retention analysis, measure events that represent significant business activities.</span></span> 

<span data-ttu-id="830ef-128">Например многие пользователи могут откройте страницу в приложении без воспроизведения hello игра, которую он отображает.</span><span class="sxs-lookup"><span data-stu-id="830ef-128">For example, many users might open a page in your app without playing hello game that it displays.</span></span> <span data-ttu-id="830ef-129">Просто представления страницы приветствия отслеживания таким образом будет предоставлять неточной оценки того, сколько людей hello игры tooplay, возвращаемых после его ранее программ.</span><span class="sxs-lookup"><span data-stu-id="830ef-129">Tracking just hello page views would therefore provide an inaccurate estimate of how many people return tooplay hello game after enjoying it previously.</span></span> <span data-ttu-id="830ef-130">tooget четкое представление о возвращение проигрыватели, ваше приложение должно отправлять пользовательское событие, если пользователь фактически играет.</span><span class="sxs-lookup"><span data-stu-id="830ef-130">tooget a clear picture of returning players, your app should send a custom event when a user actually plays.</span></span>  

<span data-ttu-id="830ef-131">Это пользовательские события toocode хорошей практикой, представляющих основные коммерческие действия, которые используются для хранения анализа.</span><span class="sxs-lookup"><span data-stu-id="830ef-131">It's good practice toocode custom events that represent key business actions, and use these for your retention analysis.</span></span> <span data-ttu-id="830ef-132">hello результат toocapture игры, необходимо toowrite строку кода toosend пользовательское событие tooApplication аналитики.</span><span class="sxs-lookup"><span data-stu-id="830ef-132">toocapture hello game outcome, you need toowrite a line of code toosend a custom event tooApplication Insights.</span></span> <span data-ttu-id="830ef-133">Если при создании в коде hello веб-странице или в Node.JS, он выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="830ef-133">If you write it in hello web page code or in Node.JS, it looks like this:</span></span>

```JavaScript
    appinsights.trackEvent("won game");
```

<span data-ttu-id="830ef-134">Можно так же использовать код сервера ASP.NET, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="830ef-134">Or in ASP.NET server code:</span></span>

```C#
   telemetry.TrackEvent("won game");
```

<span data-ttu-id="830ef-135">[Узнайте больше о создании пользовательских событий](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="830ef-135">[Learn more about writing custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>


## <a name="next-steps"></a><span data-ttu-id="830ef-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="830ef-136">Next steps</span></span>
- <span data-ttu-id="830ef-137">опыт использования tooenable, начать отправку [пользовательские события](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) или [просмотры страниц](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="830ef-137">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="830ef-138">При отправке уже, пользовательские события и представления страницы, просмотр hello использования средств toolearn как пользователям использовать эту службу.</span><span class="sxs-lookup"><span data-stu-id="830ef-138">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    - [<span data-ttu-id="830ef-139">Пользователи, сеансы, события</span><span class="sxs-lookup"><span data-stu-id="830ef-139">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="830ef-140">Воронки</span><span class="sxs-lookup"><span data-stu-id="830ef-140">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="830ef-141">Средство "Маршруты пользователей"</span><span class="sxs-lookup"><span data-stu-id="830ef-141">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="830ef-142">Книги</span><span class="sxs-lookup"><span data-stu-id="830ef-142">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="830ef-143">Добавление контекста пользователей</span><span class="sxs-lookup"><span data-stu-id="830ef-143">Add user context</span></span>](app-insights-usage-send-user-context.md)


