---
title: "aaaSet копирование веб-аналитики приложений для ASP.NET с помощью Azure Application Insights | Документы Microsoft"
description: "Настройка средств аналитики производительности, доступности и использования для веб-сайта ASP.NET, размещенного локально или в Azure."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d0eee3c0-b328-448f-8123-f478052751db
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: 61a3cdce68da48bfb9450b1d296acc1535f50a38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-application-insights-for-your-aspnet-website"></a><span data-ttu-id="11aaa-103">Настройка Application Insights для веб-сайта ASP.NET</span><span class="sxs-lookup"><span data-stu-id="11aaa-103">Set up Application Insights for your ASP.NET website</span></span>

<span data-ttu-id="11aaa-104">Эта процедура позволяет настроить вашей ASP.NET web app toosend телеметрии toohello [Azure Application Insights](app-insights-overview.md) службы.</span><span class="sxs-lookup"><span data-stu-id="11aaa-104">This procedure configures your ASP.NET web app toosend telemetry toohello [Azure Application Insights](app-insights-overview.md) service.</span></span> <span data-ttu-id="11aaa-105">Он работает для приложений ASP.NET, размещенных на сервере IIS или в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="11aaa-105">It works for ASP.NET apps that are hosted either in your own IIS server or in hello Cloud.</span></span> <span data-ttu-id="11aaa-106">Вы получите диаграммы и язык запросами, которые помогут понять hello производительности приложения и как люди используют ее, а также автоматического оповещения для сбоев или проблем с производительностью.</span><span class="sxs-lookup"><span data-stu-id="11aaa-106">You get charts and a powerful query language that help you understand hello performance of your app and how people are using it, plus automatic alerts on failures or performance issues.</span></span> <span data-ttu-id="11aaa-107">Многим разработчикам кажутся эти функции отлично, как их можно, но можно расширить и настроить hello телеметрии, если необходимо.</span><span class="sxs-lookup"><span data-stu-id="11aaa-107">Many developers find these features great as they are, but you can also extend and customize hello telemetry if you need to.</span></span>

<span data-ttu-id="11aaa-108">Настройка выполняется несколькими щелчками в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="11aaa-108">Setup takes just a few clicks in Visual Studio.</span></span> <span data-ttu-id="11aaa-109">У вас есть hello параметр tooavoid расходы, ограничивая объем hello телеметрии.</span><span class="sxs-lookup"><span data-stu-id="11aaa-109">You have hello option tooavoid charges by limiting hello volume of telemetry.</span></span> <span data-ttu-id="11aaa-110">Это позволяет вам tooexperiment и отладки или toomonitor сайт с не много пользователей.</span><span class="sxs-lookup"><span data-stu-id="11aaa-110">This allows you tooexperiment and debug, or toomonitor a site with not many users.</span></span> <span data-ttu-id="11aaa-111">Если вы решите, нужно заранее toogo и мониторинга на рабочем сайте, это легко tooraise hello ограничить позже.</span><span class="sxs-lookup"><span data-stu-id="11aaa-111">When you decide you want toogo ahead and monitor your production site, it's easy tooraise hello limit later.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="11aaa-112">Перед началом</span><span class="sxs-lookup"><span data-stu-id="11aaa-112">Before you start</span></span>
<span data-ttu-id="11aaa-113">Вам необходимы:</span><span class="sxs-lookup"><span data-stu-id="11aaa-113">You need:</span></span>

