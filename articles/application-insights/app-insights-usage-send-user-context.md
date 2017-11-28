---
title: "Использование tooenable контекст пользователя aaaSending возможности Azure Application Insights | Документы Microsoft"
description: "Отслеживайте, как пользователи перемещаются по службе, назначив каждому из них строку уникального постоянного идентификатора в Application Insights."
services: application-insights
documentationcenter: 
author: abgreg
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: csharp
ms.topic: article
ms.date: 08/02/2017
ms.author: bwren
ms.openlocfilehash: 0e6c2348f53a3ea970060334179b0dd070925e82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
#  <a name="sending-user-context-tooenable-usage-experiences-in-azure-application-insights"></a><span data-ttu-id="d55f1-103">Отправка использование tooenable контекст пользователя возникает в Azure Application Insights</span><span class="sxs-lookup"><span data-stu-id="d55f1-103">Sending user context tooenable usage experiences in Azure Application Insights</span></span>

## <a name="tracking-users"></a><span data-ttu-id="d55f1-104">Отслеживание пользователей</span><span class="sxs-lookup"><span data-stu-id="d55f1-104">Tracking users</span></span>

<span data-ttu-id="d55f1-105">Application Insights позволяет вам toomonitor и отслеживать пользователей через набор средств использования продукта:</span><span class="sxs-lookup"><span data-stu-id="d55f1-105">Application Insights enables you toomonitor and track your users through a set of product usage tools:</span></span> 
* [<span data-ttu-id="d55f1-106">Пользователи, сеансы, события</span><span class="sxs-lookup"><span data-stu-id="d55f1-106">Users, Sessions, Events</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-segmentation)
* [<span data-ttu-id="d55f1-107">Воронки</span><span class="sxs-lookup"><span data-stu-id="d55f1-107">Funnels</span></span>](https://docs.microsoft.com/azure/application-insights/usage-funnels)
* [<span data-ttu-id="d55f1-108">Сохранение</span><span class="sxs-lookup"><span data-stu-id="d55f1-108">Retention</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-retention)
* <span data-ttu-id="d55f1-109">когорты;</span><span class="sxs-lookup"><span data-stu-id="d55f1-109">Cohorts</span></span>
* [<span data-ttu-id="d55f1-110">Книги</span><span class="sxs-lookup"><span data-stu-id="d55f1-110">Workbooks</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-workbooks)

<span data-ttu-id="d55f1-111">В tootrack порядке, что пользователь выполняет со временем Application Insights требуется идентификатор для каждого пользователя или сеанса.</span><span class="sxs-lookup"><span data-stu-id="d55f1-111">In order tootrack what a user does over time, Application Insights needs an ID for each user or session.</span></span> <span data-ttu-id="d55f1-112">Включите эти идентификаторы в каждое представление пользовательского события или страницы.</span><span class="sxs-lookup"><span data-stu-id="d55f1-112">Include these IDs in every custom event or page view.</span></span>
- <span data-ttu-id="d55f1-113">Для пользователей, воронок, инструментов хранения и когорт: включите идентификатор пользователя.</span><span class="sxs-lookup"><span data-stu-id="d55f1-113">Users, Funnels, Retention, and Cohorts: Include user ID.</span></span>
- <span data-ttu-id="d55f1-114">Для сеансов: включите идентификатор сеанса.</span><span class="sxs-lookup"><span data-stu-id="d55f1-114">Sessions: Include session ID.</span></span>

<span data-ttu-id="d55f1-115">Если приложение интегрировано с hello [JavaScript SDK](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page), автоматически отслеживаются идентификатор пользователя.</span><span class="sxs-lookup"><span data-stu-id="d55f1-115">If your app is integrated with hello [JavaScript SDK](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page), user ID is tracked automatically.</span></span>

## <a name="choosing-user-ids"></a><span data-ttu-id="d55f1-116">Выбор идентификаторов пользователей</span><span class="sxs-lookup"><span data-stu-id="d55f1-116">Choosing user IDs</span></span>

<span data-ttu-id="d55f1-117">Идентификаторы пользователей должны быть постоянными в tootrack сеансы пользователей поведение пользователей со временем.</span><span class="sxs-lookup"><span data-stu-id="d55f1-117">User IDs should persist across user sessions tootrack how users behave over time.</span></span> <span data-ttu-id="d55f1-118">Существуют различные подходы для сохранения идентификатора hello.</span><span class="sxs-lookup"><span data-stu-id="d55f1-118">There are various approaches for persisting hello ID.</span></span>
- <span data-ttu-id="d55f1-119">Определение пользователя, уже имеющееся в службе.</span><span class="sxs-lookup"><span data-stu-id="d55f1-119">A definition of a user that you already have in your service.</span></span>
- <span data-ttu-id="d55f1-120">Если службы hello браузера tooa доступ, его можно передать браузера hello куки-файл с Идентификатором его.</span><span class="sxs-lookup"><span data-stu-id="d55f1-120">If hello service has access tooa browser, it can pass hello browser a cookie with an ID in it.</span></span> <span data-ttu-id="d55f1-121">Идентификатор Hello будет сохраняться для пребывания hello cookie в браузере пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="d55f1-121">hello ID will persist for as long as hello cookie remains in hello user's browser.</span></span>
- <span data-ttu-id="d55f1-122">При необходимости можно использовать новый идентификатор каждого сеанса, но результаты hello о пользователях будут ограничены.</span><span class="sxs-lookup"><span data-stu-id="d55f1-122">If necessary, you can use a new ID each session, but hello results about users will be limited.</span></span> <span data-ttu-id="d55f1-123">Например не будет возможности toosee как поведение пользователя меняется со временем.</span><span class="sxs-lookup"><span data-stu-id="d55f1-123">For example, you won't be able toosee how a user's behavior changes over time.</span></span>

<span data-ttu-id="d55f1-124">Идентификатор Hello должно быть идентификатором Guid или другой строковым недостаточно сложный tooidentify каждого пользователя уникально.</span><span class="sxs-lookup"><span data-stu-id="d55f1-124">hello ID should be a Guid or another string complex enough tooidentify each user uniquely.</span></span> <span data-ttu-id="d55f1-125">Например, это может быть длинное случайное число.</span><span class="sxs-lookup"><span data-stu-id="d55f1-125">For example, it could be a long random number.</span></span>

<span data-ttu-id="d55f1-126">Если идентификатор hello содержит персональные идентификационные сведения о пользователе hello, не соответствующее значение toosend tooApplication аналитики как идентификатор пользователя.</span><span class="sxs-lookup"><span data-stu-id="d55f1-126">If hello ID contains personally identifying information about hello user, it is not an appropriate value toosend tooApplication Insights as a user ID.</span></span> <span data-ttu-id="d55f1-127">Вы можете отправить такой код как [идентификатор пользователя с проверкой подлинности](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users), но не удовлетворяет hello требования идентификатор пользователя для сценариев использования.</span><span class="sxs-lookup"><span data-stu-id="d55f1-127">You can send such an ID as an [authenticated user ID](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users), but it does not fulfill hello user ID requirement for usage scenarios.</span></span>

## <a name="aspnet-apps-set-user-context-in-an-itelemetryinitializer"></a><span data-ttu-id="d55f1-128">Приложения ASP.NET: установка контекста пользователя в ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="d55f1-128">ASP.NET Apps: Set user context in an ITelemetryInitializer</span></span>

<span data-ttu-id="d55f1-129">Создание инициализатор телеметрии как подробно описано [здесь](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer)и набор hello Context.User.Id и hello Context.Session.Id.</span><span class="sxs-lookup"><span data-stu-id="d55f1-129">Create a telemetry initializer, as described in detail [here](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer), and set hello Context.User.Id and hello Context.Session.Id.</span></span>

<span data-ttu-id="d55f1-130">Этот пример устанавливает идентификатор tooan идентификатор пользователя hello, срок действия сеанса hello.</span><span class="sxs-lookup"><span data-stu-id="d55f1-130">This example sets hello user ID tooan identifier that expires after hello session.</span></span> <span data-ttu-id="d55f1-131">По возможности используйте идентификатор пользователя, который сохраняется между сеансами.</span><span class="sxs-lookup"><span data-stu-id="d55f1-131">If possible, use a user ID that persists across sessions.</span></span>

<span data-ttu-id="d55f1-132">*C#*</span><span class="sxs-lookup"><span data-stu-id="d55f1-132">*C#*</span></span>

```C#

    using System;
    using System.Web;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that sets hello user ID.
       *
       */
      public class MyTelemetryInitializer : ITelemetryInitializer
      {
        public void Initialize(ITelemetry telemetry)
        {
            // For a full experience, track each user across sessions. For an incomplete view of user 
            // behavior within a session, store user ID on hello HttpContext Session.
            // Set hello user ID if we haven't done so yet.
            if (HttpContext.Current.Session["UserId"] == null)
            {
                HttpContext.Current.Session["UserId"] = Guid.NewGuid();
            }

            // Set hello user id on hello Application Insights telemetry item.
            telemetry.Context.User.Id = (string)HttpContext.Current.Session["UserId"];

            // Set hello session id on hello Application Insights telemetry item.
            telemetry.Context.Session.Id = HttpContext.Current.Session.SessionID;
        }
      }
    }
```

## <a name="next-steps"></a><span data-ttu-id="d55f1-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d55f1-133">Next steps</span></span>
- <span data-ttu-id="d55f1-134">опыт использования tooenable, начать отправку [пользовательские события](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) или [просмотры страниц](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="d55f1-134">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="d55f1-135">При отправке уже, пользовательские события и представления страницы, просмотр hello использования средств toolearn как пользователям использовать эту службу.</span><span class="sxs-lookup"><span data-stu-id="d55f1-135">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    * [<span data-ttu-id="d55f1-136">Общие сведения об использовании</span><span class="sxs-lookup"><span data-stu-id="d55f1-136">Usage overview</span></span>](app-insights-usage-overview.md)
    * [<span data-ttu-id="d55f1-137">Анализ пользователей, сеансов и событий в Application Insights</span><span class="sxs-lookup"><span data-stu-id="d55f1-137">Users, Sessions, and Events</span></span>](app-insights-usage-segmentation.md)
    * [<span data-ttu-id="d55f1-138">Воронки</span><span class="sxs-lookup"><span data-stu-id="d55f1-138">Funnels</span></span>](usage-funnels.md)
    * [<span data-ttu-id="d55f1-139">Сохранение</span><span class="sxs-lookup"><span data-stu-id="d55f1-139">Retention</span></span>](app-insights-usage-retention.md)
    * [<span data-ttu-id="d55f1-140">Книги</span><span class="sxs-lookup"><span data-stu-id="d55f1-140">Workbooks</span></span>](app-insights-usage-workbooks.md)
