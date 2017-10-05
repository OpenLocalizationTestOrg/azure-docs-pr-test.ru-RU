---
title: "Настройка аналитики веб-приложения для ASP.NET с помощью Azure Application Insights | Документация Майкрософт"
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
ms.openlocfilehash: cb247ee68da88265f7c51258644064463d44f8b5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="set-up-application-insights-for-your-aspnet-website"></a><span data-ttu-id="11ff7-103">Настройка Application Insights для веб-сайта ASP.NET</span><span class="sxs-lookup"><span data-stu-id="11ff7-103">Set up Application Insights for your ASP.NET website</span></span>

<span data-ttu-id="11ff7-104">Эта процедура настраивает веб-приложение ASP.NET для отправки данных телеметрии в службу [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="11ff7-104">This procedure configures your ASP.NET web app to send telemetry to the [Azure Application Insights](app-insights-overview.md) service.</span></span> <span data-ttu-id="11ff7-105">Она работает для приложений ASP.NET, размещенных на сервере IIS или в облаке.</span><span class="sxs-lookup"><span data-stu-id="11ff7-105">It works for ASP.NET apps that are hosted either in your own IIS server or in the Cloud.</span></span> <span data-ttu-id="11ff7-106">Она предоставляет диаграммы и эффективный язык запросов, который поможет определить производительность приложений и способ использования приложений пользователями, а также автоматические оповещения о сбоях или проблемах с производительностью.</span><span class="sxs-lookup"><span data-stu-id="11ff7-106">You get charts and a powerful query language that help you understand the performance of your app and how people are using it, plus automatic alerts on failures or performance issues.</span></span> <span data-ttu-id="11ff7-107">Многим разработчикам нравятся эти функции в изначальном виде, но при необходимости их можно расширить и настроить данные телеметрии.</span><span class="sxs-lookup"><span data-stu-id="11ff7-107">Many developers find these features great as they are, but you can also extend and customize the telemetry if you need to.</span></span>

<span data-ttu-id="11ff7-108">Настройка выполняется несколькими щелчками в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="11ff7-108">Setup takes just a few clicks in Visual Studio.</span></span> <span data-ttu-id="11ff7-109">Вы можете избежать расходов, ограничив объем телеметрии.</span><span class="sxs-lookup"><span data-stu-id="11ff7-109">You have the option to avoid charges by limiting the volume of telemetry.</span></span> <span data-ttu-id="11ff7-110">Это позволяет экспериментировать и выполнять отладку или наблюдать за сайтом с небольшим числом пользователей.</span><span class="sxs-lookup"><span data-stu-id="11ff7-110">This allows you to experiment and debug, or to monitor a site with not many users.</span></span> <span data-ttu-id="11ff7-111">Если вы хотите отслеживать рабочий сайт, вы можете легко увеличить лимит позже.</span><span class="sxs-lookup"><span data-stu-id="11ff7-111">When you decide you want to go ahead and monitor your production site, it's easy to raise the limit later.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="11ff7-112">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="11ff7-112">Before you start</span></span>
<span data-ttu-id="11ff7-113">Вам необходимы:</span><span class="sxs-lookup"><span data-stu-id="11ff7-113">You need:</span></span>

* <span data-ttu-id="11ff7-114">Visual Studio 2013 с обновлением 3 или более новая версия.</span><span class="sxs-lookup"><span data-stu-id="11ff7-114">Visual Studio 2013 update 3 or later.</span></span> <span data-ttu-id="11ff7-115">Чем новее версия, тем лучше.</span><span class="sxs-lookup"><span data-stu-id="11ff7-115">Later is better.</span></span>
* <span data-ttu-id="11ff7-116">подписка на [Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="11ff7-116">A subscription to [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="11ff7-117">Если у вашей группы или организации есть подписка Azure, владелец может добавить вас в нее с помощью вашей [учетной записи Майкрософт](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="11ff7-117">If your team or organization has an Azure subscription, the owner can add you to it, by using your [Microsoft account](http://live.com).</span></span>

<span data-ttu-id="11ff7-118">Существуют и другие статьи, к которым можно обратиться, если вас интересуют такие темы, как:</span><span class="sxs-lookup"><span data-stu-id="11ff7-118">There are alternative topics to look at if you are interested in:</span></span>

* [<span data-ttu-id="11ff7-119">инструментирование веб-приложения во время выполнения;</span><span class="sxs-lookup"><span data-stu-id="11ff7-119">Instrumenting a web app at runtime</span></span>](app-insights-monitor-performance-live-website-now.md)
* [<span data-ttu-id="11ff7-120">облачных служб Azure</span><span class="sxs-lookup"><span data-stu-id="11ff7-120">Azure Cloud Services</span></span>](app-insights-cloudservices.md)

## <span data-ttu-id="11ff7-121"><a name="ide"></a> Шаг 1. Добавление пакета SDK Application Insights</span><span class="sxs-lookup"><span data-stu-id="11ff7-121"><a name="ide"></a> Step 1: Add the Application Insights SDK</span></span>

<span data-ttu-id="11ff7-122">В обозревателе решений щелкните проект веб-приложения правой кнопкой мыши и выберите пункт **Добавить** > **Телеметрия Application Insights** или **Настроить Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="11ff7-122">Right-click your web app project in Solution Explorer, and choose **Add** > **Application Insights Telemetry...** or **Configure Application Insights**.</span></span>

![Снимок экрана с окном обозревателя решений, где выделен параметр "Добавить" и "Телеметрия Application Insights"](./media/app-insights-asp-net/appinsights-03-addExisting.png)

<span data-ttu-id="11ff7-124">(В Visual Studio 2015 есть параметр, который позволяет добавить Application Insights в диалоговое окно создания проекта.)</span><span class="sxs-lookup"><span data-stu-id="11ff7-124">(In Visual Studio 2015, there's also an option to add Application Insights in the New Project dialog.)</span></span>

<span data-ttu-id="11ff7-125">Перейдите на страницу настройки Application Insights.</span><span class="sxs-lookup"><span data-stu-id="11ff7-125">Continue to the Application Insights configuration page:</span></span>

![Снимок экрана с окном страницы "Зарегистрировать приложение в Application Insights"](./media/app-insights-asp-net/visual-studio-register-dialog.png)

<span data-ttu-id="11ff7-127">**а.**</span><span class="sxs-lookup"><span data-stu-id="11ff7-127">**a.**</span></span> <span data-ttu-id="11ff7-128">Выберите учетную запись и подписку, которые будут использоваться для доступа к Azure.</span><span class="sxs-lookup"><span data-stu-id="11ff7-128">Select the account and subscription that you use to access Azure.</span></span>

<span data-ttu-id="11ff7-129">**б.**</span><span class="sxs-lookup"><span data-stu-id="11ff7-129">**b.**</span></span> <span data-ttu-id="11ff7-130">Выберите ресурс в Azure, в котором должны отображаться данные из приложения.</span><span class="sxs-lookup"><span data-stu-id="11ff7-130">Select the resource in Azure where you want to see the data from your app.</span></span> <span data-ttu-id="11ff7-131">Обычно:</span><span class="sxs-lookup"><span data-stu-id="11ff7-131">Usually:</span></span>

* <span data-ttu-id="11ff7-132">Используйте [один ресурс для разных компонентов](app-insights-monitor-multi-role-apps.md) одного приложения.</span><span class="sxs-lookup"><span data-stu-id="11ff7-132">Use a [single resource for different components](app-insights-monitor-multi-role-apps.md) of a single application.</span></span> 
* <span data-ttu-id="11ff7-133">Создавайте разные ресурсы для несвязанных приложений.</span><span class="sxs-lookup"><span data-stu-id="11ff7-133">Create separate resources for unrelated applications.</span></span>
 
<span data-ttu-id="11ff7-134">Если вы хотите задать группу ресурсов или расположение, где будут храниться данные, щелкните **Настроить параметры**.</span><span class="sxs-lookup"><span data-stu-id="11ff7-134">If you want to set the resource group or the location where your data is stored, click **Configure settings**.</span></span> <span data-ttu-id="11ff7-135">Группы ресурсов используются для управления доступом к данным.</span><span class="sxs-lookup"><span data-stu-id="11ff7-135">Resource groups are used to control access to data.</span></span> <span data-ttu-id="11ff7-136">Например, если имеется несколько приложений, которые являются частью одной системы, вы можете поместить их данные Application Insights в одну группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="11ff7-136">For example, if you have several apps that form part of the same system, you might put their Application Insights data in the same resource group.</span></span>

<span data-ttu-id="11ff7-137">**в.**</span><span class="sxs-lookup"><span data-stu-id="11ff7-137">**c.**</span></span> <span data-ttu-id="11ff7-138">Задайте максимальное ограничение объема свободных данных, чтобы избежать ненужных расходов.</span><span class="sxs-lookup"><span data-stu-id="11ff7-138">Set a cap at the free data volume limit, to avoid charges.</span></span> <span data-ttu-id="11ff7-139">Служба Application Insights является бесплатной до определенного объема данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="11ff7-139">Application Insights is free up to a certain volume of telemetry.</span></span> <span data-ttu-id="11ff7-140">После создания ресурса можно изменить выбранные параметры на портале, открыв **Компоненты и расценки** > **Управление данными** > **Ограничение ежедневного объема**.</span><span class="sxs-lookup"><span data-stu-id="11ff7-140">After the resource is created, you can change your selection in the portal by opening  **Features + pricing** > **Data volume management** > **Daily volume cap**.</span></span>

<span data-ttu-id="11ff7-141">**г.**</span><span class="sxs-lookup"><span data-stu-id="11ff7-141">**d.**</span></span> <span data-ttu-id="11ff7-142">Щелкните **Регистрация**, чтобы приступить к настройке Application Insights для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="11ff7-142">Click **Register** to go ahead and configure Application Insights for your web app.</span></span> <span data-ttu-id="11ff7-143">Данные телеметрии будут отправляться на [портал Azure](https://portal.azure.com) как во время отладки, так и после публикации приложения.</span><span class="sxs-lookup"><span data-stu-id="11ff7-143">Telemetry will be sent to the [Azure portal](https://portal.azure.com), both during debugging and after you have published your app.</span></span>

<span data-ttu-id="11ff7-144">**д.**</span><span class="sxs-lookup"><span data-stu-id="11ff7-144">**e.**</span></span> <span data-ttu-id="11ff7-145">Если вы не хотите отправлять данные телеметрии на портал во время отладки, просто добавьте пакет SDK Application Insights в приложение, но не настраивайте ресурс на портале.</span><span class="sxs-lookup"><span data-stu-id="11ff7-145">If you don't want to send telemetry to the portal while you're debugging, just add the Application Insights SDK to your app but don't configure a resource in the portal.</span></span> <span data-ttu-id="11ff7-146">Во время отладки можно будет просмотреть данные телеметрии в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="11ff7-146">You will be able to see telemetry in Visual Studio while you are debugging.</span></span> <span data-ttu-id="11ff7-147">Позже вы сможете вернуться на эту страницу настроек или можете дождаться, когда приложение будет развернуто, и [переключиться на данные телеметрии во время выполнения](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="11ff7-147">Later, you can return to this configuration page, or you could wait until after you have deployed your app and [switch on telemetry at run time](app-insights-monitor-performance-live-website-now.md).</span></span>


## <span data-ttu-id="11ff7-148"><a name="run"></a> Шаг 2. Запуск приложения</span><span class="sxs-lookup"><span data-stu-id="11ff7-148"><a name="run"></a> Step 2: Run your app</span></span>
<span data-ttu-id="11ff7-149">Запустите приложение, нажав клавишу F5.</span><span class="sxs-lookup"><span data-stu-id="11ff7-149">Run your app with F5.</span></span> <span data-ttu-id="11ff7-150">Откройте разные страницы, чтобы создать некоторый объем данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="11ff7-150">Open different pages to generate some telemetry.</span></span>

<span data-ttu-id="11ff7-151">В Visual Studio вы увидите число записанных в журнал событий.</span><span class="sxs-lookup"><span data-stu-id="11ff7-151">In Visual Studio, you see a count of the events that have been logged.</span></span>

![Снимок экрана, где отображается Visual Studio](./media/app-insights-asp-net/54.png)

## <a name="step-3-see-your-telemetry"></a><span data-ttu-id="11ff7-154">Шаг 3. Просмотр данных телеметрии</span><span class="sxs-lookup"><span data-stu-id="11ff7-154">Step 3: See your telemetry</span></span>
<span data-ttu-id="11ff7-155">Вы можете просмотреть данные телеметрии в Visual Studio или на веб-портале Application Insights.</span><span class="sxs-lookup"><span data-stu-id="11ff7-155">You can see your telemetry either in Visual Studio or in the Application Insights web portal.</span></span> <span data-ttu-id="11ff7-156">Выполните поиск данных телеметрии в Visual Studio для отладки приложения.</span><span class="sxs-lookup"><span data-stu-id="11ff7-156">Search telemetry in Visual Studio to help you debug your app.</span></span> <span data-ttu-id="11ff7-157">Отслеживайте производительность и использование на веб-портале в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="11ff7-157">Monitor performance and usage in the web portal when your system is live.</span></span> 

### <a name="see-your-telemetry-in-visual-studio"></a><span data-ttu-id="11ff7-158">Просмотр данных телеметрии в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="11ff7-158">See your telemetry in Visual Studio</span></span>

<span data-ttu-id="11ff7-159">В Visual Studio откройте окно Application Insights.</span><span class="sxs-lookup"><span data-stu-id="11ff7-159">In Visual Studio, open the Application Insights window.</span></span> <span data-ttu-id="11ff7-160">Нажмите кнопку **Application Insights** или щелкните проект в обозревателе решений правой кнопкой мыши, выберите **Application Insights**, а затем щелкните **Поиск действующей телеметрии**.</span><span class="sxs-lookup"><span data-stu-id="11ff7-160">Either click the **Application Insights** button, or right-click your project in Solution Explorer, select **Application Insights**, and then click **Search Live Telemetry**.</span></span>

<span data-ttu-id="11ff7-161">В окне поиска Application Insights в Visual Studio просмотрите представление **данных, полученных в ходе сеанса отладки**, где отображаются данные телеметрии, созданные в серверной части приложения.</span><span class="sxs-lookup"><span data-stu-id="11ff7-161">In the Visual Studio Application Insights Search window, see the **Data from Debug session** view for telemetry generated in the server side of your app.</span></span> <span data-ttu-id="11ff7-162">Поэкспериментируйте с фильтрами и щелкните любое событие, чтобы просмотреть подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="11ff7-162">Experiment with the filters, and click any event to see more detail.</span></span>

![Снимок экрана, где показано представление данных, полученных в ходе сеанса отладки, в окне Application Insights.](./media/app-insights-asp-net/55.png)

> [!NOTE]
> <span data-ttu-id="11ff7-164">Если данные не отображаются, проверьте диапазон времени и щелкните значок поиска.</span><span class="sxs-lookup"><span data-stu-id="11ff7-164">If you don't see any data, make sure the time range is correct, and click the Search icon.</span></span>

<span data-ttu-id="11ff7-165">[Дополнительные сведения о средствах Application Insights в Visual Studio](app-insights-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="11ff7-165">[Learn more about Application Insights tools in Visual Studio](app-insights-visual-studio.md).</span></span>

<a name="monitor"></a>
### <a name="see-telemetry-in-web-portal"></a><span data-ttu-id="11ff7-166">Просмотр данных телеметрии на веб-портале</span><span class="sxs-lookup"><span data-stu-id="11ff7-166">See telemetry in web portal</span></span>

<span data-ttu-id="11ff7-167">Вы можете также просматривать данные телеметрии на веб-портале Application Insights, если только не решили установить только пакет SDK.</span><span class="sxs-lookup"><span data-stu-id="11ff7-167">You can also see telemetry in the Application Insights web portal (unless you chose to install only the SDK).</span></span> <span data-ttu-id="11ff7-168">На портале представлено больше дополнительных диаграмм, средств анализа и представлений различных компонентов, чем в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="11ff7-168">The portal has more charts, analytic tools, and cross-component views than Visual Studio.</span></span> <span data-ttu-id="11ff7-169">На портале также доступны оповещения.</span><span class="sxs-lookup"><span data-stu-id="11ff7-169">The portal also provides alerts.</span></span>

<span data-ttu-id="11ff7-170">Откройте ресурс Application Insights.</span><span class="sxs-lookup"><span data-stu-id="11ff7-170">Open your Application Insights resource.</span></span> <span data-ttu-id="11ff7-171">Войдите на [портал Azure](https://portal.azure.com/) и найдите его там или щелкните правой кнопкой мыши проект в Visual Studio и перейдите к нему.</span><span class="sxs-lookup"><span data-stu-id="11ff7-171">Either sign in to the [Azure portal](https://portal.azure.com/) and find it there, or right-click the project in Visual Studio, and let it take you there.</span></span>

![Снимок экрана с окном Visual Studio, где показано, как открыть портал Application Insights](./media/app-insights-asp-net/appinsights-04-openPortal.png)

> [!NOTE]
> <span data-ttu-id="11ff7-173">Если произошла ошибка доступа, возможно, у вас есть несколько наборов учетных данных Майкрософт и вы использовали для входа неправильный набор.</span><span class="sxs-lookup"><span data-stu-id="11ff7-173">If you get an access error: Do you have more than one set of Microsoft credentials, and are you signed in with the wrong set?</span></span> <span data-ttu-id="11ff7-174">На портале повторите процедуру выхода и входа.</span><span class="sxs-lookup"><span data-stu-id="11ff7-174">In the portal, sign out and sign in again.</span></span>

<span data-ttu-id="11ff7-175">На портале откроется представление данных телеметрии из приложения.</span><span class="sxs-lookup"><span data-stu-id="11ff7-175">The portal opens on a view of the telemetry from your app.</span></span>

![Снимок экрана, где отображается страница с обзором Application Insights](./media/app-insights-asp-net/66.png)

<span data-ttu-id="11ff7-177">На портале щелкните любую плитку, чтобы просмотреть подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="11ff7-177">In the portal, click any tile or chart to see more detail.</span></span>

<span data-ttu-id="11ff7-178">[Дополнительные сведения об использовании Application Insights на портале Azure](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="11ff7-178">[Learn more about using Application Insights in the Azure portal](app-insights-dashboards.md).</span></span>

## <a name="step-4-publish-your-app"></a><span data-ttu-id="11ff7-179">Шах 4. Публикация приложения</span><span class="sxs-lookup"><span data-stu-id="11ff7-179">Step 4: Publish your app</span></span>
<span data-ttu-id="11ff7-180">Опубликуйте приложение на сервере IIS или в Azure.</span><span class="sxs-lookup"><span data-stu-id="11ff7-180">Publish your app to your IIS server or to Azure.</span></span> <span data-ttu-id="11ff7-181">Просмотрите [динамический поток метрик](app-insights-metrics-explorer.md#live-metrics-stream), чтобы убедиться в бесперебойной работе приложения.</span><span class="sxs-lookup"><span data-stu-id="11ff7-181">Watch [Live Metrics Stream](app-insights-metrics-explorer.md#live-metrics-stream) to make sure everything is running smoothly.</span></span>

<span data-ttu-id="11ff7-182">Телеметрия создается на портале Application Insights, где можно отслеживать метрики, выполнять поиск данных телеметрии и настраивать [панели мониторинга](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="11ff7-182">Your telemetry builds up in the Application Insights portal, where you can monitor metrics, search your telemetry, and set up [dashboards](app-insights-dashboards.md).</span></span> <span data-ttu-id="11ff7-183">Можно также использовать эффективный [язык запросов Log Analytics](https://docs.loganalytics.io/) для анализа использования и производительности или поиска определенных событий.</span><span class="sxs-lookup"><span data-stu-id="11ff7-183">You can also use the powerful [Log Analytics query language](https://docs.loganalytics.io/) to analyze usage and performance, or to find specific events.</span></span>

<span data-ttu-id="11ff7-184">Кроме того, можно продолжить анализировать телеметрию в [Visual Studio](app-insights-visual-studio.md) с помощью таких средств, как поиск по журналу диагностики и [тренды](app-insights-visual-studio-trends.md).</span><span class="sxs-lookup"><span data-stu-id="11ff7-184">You can also continue to analyze your telemetry in [Visual Studio](app-insights-visual-studio.md), with tools such as diagnostic search and [trends](app-insights-visual-studio-trends.md).</span></span>

> [!NOTE]
> <span data-ttu-id="11ff7-185">Если приложение отправляет достаточно данных телеметрии для достижения [пределов регулирования](app-insights-pricing.md#limits-summary), включается автоматическая [выборка](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="11ff7-185">If your app sends enough telemetry to approach the [throttling limits](app-insights-pricing.md#limits-summary), automatic [sampling](app-insights-sampling.md) switches on.</span></span> <span data-ttu-id="11ff7-186">Выборка позволяет уменьшить количество данных телеметрии, отправляемых из приложения, сохраняя связанные данные в целях диагностики.</span><span class="sxs-lookup"><span data-stu-id="11ff7-186">Sampling reduces the quantity of telemetry sent from your app, while preserving correlated data for diagnostic purposes.</span></span>
>
>

## <span data-ttu-id="11ff7-187"><a name="land"></a>Все готово</span><span class="sxs-lookup"><span data-stu-id="11ff7-187"><a name="land"></a> You're all set</span></span>

<span data-ttu-id="11ff7-188">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="11ff7-188">Congratulations!</span></span> <span data-ttu-id="11ff7-189">Вы установили в приложение пакет Application Insights и настроили его для отправки данных телеметрии в службу Application Insights в Azure.</span><span class="sxs-lookup"><span data-stu-id="11ff7-189">You installed the Application Insights package in your app, and configured it to send telemetry to the Application Insights service on Azure.</span></span>

![Диаграмма перемещения данных телеметрии](./media/app-insights-asp-net/01-scheme.png)

<span data-ttu-id="11ff7-191">Ресурс Azure, который получает данные телеметрии приложения, определяется *ключом инструментирования*.</span><span class="sxs-lookup"><span data-stu-id="11ff7-191">The Azure resource that receives your app's telemetry is identified by an *instrumentation key*.</span></span> <span data-ttu-id="11ff7-192">Вы найдете этот ключ в файле ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="11ff7-192">You'll find this key in the ApplicationInsights.config file.</span></span>


## <a name="upgrade-to-future-sdk-versions"></a><span data-ttu-id="11ff7-193">Обновление до будущих версий пакета SDK</span><span class="sxs-lookup"><span data-stu-id="11ff7-193">Upgrade to future SDK versions</span></span>
<span data-ttu-id="11ff7-194">Чтобы установить [новый выпуск пакета SDK](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases), еще раз откройте **диспетчер пакетов NuGet** и выполните фильтрацию по установленным пакетам.</span><span class="sxs-lookup"><span data-stu-id="11ff7-194">To upgrade to a [new release of the SDK](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases), open the **NuGet package manager** again, and filter on installed packages.</span></span> <span data-ttu-id="11ff7-195">Выберите элемент **Microsoft.ApplicationInsights.Web**, а затем — элемент **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="11ff7-195">Select **Microsoft.ApplicationInsights.Web**, and choose **Upgrade**.</span></span>

<span data-ttu-id="11ff7-196">Если были выполнены какие-либо настройки файла ApplicationInsights.config, то прежде чем выполнять обновление, сохраните его копию.</span><span class="sxs-lookup"><span data-stu-id="11ff7-196">If you made any customizations to ApplicationInsights.config, save a copy of it before you upgrade.</span></span> <span data-ttu-id="11ff7-197">Затем объедините изменения в новой версии.</span><span class="sxs-lookup"><span data-stu-id="11ff7-197">Then, merge your changes into the new version.</span></span>

## <a name="video"></a><span data-ttu-id="11ff7-198">Видео</span><span class="sxs-lookup"><span data-stu-id="11ff7-198">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="11ff7-199">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="11ff7-199">Next steps</span></span>

### <a name="more-telemetry"></a><span data-ttu-id="11ff7-200">Дополнительные данные телеметрии</span><span class="sxs-lookup"><span data-stu-id="11ff7-200">More telemetry</span></span>

* <span data-ttu-id="11ff7-201">**[Данные загрузки браузера и страниц](app-insights-javascript.md)** — вставьте фрагмент кода в веб-страницы.</span><span class="sxs-lookup"><span data-stu-id="11ff7-201">**[Browser and page load data](app-insights-javascript.md)** - Insert a code snippet in your web pages.</span></span>
* <span data-ttu-id="11ff7-202">**[Более подробные зависимости и данные отслеживание исключений](app-insights-monitor-performance-live-website-now.md)** — установите монитор состояния на сервере.</span><span class="sxs-lookup"><span data-stu-id="11ff7-202">**[Get more detailed dependency and exception monitoring](app-insights-monitor-performance-live-website-now.md)** - Install Status Monitor on your server.</span></span>
* <span data-ttu-id="11ff7-203">**[Добавьте в приложение код для пользовательских событий](app-insights-api-custom-events-metrics.md)**, чтобы считать, фиксировать время и измерять действия пользователя.</span><span class="sxs-lookup"><span data-stu-id="11ff7-203">**[Code custom events](app-insights-api-custom-events-metrics.md)** to count, time, or measure user actions.</span></span>
* <span data-ttu-id="11ff7-204">**[Получение данных журнала](app-insights-asp-net-trace-logs.md)** — согласовывайте данные журналов с данными телеметрии.</span><span class="sxs-lookup"><span data-stu-id="11ff7-204">**[Get log data](app-insights-asp-net-trace-logs.md)** - Correlate log data with your telemetry.</span></span>

### <a name="analysis"></a><span data-ttu-id="11ff7-205">Анализ</span><span class="sxs-lookup"><span data-stu-id="11ff7-205">Analysis</span></span>

* <span data-ttu-id="11ff7-206">**[Работа с Application Insights в Visual Studio](app-insights-visual-studio.md)**</span><span class="sxs-lookup"><span data-stu-id="11ff7-206">**[Working with Application Insights in Visual Studio](app-insights-visual-studio.md)**</span></span><br/><span data-ttu-id="11ff7-207">Содержит сведения об отладке с помощью телеметрии, о поиске по журналу диагностики и детализации кода.</span><span class="sxs-lookup"><span data-stu-id="11ff7-207">Includes information about debugging with telemetry, diagnostic search, and drill through to code.</span></span>
* <span data-ttu-id="11ff7-208">**[Работа с порталом Application Insights](app-insights-dashboards.md)**</span><span class="sxs-lookup"><span data-stu-id="11ff7-208">**[Working with the Application Insights portal](app-insights-dashboards.md)**</span></span><br/> <span data-ttu-id="11ff7-209">Содержит сведения о панелях мониторинга, эффективных средствах диагностики и анализа, оповещениях, картах динамических зависимостей приложения, а также сведения об экспорте данных телеметрии.</span><span class="sxs-lookup"><span data-stu-id="11ff7-209">Includes information about dashboards, powerful diagnostic and analytic tools, alerts, a live dependency map of your application, and telemetry export.</span></span>
* <span data-ttu-id="11ff7-210">**[Аналитика](app-insights-analytics-tour.md)** — эффективный язык запросов.</span><span class="sxs-lookup"><span data-stu-id="11ff7-210">**[Analytics](app-insights-analytics-tour.md)** - The powerful query language.</span></span>

### <a name="alerts"></a><span data-ttu-id="11ff7-211">Оповещения</span><span class="sxs-lookup"><span data-stu-id="11ff7-211">Alerts</span></span>

* <span data-ttu-id="11ff7-212">[Тесты доступности.](app-insights-monitor-web-app-availability.md) Создавайте тесты, позволяющие проверить, доступен ли ваш сайт в Интернете.</span><span class="sxs-lookup"><span data-stu-id="11ff7-212">[Availability tests](app-insights-monitor-web-app-availability.md): Create tests to make sure your site is visible on the web.</span></span>
* <span data-ttu-id="11ff7-213">[Интеллектуальная диагностика.](app-insights-proactive-diagnostics.md) Эти тесты выполняются автоматически, поэтому вам не нужно их настраивать.</span><span class="sxs-lookup"><span data-stu-id="11ff7-213">[Smart diagnostics](app-insights-proactive-diagnostics.md): These tests run automatically, so you don't have to do anything to set them up.</span></span> <span data-ttu-id="11ff7-214">Благодаря ей вы узнаете о необычном количестве неудачных запросов.</span><span class="sxs-lookup"><span data-stu-id="11ff7-214">They tell you if your app has an unusual rate of failed requests.</span></span>
* <span data-ttu-id="11ff7-215">[Оповещения о метриках.](app-insights-alerts.md) Настройте их, чтобы получать уведомления в случае, если метрика превысила пороговое значение.</span><span class="sxs-lookup"><span data-stu-id="11ff7-215">[Metric alerts](app-insights-alerts.md): Set these to warn you if a metric crosses a threshold.</span></span> <span data-ttu-id="11ff7-216">Их можно настроить для пользовательских метрик, добавляемых в код приложения.</span><span class="sxs-lookup"><span data-stu-id="11ff7-216">You can set them on custom metrics that you code into your app.</span></span>

### <a name="automation"></a><span data-ttu-id="11ff7-217">Служба автоматизации</span><span class="sxs-lookup"><span data-stu-id="11ff7-217">Automation</span></span>

* [<span data-ttu-id="11ff7-218">Создание ресурсов Application Insights с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="11ff7-218">Automate creating an Application Insights resource</span></span>](app-insights-powershell.md)