* <span data-ttu-id="11aaa-114">Visual Studio 2013 с обновлением 3 или более новая версия.</span><span class="sxs-lookup"><span data-stu-id="11aaa-114">Visual Studio 2013 update 3 or later.</span></span> <span data-ttu-id="11aaa-115">Чем новее версия, тем лучше.</span><span class="sxs-lookup"><span data-stu-id="11aaa-115">Later is better.</span></span>
* <span data-ttu-id="11aaa-116">Подписка слишком[Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="11aaa-116">A subscription too[Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="11aaa-117">Если в команде или организации имеет подписку Azure, владелец hello можно добавить вы tooit, с помощью вашей [учетную запись Майкрософт](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="11aaa-117">If your team or organization has an Azure subscription, hello owner can add you tooit, by using your [Microsoft account](http://live.com).</span></span>

<span data-ttu-id="11aaa-118">Если вы заинтересованы в существует toolook альтернативные разделы в:</span><span class="sxs-lookup"><span data-stu-id="11aaa-118">There are alternative topics toolook at if you are interested in:</span></span>

* [<span data-ttu-id="11aaa-119">инструментирование веб-приложения во время выполнения;</span><span class="sxs-lookup"><span data-stu-id="11aaa-119">Instrumenting a web app at runtime</span></span>](app-insights-monitor-performance-live-website-now.md)
* [<span data-ttu-id="11aaa-120">облачных служб Azure</span><span class="sxs-lookup"><span data-stu-id="11aaa-120">Azure Cloud Services</span></span>](app-insights-cloudservices.md)

## <span data-ttu-id="11aaa-121"><a name="ide"></a>Шаг 1: Добавление hello пакет SDK Application Insights</span><span class="sxs-lookup"><span data-stu-id="11aaa-121"><a name="ide"></a> Step 1: Add hello Application Insights SDK</span></span>

<span data-ttu-id="11aaa-122">В обозревателе решений щелкните проект веб-приложения правой кнопкой мыши и выберите пункт **Добавить** > **Телеметрия Application Insights** или **Настроить Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="11aaa-122">Right-click your web app project in Solution Explorer, and choose **Add** > **Application Insights Telemetry...** or **Configure Application Insights**.</span></span>

![Снимок экрана с окном обозревателя решений, где выделен параметр "Добавить" и "Телеметрия Application Insights"](./media/app-insights-asp-net/appinsights-03-addExisting.png)

<span data-ttu-id="11aaa-124">(В Visual Studio 2015 также есть параметр tooadd Application Insights, в диалоговом окне нового проекта hello.)</span><span class="sxs-lookup"><span data-stu-id="11aaa-124">(In Visual Studio 2015, there's also an option tooadd Application Insights in hello New Project dialog.)</span></span>

<span data-ttu-id="11aaa-125">Продолжить-страница конфигурации toohello Application Insights:</span><span class="sxs-lookup"><span data-stu-id="11aaa-125">Continue toohello Application Insights configuration page:</span></span>

![Снимок экрана с окном страницы "Зарегистрировать приложение в Application Insights"](./media/app-insights-asp-net/visual-studio-register-dialog.png)

<span data-ttu-id="11aaa-127">**а.**</span><span class="sxs-lookup"><span data-stu-id="11aaa-127">**a.**</span></span> <span data-ttu-id="11aaa-128">Выберите учетную запись hello и подписки, которая используется tooaccess Azure.</span><span class="sxs-lookup"><span data-stu-id="11aaa-128">Select hello account and subscription that you use tooaccess Azure.</span></span>

<span data-ttu-id="11aaa-129">**б.**</span><span class="sxs-lookup"><span data-stu-id="11aaa-129">**b.**</span></span> <span data-ttu-id="11aaa-130">Выберите ресурс hello в Azure, где вы хотите toosee hello данные из приложения.</span><span class="sxs-lookup"><span data-stu-id="11aaa-130">Select hello resource in Azure where you want toosee hello data from your app.</span></span> <span data-ttu-id="11aaa-131">Обычно:</span><span class="sxs-lookup"><span data-stu-id="11aaa-131">Usually:</span></span>

* <span data-ttu-id="11aaa-132">Используйте [один ресурс для разных компонентов](app-insights-monitor-multi-role-apps.md) одного приложения.</span><span class="sxs-lookup"><span data-stu-id="11aaa-132">Use a [single resource for different components](app-insights-monitor-multi-role-apps.md) of a single application.</span></span> 
* <span data-ttu-id="11aaa-133">Создавайте разные ресурсы для несвязанных приложений.</span><span class="sxs-lookup"><span data-stu-id="11aaa-133">Create separate resources for unrelated applications.</span></span>
 
<span data-ttu-id="11aaa-134">Tooset hello ресурсов группы или hello место хранения данных, нажмите кнопку **настройки**.</span><span class="sxs-lookup"><span data-stu-id="11aaa-134">If you want tooset hello resource group or hello location where your data is stored, click **Configure settings**.</span></span> <span data-ttu-id="11aaa-135">Группы ресурсов — используется toocontrol toodata доступа.</span><span class="sxs-lookup"><span data-stu-id="11aaa-135">Resource groups are used toocontrol access toodata.</span></span> <span data-ttu-id="11aaa-136">Например, если имеется несколько приложений, являющиеся частью hello же системе, может поместить данные Application Insights в hello одну группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="11aaa-136">For example, if you have several apps that form part of hello same system, you might put their Application Insights data in hello same resource group.</span></span>

<span data-ttu-id="11aaa-137">**в.**</span><span class="sxs-lookup"><span data-stu-id="11aaa-137">**c.**</span></span> <span data-ttu-id="11aaa-138">Задайте ограничение на ограничение тома данных free hello, tooavoid расходов.</span><span class="sxs-lookup"><span data-stu-id="11aaa-138">Set a cap at hello free data volume limit, tooavoid charges.</span></span> <span data-ttu-id="11aaa-139">Application Insights Освободите tooa определенных объем телеметрии.</span><span class="sxs-lookup"><span data-stu-id="11aaa-139">Application Insights is free up tooa certain volume of telemetry.</span></span> <span data-ttu-id="11aaa-140">После создания ресурса hello можно изменить выбранные параметры на портале hello, открыв **компоненты и цены** > **управление томами данных** > **ежедневно ограничение тома**.</span><span class="sxs-lookup"><span data-stu-id="11aaa-140">After hello resource is created, you can change your selection in hello portal by opening  **Features + pricing** > **Data volume management** > **Daily volume cap**.</span></span>

<span data-ttu-id="11aaa-141">**г.**</span><span class="sxs-lookup"><span data-stu-id="11aaa-141">**d.**</span></span> <span data-ttu-id="11aaa-142">Нажмите кнопку **зарегистрировать** toogo вперед и настраивать Application Insights для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="11aaa-142">Click **Register** toogo ahead and configure Application Insights for your web app.</span></span> <span data-ttu-id="11aaa-143">Данные телеметрии будут отправляться toohello [портал Azure](https://portal.azure.com), во время отладки и после публикации приложения.</span><span class="sxs-lookup"><span data-stu-id="11aaa-143">Telemetry will be sent toohello [Azure portal](https://portal.azure.com), both during debugging and after you have published your app.</span></span>

<span data-ttu-id="11aaa-144">**д.**</span><span class="sxs-lookup"><span data-stu-id="11aaa-144">**e.**</span></span> <span data-ttu-id="11aaa-145">Если вы не хотите toosend телеметрии toohello портала во время отладки, просто добавьте tooyour приложение hello пакет SDK Application Insights, но не настраивайте ресурса в портале hello.</span><span class="sxs-lookup"><span data-stu-id="11aaa-145">If you don't want toosend telemetry toohello portal while you're debugging, just add hello Application Insights SDK tooyour app but don't configure a resource in hello portal.</span></span> <span data-ttu-id="11aaa-146">Можно будет toosee телеметрии в Visual Studio в процессе отладки.</span><span class="sxs-lookup"><span data-stu-id="11aaa-146">You will be able toosee telemetry in Visual Studio while you are debugging.</span></span> <span data-ttu-id="11aaa-147">Позже, можно вернуть страницу настройки toothis или удалось дождаться после развертывания приложения и [переключиться на телеметрии во время выполнения](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="11aaa-147">Later, you can return toothis configuration page, or you could wait until after you have deployed your app and [switch on telemetry at run time](app-insights-monitor-performance-live-website-now.md).</span></span>


## <span data-ttu-id="11aaa-148"><a name="run"></a> Шаг 2. Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="11aaa-148"><a name="run"></a> Step 2: Run your app</span></span>
<span data-ttu-id="11aaa-149">Запустите приложение, нажав клавишу F5.</span><span class="sxs-lookup"><span data-stu-id="11aaa-149">Run your app with F5.</span></span> <span data-ttu-id="11aaa-150">Откройте некоторые телеметрии toogenerate разным страницам.</span><span class="sxs-lookup"><span data-stu-id="11aaa-150">Open different pages toogenerate some telemetry.</span></span>

<span data-ttu-id="11aaa-151">В Visual Studio отображается количество событий hello, которые были записаны.</span><span class="sxs-lookup"><span data-stu-id="11aaa-151">In Visual Studio, you see a count of hello events that have been logged.</span></span>

![Снимок экрана, где отображается Visual Studio](./media/app-insights-asp-net/54.png)

## <a name="step-3-see-your-telemetry"></a><span data-ttu-id="11aaa-154">Шаг 3. Просмотр данных телеметрии</span><span class="sxs-lookup"><span data-stu-id="11aaa-154">Step 3: See your telemetry</span></span>
<span data-ttu-id="11aaa-155">Вы увидите телеметрии в Visual Studio или на веб-портале Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="11aaa-155">You can see your telemetry either in Visual Studio or in hello Application Insights web portal.</span></span> <span data-ttu-id="11aaa-156">Поиск телеметрии в Visual Studio toohelp отладке приложения.</span><span class="sxs-lookup"><span data-stu-id="11aaa-156">Search telemetry in Visual Studio toohelp you debug your app.</span></span> <span data-ttu-id="11aaa-157">Мониторинг производительности и использовании hello веб-портале, когда система находится в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="11aaa-157">Monitor performance and usage in hello web portal when your system is live.</span></span> 

### <a name="see-your-telemetry-in-visual-studio"></a><span data-ttu-id="11aaa-158">Просмотр данных телеметрии в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="11aaa-158">See your telemetry in Visual Studio</span></span>

<span data-ttu-id="11aaa-159">В Visual Studio откройте окно hello Application Insights.</span><span class="sxs-lookup"><span data-stu-id="11aaa-159">In Visual Studio, open hello Application Insights window.</span></span> <span data-ttu-id="11aaa-160">Либо щелкните hello **Application Insights** кнопку или щелкните правой кнопкой мыши проект в обозревателе решений выберите **Application Insights**и нажмите кнопку **поиск телеметрии Live**.</span><span class="sxs-lookup"><span data-stu-id="11aaa-160">Either click hello **Application Insights** button, or right-click your project in Solution Explorer, select **Application Insights**, and then click **Search Live Telemetry**.</span></span>

<span data-ttu-id="11aaa-161">В окне поиска Visual Studio Application Insights hello просмотреть hello **данные из сеанса отладки** представление для телеметрии, созданные в hello серверная часть приложения.</span><span class="sxs-lookup"><span data-stu-id="11aaa-161">In hello Visual Studio Application Insights Search window, see hello **Data from Debug session** view for telemetry generated in hello server side of your app.</span></span> <span data-ttu-id="11aaa-162">Поэкспериментируйте с фильтрами hello и щелкните любое событие toosee более подробно.</span><span class="sxs-lookup"><span data-stu-id="11aaa-162">Experiment with hello filters, and click any event toosee more detail.</span></span>

![Снимок экрана: hello, представления данных из сеанса отладки в окне приветствия Application Insights.](./media/app-insights-asp-net/55.png)

> [!NOTE]
> <span data-ttu-id="11aaa-164">Если данные не отображаются, убедитесь, что диапазон времени hello указано правильно и щелкните значок поиска hello.</span><span class="sxs-lookup"><span data-stu-id="11aaa-164">If you don't see any data, make sure hello time range is correct, and click hello Search icon.</span></span>

<span data-ttu-id="11aaa-165">[Дополнительные сведения о средствах Application Insights в Visual Studio](app-insights-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="11aaa-165">[Learn more about Application Insights tools in Visual Studio](app-insights-visual-studio.md).</span></span>

<a name="monitor"></a>
### <a name="see-telemetry-in-web-portal"></a><span data-ttu-id="11aaa-166">Просмотр данных телеметрии на веб-портале</span><span class="sxs-lookup"><span data-stu-id="11aaa-166">See telemetry in web portal</span></span>

<span data-ttu-id="11aaa-167">Также видно телеметрии на веб-портале Application Insights hello (если не выбран только hello tooinstall SDK).</span><span class="sxs-lookup"><span data-stu-id="11aaa-167">You can also see telemetry in hello Application Insights web portal (unless you chose tooinstall only hello SDK).</span></span> <span data-ttu-id="11aaa-168">портал Hello имеет дополнительные диаграммы, аналитических средств и компонентов между представлениями, чем Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="11aaa-168">hello portal has more charts, analytic tools, and cross-component views than Visual Studio.</span></span> <span data-ttu-id="11aaa-169">портал Hello также предоставляет предупреждения.</span><span class="sxs-lookup"><span data-stu-id="11aaa-169">hello portal also provides alerts.</span></span>

<span data-ttu-id="11aaa-170">Откройте ресурс Application Insights.</span><span class="sxs-lookup"><span data-stu-id="11aaa-170">Open your Application Insights resource.</span></span> <span data-ttu-id="11aaa-171">Либо войти toohello [портал Azure](https://portal.azure.com/) и найти его, или щелкните правой кнопкой мыши hello проект в Visual Studio и позвольте ему перейти на него.</span><span class="sxs-lookup"><span data-stu-id="11aaa-171">Either sign in toohello [Azure portal](https://portal.azure.com/) and find it there, or right-click hello project in Visual Studio, and let it take you there.</span></span>

![Снимок экрана в Visual Studio, показывающий, как tooopen hello портале Application Insights](./media/app-insights-asp-net/appinsights-04-openPortal.png)

> [!NOTE]
> <span data-ttu-id="11aaa-173">Если возникает ошибка доступа: имеется более одного набора учетных данных Майкрософт, и вы вошли hello не тот набор?</span><span class="sxs-lookup"><span data-stu-id="11aaa-173">If you get an access error: Do you have more than one set of Microsoft credentials, and are you signed in with hello wrong set?</span></span> <span data-ttu-id="11aaa-174">На портале hello выйдите из системы и войти в систему.</span><span class="sxs-lookup"><span data-stu-id="11aaa-174">In hello portal, sign out and sign in again.</span></span>

<span data-ttu-id="11aaa-175">Откроется портал Hello на представлении hello телеметрии из приложения.</span><span class="sxs-lookup"><span data-stu-id="11aaa-175">hello portal opens on a view of hello telemetry from your app.</span></span>

![Снимок экрана, где отображается страница с обзором Application Insights](./media/app-insights-asp-net/66.png)

<span data-ttu-id="11aaa-177">На портале hello щелкните любой плитки или диаграммы toosee более подробно.</span><span class="sxs-lookup"><span data-stu-id="11aaa-177">In hello portal, click any tile or chart toosee more detail.</span></span>

<span data-ttu-id="11aaa-178">[Дополнительные сведения об использовании Application Insights в hello портал Azure](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="11aaa-178">[Learn more about using Application Insights in hello Azure portal](app-insights-dashboards.md).</span></span>

## <a name="step-4-publish-your-app"></a><span data-ttu-id="11aaa-179">Шах 4. Публикация приложения</span><span class="sxs-lookup"><span data-stu-id="11aaa-179">Step 4: Publish your app</span></span>
<span data-ttu-id="11aaa-180">Опубликуйте на сервере IIS tooyour приложения или tooAzure.</span><span class="sxs-lookup"><span data-stu-id="11aaa-180">Publish your app tooyour IIS server or tooAzure.</span></span> <span data-ttu-id="11aaa-181">Контрольное значение [обновляющегося потока метрики](app-insights-metrics-explorer.md#live-metrics-stream) toomake убедиться, что все работает плавно.</span><span class="sxs-lookup"><span data-stu-id="11aaa-181">Watch [Live Metrics Stream](app-insights-metrics-explorer.md#live-metrics-stream) toomake sure everything is running smoothly.</span></span>

<span data-ttu-id="11aaa-182">Накапливает телеметрии в Application Insights hello портал, где мониторинг метрик, поиск телеметрии и настроить [панелей мониторинга](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="11aaa-182">Your telemetry builds up in hello Application Insights portal, where you can monitor metrics, search your telemetry, and set up [dashboards](app-insights-dashboards.md).</span></span> <span data-ttu-id="11aaa-183">Можно также использовать hello мощные [языка запросов анализа журналов](https://docs.loganalytics.io/) tooanalyze об использовании и производительности или toofind определенных событий.</span><span class="sxs-lookup"><span data-stu-id="11aaa-183">You can also use hello powerful [Log Analytics query language](https://docs.loganalytics.io/) tooanalyze usage and performance, or toofind specific events.</span></span>

<span data-ttu-id="11aaa-184">Вы также можете продолжить tooanalyze телеметрии в [Visual Studio](app-insights-visual-studio.md), с помощью средства, такие как поиск диагностики и [тенденции](app-insights-visual-studio-trends.md).</span><span class="sxs-lookup"><span data-stu-id="11aaa-184">You can also continue tooanalyze your telemetry in [Visual Studio](app-insights-visual-studio.md), with tools such as diagnostic search and [trends](app-insights-visual-studio-trends.md).</span></span>

> [!NOTE]
> <span data-ttu-id="11aaa-185">Если приложение отправляет достаточно hello телеметрии tooapproach [ограничивает](app-insights-pricing.md#limits-summary)автоматической [выборки](app-insights-sampling.md) переключается.</span><span class="sxs-lookup"><span data-stu-id="11aaa-185">If your app sends enough telemetry tooapproach hello [throttling limits](app-insights-pricing.md#limits-summary), automatic [sampling](app-insights-sampling.md) switches on.</span></span> <span data-ttu-id="11aaa-186">Выборка снижает количество hello телеметрии, отправляемых из приложения, во время сохранения связанных данных в целях диагностики.</span><span class="sxs-lookup"><span data-stu-id="11aaa-186">Sampling reduces hello quantity of telemetry sent from your app, while preserving correlated data for diagnostic purposes.</span></span>
>
>

## <span data-ttu-id="11aaa-187"><a name="land"></a>Все готово</span><span class="sxs-lookup"><span data-stu-id="11aaa-187"><a name="land"></a> You're all set</span></span>

<span data-ttu-id="11aaa-188">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="11aaa-188">Congratulations!</span></span> <span data-ttu-id="11aaa-189">Установленный пакет Application Insights hello в приложении и настроена служба Application Insights toohello toosend телеметрии на Azure.</span><span class="sxs-lookup"><span data-stu-id="11aaa-189">You installed hello Application Insights package in your app, and configured it toosend telemetry toohello Application Insights service on Azure.</span></span>

![Диаграмма перемещения данных телеметрии](./media/app-insights-asp-net/01-scheme.png)

<span data-ttu-id="11aaa-191">ресурс Azure, который получает телеметрии приложения Hello определяется *ключ инструментирования*.</span><span class="sxs-lookup"><span data-stu-id="11aaa-191">hello Azure resource that receives your app's telemetry is identified by an *instrumentation key*.</span></span> <span data-ttu-id="11aaa-192">Этот ключ можно найти в файле ApplicationInsights.config hello.</span><span class="sxs-lookup"><span data-stu-id="11aaa-192">You'll find this key in hello ApplicationInsights.config file.</span></span>


## <a name="upgrade-toofuture-sdk-versions"></a><span data-ttu-id="11aaa-193">Обновление версии пакета SDK toofuture</span><span class="sxs-lookup"><span data-stu-id="11aaa-193">Upgrade toofuture SDK versions</span></span>
<span data-ttu-id="11aaa-194">tooupgrade tooa [новый выпуск пакета SDK для hello](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases)откройте hello **диспетчера пакетов NuGet** еще раз и фильтр для установленных пакетов.</span><span class="sxs-lookup"><span data-stu-id="11aaa-194">tooupgrade tooa [new release of hello SDK](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases), open hello **NuGet package manager** again, and filter on installed packages.</span></span> <span data-ttu-id="11aaa-195">Выберите элемент **Microsoft.ApplicationInsights.Web**, а затем — элемент **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="11aaa-195">Select **Microsoft.ApplicationInsights.Web**, and choose **Upgrade**.</span></span>

<span data-ttu-id="11aaa-196">При внесении любого tooApplicationInsights.config настроек, сохраните ее копию перед обновлением.</span><span class="sxs-lookup"><span data-stu-id="11aaa-196">If you made any customizations tooApplicationInsights.config, save a copy of it before you upgrade.</span></span> <span data-ttu-id="11aaa-197">Затем объединить изменения в новой версии hello.</span><span class="sxs-lookup"><span data-stu-id="11aaa-197">Then, merge your changes into hello new version.</span></span>

## <a name="video"></a><span data-ttu-id="11aaa-198">Видео</span><span class="sxs-lookup"><span data-stu-id="11aaa-198">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="11aaa-199">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="11aaa-199">Next steps</span></span>

### <a name="more-telemetry"></a><span data-ttu-id="11aaa-200">Дополнительные данные телеметрии</span><span class="sxs-lookup"><span data-stu-id="11aaa-200">More telemetry</span></span>

* <span data-ttu-id="11aaa-201">**[Данные загрузки браузера и страниц](app-insights-javascript.md)** — вставьте фрагмент кода в веб-страницы.</span><span class="sxs-lookup"><span data-stu-id="11aaa-201">**[Browser and page load data](app-insights-javascript.md)** - Insert a code snippet in your web pages.</span></span>
* <span data-ttu-id="11aaa-202">**[Более подробные зависимости и данные отслеживание исключений](app-insights-monitor-performance-live-website-now.md)** — установите монитор состояния на сервере.</span><span class="sxs-lookup"><span data-stu-id="11aaa-202">**[Get more detailed dependency and exception monitoring](app-insights-monitor-performance-live-website-now.md)** - Install Status Monitor on your server.</span></span>
* <span data-ttu-id="11aaa-203">**[Пользовательские события кода](app-insights-api-custom-events-metrics.md)**  toocount, время, или меры действия пользователя.</span><span class="sxs-lookup"><span data-stu-id="11aaa-203">**[Code custom events](app-insights-api-custom-events-metrics.md)** toocount, time, or measure user actions.</span></span>
* <span data-ttu-id="11aaa-204">**[Получение данных журнала](app-insights-asp-net-trace-logs.md)** — согласовывайте данные журналов с данными телеметрии.</span><span class="sxs-lookup"><span data-stu-id="11aaa-204">**[Get log data](app-insights-asp-net-trace-logs.md)** - Correlate log data with your telemetry.</span></span>

### <a name="analysis"></a><span data-ttu-id="11aaa-205">Анализ</span><span class="sxs-lookup"><span data-stu-id="11aaa-205">Analysis</span></span>

* <span data-ttu-id="11aaa-206">**[Работа с Application Insights в Visual Studio](app-insights-visual-studio.md)**</span><span class="sxs-lookup"><span data-stu-id="11aaa-206">**[Working with Application Insights in Visual Studio](app-insights-visual-studio.md)**</span></span><br/><span data-ttu-id="11aaa-207">Содержит сведения об отладке с телеметрии, диагностики поиска и детализация toocode.</span><span class="sxs-lookup"><span data-stu-id="11aaa-207">Includes information about debugging with telemetry, diagnostic search, and drill through toocode.</span></span>
* <span data-ttu-id="11aaa-208">**[Работа с порталом Application Insights hello](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="11aaa-208">**[Working with hello Application Insights portal](app-insights-dashboards.md)**</span></span><br/> <span data-ttu-id="11aaa-209">Содержит сведения о панелях мониторинга, эффективных средствах диагностики и анализа, оповещениях, картах динамических зависимостей приложения, а также сведения об экспорте данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="11aaa-209">Includes information about dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and telemetry export.</span></span>
* <span data-ttu-id="11aaa-210">**[Аналитика](app-insights-analytics-tour.md)**  -hello запросами языка.</span><span class="sxs-lookup"><span data-stu-id="11aaa-210">**[Analytics](app-insights-analytics-tour.md)** - hello powerful query language.</span></span>

### <a name="alerts"></a><span data-ttu-id="11aaa-211">Оповещения</span><span class="sxs-lookup"><span data-stu-id="11aaa-211">Alerts</span></span>

* <span data-ttu-id="11aaa-212">[Проверяет доступность](app-insights-monitor-web-app-availability.md): Создание тестов toomake убедиться, что веб-сайт будет видимым в веб-hello.</span><span class="sxs-lookup"><span data-stu-id="11aaa-212">[Availability tests](app-insights-monitor-web-app-availability.md): Create tests toomake sure your site is visible on hello web.</span></span>
* <span data-ttu-id="11aaa-213">[Интеллектуальные диагностики](app-insights-proactive-diagnostics.md): эти тесты выполняются автоматически, поэтому не нужно toodo любые tooset их вверх.</span><span class="sxs-lookup"><span data-stu-id="11aaa-213">[Smart diagnostics](app-insights-proactive-diagnostics.md): These tests run automatically, so you don't have toodo anything tooset them up.</span></span> <span data-ttu-id="11aaa-214">Благодаря ей вы узнаете о необычном количестве неудачных запросов.</span><span class="sxs-lookup"><span data-stu-id="11aaa-214">They tell you if your app has an unusual rate of failed requests.</span></span>
* <span data-ttu-id="11aaa-215">[Метрики оповещений](app-insights-alerts.md): задайте эти toowarn вы метрики пересекает пороговое значение.</span><span class="sxs-lookup"><span data-stu-id="11aaa-215">[Metric alerts](app-insights-alerts.md): Set these toowarn you if a metric crosses a threshold.</span></span> <span data-ttu-id="11aaa-216">Их можно настроить для пользовательских метрик, добавляемых в код приложения.</span><span class="sxs-lookup"><span data-stu-id="11aaa-216">You can set them on custom metrics that you code into your app.</span></span>

### <a name="automation"></a><span data-ttu-id="11aaa-217">Служба автоматизации</span><span class="sxs-lookup"><span data-stu-id="11aaa-217">Automation</span></span>

* [<span data-ttu-id="11aaa-218">Создание ресурсов Application Insights с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="11aaa-218">Automate creating an Application Insights resource</span></span>](app-insights-powershell.md)
